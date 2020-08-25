... submit a job on Torngat
===========================

When submitting a job the command qsub is used. The parameters for the
job can be contained in a submisison script file, or can be included on
the qsub command line. For additional docs, please see the
`acenet information`_, or check out the
`official documentation`_. Keep in mind the official docs are for a newer version
than torngat currently supports.

Here are common parameters:

-cwd     This will maintain the Current Working Directory. In other words,
         files without a full path specification will be taken from the
         location the job was started

         Script example:
         ``#$ -cwd``

-N       Gives the job a defined name. If this parameter is not given, the
         job name will be the submission script name.

         Script example:
         ``#$ -N my-job``

-pe      Tells the scheduler which parallel environment to use, see
         documentation on :ref:`pe configuration` for more information.
         In particular, when using impi, additional glue is
         currently required.

         Script example:
         ``#$ -pe impi 1``

         - When using the environment ``impi`` a machine file must be
           generated, please see

-q       This has become important as there are now multiple queues on
         torngat, just as on acenet. The general queue to use is sl6.q. This
         queue only has minimal resources. A better queue would be the group
         queue. This can be determined by using the command “id” and looking
         for your supervisor's group name. Queue names can also be obtained
         by running the command “qstat -g c”, please be sure to only use the
         queue to which you are entitled.

         Script example:
         ``#$ -q sl6.q``

-j y     Joins stdout and stderr. If set to n, the default, then a separate
         file will be used for each output stream.

         Script example:
         ``#$ -j y``

-o       directs output into the named file. A best practice is to use the
         JOB\_ID variable to prevent merging of output from different jobs.

         Script example:
         ``#$ -o $JOB_ID.out``

-V       (Capital V), keeps any customized environment settings.

         Script example:
         ``#$ -V``

-M       Send email about the job to this address

         Script example:
         ``#$ -M cagg-systems@mun.ca``

-m <b|e|a|s|n>
         Choose when to send mail. For example to send mail when the job
         starts and ends

         Script example:
         ``#$ -m be``

.. target-notes::

.. _`acenet information`: http://www.ace-net.ca/wiki/SGE#Job_parameters_acenet_information
.. _`official documentation`: http://docs.oracle.com/cd/E24901_01/doc.62/e21976/toc.htm_official_documentation
.. _Parallel\_Environments: Parallel_Environments
