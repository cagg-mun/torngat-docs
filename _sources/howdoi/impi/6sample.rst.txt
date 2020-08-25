Sample Programs
---------------

MPI Hello World program in C language:

.. code-block:: c
   :linenos:

    #include <mpi.h>

    int main(int argc, char ** argv)
    {
      int rank, size, len;
      char host[MPI_MAX_PROCESSOR_NAME];

      MPI_Init(&argc, &argv);

      MPI_Comm_rank(MPI_COMM_WORLD, &rank);
      MPI_Comm_size(MPI_COMM_WORLD, &size);
      MPI_Get_processor_name(host, &len);

      printf("Process %3d of %d says Hello from host %s\n",
              rank, size, host);

      MPI_Finalize();
    }

( sample file: /home/gblades/wiki/hello.c )

MPI Hello World program in C++:

.. code-block:: cpp
   :linenos:

    #include <mpi.h>
    #include <iostream>

    using namespace std;

    int main(int argc, char ** argv)
    {
      int rank, size, len;
      char host[MPI_MAX_PROCESSOR_NAME];

      MPI_Init(&argc, &argv);

      MPI_Comm_rank(MPI_COMM_WORLD, &rank);
      MPI_Comm_size(MPI_COMM_WORLD, &size);
      MPI_Get_processor_name(host, &len);

      cout << "Process " << rank << " of " << size
           << " says Hello from host " << host << endl;

      MPI_Finalize();
    }

( sample file: /home/gblades/wiki/hello.cpp )

MPI Hello World program in Fortran:

.. code-block:: fortran
   :linenos:

          program hello

          include 'mpif.h'

          integer rank, size, len, ierror
          character*(MPI_MAX_PROCESSOR_NAME) host

          call MPI_INIT(ierror)

          call MPI_COMM_SIZE(MPI_COMM_WORLD, size, ierror)
          call MPI_COMM_RANK(MPI_COMM_WORLD, rank, ierror)
          call MPI_Get_processor_name(host, len);

          print*, 'Process ', rank, 'of ', size, 'says Hello from ', host

          call MPI_FINALIZE(ierror)

          end

( sample file: /home/gblades/wiki/hello.f )
