Select MPI version
==================

Use the mpi selector facility to set the MPI version to Intel MPI.
------------------------------------------------------------------

.. code-block:: bash

    $ mpi-selector-menu

    Current system default: impi_4.0.1.007
    Current user default:   impi_4.0.1.007

    If the current user default is not impi, change it to impi:

    1. impi_4.0.1.007
    2. mvapich_gcc-1.2.0
    3. openmpi_gcc-1.4.3
    U. Unset default
    Q. Quit

    Selection (1-3[us], U[us], Q): 1
    Operator on the per-user or system-wide default (u/s)? u
    Defaults already exist; overwrite them? (y/N) y

    Current system default: impi_4.0.1.007
    Current user default:   impi_4.0.1.007

    Selection (1-3[us], U[us], Q): Q

    WARNING: Changes made to mpi-selector defaults will not be visible until you start a new shell!

    $

Log out and log back in.