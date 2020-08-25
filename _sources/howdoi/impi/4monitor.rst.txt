Monitoring Jobs
===============

To show your jobs:
------------------

.. code-block:: bash

    $ qstat

    job-ID  prior   name       user        state submit/start at   slots     
    --------------------------------------------------------------------
       1313 0.50500 hello      gblades     r     04/17/2012 12:24:00  32        

To show all jobs:
-----------------

.. code-block:: bash

    $ qstat  -u  “*”

    job-ID  prior   name       user        state submit/start at   slots     
    --------------------------------------------------------------------
       1616 0.60500 z.cmd      username1   r     04/13/2012 22:03:13 144        
       1522 0.50500 job.sh     username2   r     03/27/2012 10:23:21   1                 

To show all queues:
-------------------

.. code-block:: bash

    $ qstat  -f

    queuename                      qtype used/tot. load_avg states          
    --------------------------------------------------------------------
    all.q@cn01.localdomain         BIP   12/12     12.05        
    --------------------------------------------------------------------
    all.q@cn02.localdomain         BIP   12/12     12.04        
    --------------------------------------------------------------------
    all.q@cn03.localdomain         BIP   12/12     12.06        
    --------------------------------------------------------------------
                                   etc…

To delete (abort) a job:
------------------------

.. code-block:: bash

    $ qdel  1313