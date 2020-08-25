... run MATLAB
==============

Accessing a MATLAB node
-----------------------

Prerequisites
"""""""""""""

You must be running an X11 server on your system. If you are
accessing from a Unix/Linux system that
has a GUI then this should function. From an MS Windows system, it is
necessary to install an X11 server. Possibly the easiest to setup is
`XMing`_, and the most
up-to-date is the X11 server included with the `Cygwin`_ package.

Access instructions
"""""""""""""""""""

#. ``ssh`` to torngat. Be sure to use the ``-X`` option if you want to
   run the MATLAB desktop, or do any plotting.
#. from the head node on torngat, run the command: ``qrsh -q -pe 12per 12 'matlab'``

   -  for example ``qrsh -q rhaynes.q -pe 12per 12 'matlab'``

#. At this point Grid Engine will allocate a full single node and start
   MATLAB in interactive mode on your screen.

Parallel computing in MATLAB
----------------------------

The parallel computing toolbox is installed on torngat. For help
documentation, simply type ``doc distcomp`` on the MATLAB command
line.

.. target-notes::

.. _XMing: http://www.straightrunning.com/XmingNotes/
.. _`Cygwin`: http://x.cygwin.com/