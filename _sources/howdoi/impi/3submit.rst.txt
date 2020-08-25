To run a program in the Intel MPI environment:
==============================================

Create a script file describing the job:
----------------------------------------

.. code-block:: bash
   :linenos:

    #$ -cwd
    #$ -N hello
    #$ -o hello.output -j y
    #$ -pe impi 32
    #$ -q all.q
    #$ -V

    MakeMachineFile()
    {
      cat $1 | while read line; do
         host=`echo $line|cut -f1 -d" "|cut -f1 -d"."`
         nprocs=`echo $line|cut -f2 -d" "`
         echo "$host:$nprocs"
      done
    }
    MakeMachineFile $PE_HOSTFILE >machines.$JOB_ID

    mpiexec.hydra --machinefile=machines.$JOB_ID /home/gblades/hello

    rm machines.$JOB_ID

( sample file: /home/gblades/wiki/hello.ge ) The directives section
specifies the computing environment and resources that are needed to do
the job. Each directive starts with ``#$``. The must be no space before the
``#$`` but there is a space after.

We specify that we want to execute the commands in the current directory
with the -cwd directive:

.. code-block:: bash

    #$ -cwd

We specify the name of the job with the -N directive:

.. code-block:: bash

    #$ -N hello

We specify a file for the program to write its output to and we merge
the standard output and standard error into one stream:

.. code-block:: bash

    #$ -o hello.output -j y

We are going to run the program in a parallel environment. We will
distribute out program over 32 cores. The parallel environment directive
looks like this:

.. code-block:: bash

    #$ -pe impi 32

We specify the job queue:

.. code-block:: bash

    #$ -l qname=all.q

We specify that the job have the same environemnt variables as the shell
in which the job was submitted:

.. code-block:: bash

    #$ -V

Submit the job:

.. code-block:: bash

    $ qsub hello.ge