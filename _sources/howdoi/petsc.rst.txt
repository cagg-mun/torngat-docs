... compile PETSc on Torngat
============================
${date}

Setting up an environment
---------------------------

First check the official `PETSc`_ site for documentation


#. The first step is to switch from the Intel MPI default, to the MPICH
   implementation.  This is done by removing the path for the Intel MPI compiler
   and libraries and adding the MPICH compiler

.. code-block:: bash

   $ echo $PATH

#. And now add in the correct path
#. Then correctly set the PETSC environment

.. code-block:: bash

   $ export PETSC_DIR=/opt/petsc
   $ export PETSC_ARCH=arch-linux2-c-optimized


PETSc will start and use MPI, no need to call it

See if Alison needs compiles, or other users
Conda & Alison's stuff - pysit - uses PETSc - needs complex compiled in

Sparse direct solvers -- use --download to pull them.
Matrix partitioners medas and parmedas

--with-cuda --with-cuda-arch=

ViennaCL

.. target-notes::

.. _PETSc: http://www.mcs.anl.gov/petsc/