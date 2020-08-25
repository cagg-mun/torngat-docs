... run unusual code on Torngat
===============================

*Tomasz Danek*

*June 10, 2013*

Introduction
------------

Running code utilizing “unusual” parallelisation can be tricky on
Torngat supercomputer. Of course the definition of unusual job vary but
in general it can be assumed that any hybrid process-thread code should
be consider as the one. Probably the most commonly used hybrid codes are
the combinations of MPI processes and OMP threads. This short tutorial
presents how to run this kind of code on Torngat.

“The Code”
----------

Let us consider the very simple MPI/OMP code creating a matrix which
rows and columns represents process and thread number. Each filed of
matrix is a number with first digit/digits defined by process and last
digit defined by thread number. Please note that presented code does not
present the optimal solution of the problem.

.. code-block:: c
   :linenos:

    #include <stdlib.h>
    #include <stdio.h>
    #include <mpi.h>
    #include <omp.h>

    int main (int argc, char *argv[])
    {
    int my_rank;
    int p,n_thr,i,j,x;
    unsigned int **message;

    MPI_Status status;

    MPI_Init(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &my_rank);
    MPI_Comm_size(MPI_COMM_WORLD, &p);

    #pragma omp parallel
    n_thr=omp_get_num_threads();

    message=(unsigned int **) calloc (p,sizeof(unsigned int *));
    for (i=0;i<p;i++)
            message[i]=(unsigned int *) calloc (n_thr,sizeof(unsigned int));

    #pragma omp parallel private(x)
    {
            x=omp_get_thread_num();
            message[my_rank][x]=x+(my_rank+1)*10;
    }

    for (i=0;i<p;i++)
    {
            MPI_Bcast(&message[i][0], n_thr, MPI_INT, i, MPI_COMM_WORLD);
    }

    if (my_rank==0)
    {
            for (i=0;i<p;i++)
            {
                    for (j=0;j<n_thr;j++)
                            fprintf (stderr,"%d ",message[i][j]);
                    fprintf (stderr,"\n");
            }
    }

    MPI_Finalize();
    return (0);
    }


Presented code is very simple but let us focus its most important
parallel part. First of all MPI is initialized and then each process
recognize its number (my\_rank) and size of the MPI\_COMM\_WORD
communicator (p). Then number of OMP threads (n\_thr) is set. Please
note that by default this value is taken from OMP\_NUM\_THREAD system
variable. After memory allocation for matrix message the second parallel
section is stared and process dependent row of the matrix if filled with
proper number representing process (first digit) and thread number
(second digit). Then every process broadcast its row to all other
processes so when communication is finished all process have a copy of
the same matrix. Finally process number 0 sends matrix message to
standard error stream.

This code can be compiled using Intel MPI compiler mpiicc (please note
double i):

.. code-block:: bash

    mpiicc -O3 -xHOST main.c -openmp

How to run it on torngat
------------------------

Let us assume that we want run 30 MPI processes and that every process
should start two threads. In a usual real life situation number of
threads should be equal to number of available cores to secure optimal
code efficiency so in this example user should reserve 60 cores. In
current Torngat configuration each node has 12 cores so for this run 5
nodes should be reserved.

To start and interactive session and reserve sufficient resources we
can, for example, use command:

.. code-block:: bash

    qrsh -cwd -V -q churich.q -pe impi 60 bash

For the explanation of the flags see Torngat user manual.

Then we have to define our own machine file. We can do it using the
script presented bellow:

.. code-block:: bash

    #!/bin/bash

    MakeMachineFile()
    {
      cat $1 | while read line; do
         host=`echo $line|cut -f1 -d" "|cut -f1 -d"."`
         nprocs=`echo $line|cut -f2 -d" "`
         echo "$host:$nprocs"
         np=`expr $np + $nprocs`
      done
    }

    MakeMachineFile $PE_HOSTFILE

After script execution:

.. code-block:: text

    machines > mfile

file with something similar to this should be created:

.. code-block:: text

    cn32:12
    cn24:12
    cn15:12
    cn16:12
    cn07:12

Because we do not want to run 60 processes but 30 with 2 threads number
12 should be changed for 6. If you want to run 15 processes using 4
threads you should put 3 after colon.

Now proper script for our run has to be created. Because behavior of -V
flag can be unpredictable in some SGE configuration it is usually safer
to define all used system variables in this script. The simplest
possible script looks like this:

.. code-block:: bash

    export OMP_NUM_THREADS=2
    ./a.out

Please note that the first line of the script define the number of the
threads used by every process. If omitted most probably only 1 thread
will be used by every process.

When machine and script files are ready job can be stared using mpi job
starter:

.. code:: bash

    mpiexec.hydra -machinefile=mfile -np 30 bash script

and the displayed output should be similar to:

.. code-block:: text

    10 11 
    20 21 
    30 31 
    40 41 
    50 51 
    60 61 
    70 71 
    80 81 
    90 91 
    100 101 
    110 111 
    120 121 
    130 131 
    140 141 
    150 151 
    160 161 
    170 171 
    180 181 
    190 191 
    200 201 
    210 211 
    220 221 
    230 231 
    240 241 
    250 251 
    260 261 
    270 271 
    280 281 
    290 291 
    300 301
    