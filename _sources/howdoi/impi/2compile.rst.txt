Use the mpi compiler to compile the MPI program
===============================================
See Sample program
------------------

Compile C program:
""""""""""""""""""

.. code-block:: bash

    $ mpicc hello.c  -o hello

Compile C/C++ program:
""""""""""""""""""""""

.. code-block:: bash

    $ mpic++ hello.cpp  -o hello

Compile Fortran program:
""""""""""""""""""""""""

.. code-block:: bash

    $ mpifc hello.f  -o hello

(also: mpif77, mpif90)

Switches on the command line are passed to the underlying compiler.
*******************************************************************

Example:

.. code-block:: bash

    $ mpicc hello.c -o hello -O2 -lm

.. _Section 6: IMPI/Sample_MPI_program

