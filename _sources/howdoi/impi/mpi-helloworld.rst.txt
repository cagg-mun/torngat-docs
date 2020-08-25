MPI Communications
------------------
.. code-block:: c
   :linenos:

    #include <stdio.h>
    #include <mpi.h>

    int main(int argc, char ** argv)
    {
      MPI_Init(&argc, &argv);

      int rank, size;

      MPI_Comm_rank(MPI_COMM_WORLD, &rank);
      MPI_Comm_size(MPI_COMM_WORLD, &size);

      int buffer=0, count, dest, source, tag;

      if (rank == 0) // master process
      {
        // write first message
        printf("Hello from task %3d of %3d\n", rank, size);
        // write remaining messages in sequence
        int i;
        for (i=1; i<size; i++) // for each slave process
        {
          MPI_Status status;
          // tell slave process to write message
          MPI_Send(&buffer, count=1, MPI_INT, dest=i, tag=331, MPI_COMM_WORLD);
          // wait for slave process to write message
          MPI_Recv(&buffer, count=1, MPI_INT, source=i, tag=333, MPI_COMM_WORLD,
                   &status);
        }
      }
      else // slave process
      {
        MPI_Status status;
        // wait for signal from master process to write message
        MPI_Recv(&buffer, count=1, MPI_INT, source=0, tag=331, MPI_COMM_WORLD,
                 &status);
        // write message
        printf("Hello from task %3d of %3d\n", rank, size);
        // tell master process that message is written
        MPI_Send(&buffer, count=1, MPI_INT, dest=0, tag=333, MPI_COMM_WORLD);
      }

      MPI_Barrier(MPI_COMM_WORLD); // wait until everyone is finished

      MPI_Finalize(); // bye bye
    }

A clear line before regular text