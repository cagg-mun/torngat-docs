... pick a parallel environment
===============================
Torngat has a number of Parallel Environments, the correct one will be
determined by the job requirements. To understand the parallel
environments, here is a definition of the configuration options, as well
as the PEs available on torngat

.. _pe configuration:

PE Configuration
----------------

pe\_name
    A label for the environment, must be defined in GE to be used

slots
    Total number of CPU slots available to the environment. On torngat
    each node has 12 slots, which essentially are the number of cores
    available on each node. Torngat has a maximum of 504 slots

user\_lists & xuser\_lists
    Permissions for the PE, not currently used on torngat

start\_proc\_args
    A list of commands to run before starting a job with the defined PE.
    This is commonly /bin/true or NONE, both of which do nothing for the
    job. There are some special variables which can be used.

stop\_proc\_args
    As with the start arguments, this command/script will run after the
    job has stopped.

allocation\_rule
    Currently the most important setting available, this controls the
    mechanism used to allocate (CPU)-slots are allocated to the job.

    :integer value:
        For an integer value, the number of slots/host is defined and
        must be exactly the number.
    :$fill\_up:
        allocates slots on a host until no more slots remain on the
        host, then “fills up” another host
    :$round\_robin:
        allocates slots a host at a time, each slot is allocated on a
        new host until all hosts are used, then slots are allocated
        again on hosts with available slots

control\_slaves
    This defines whether the processes controlled by the grid engine
    process. Generally this is FALSE

job\_is\_first\_task
    Only used if control\_slaves is TRUE

urgency\_slots
    Used when a range of slots is specified

This information has been compiled from the Grid Engine manual, more
details can be found at the man page sge\_pe(5)

Torngat PEs
-----------

12per
    This environment is configured to use all 12 processor cores on a
    node. If there is no node on which all 12 cores are available, the
    job will be queued. The number of requested slots for this
    environment must be a multiple of 12. For example, if 48 slots are
    requested, 4 nodes must be unoccupied for the job to begin
    execution, and the 4 nodes are completely allocated to the running
    job.

1per
    Each host can only have one slot allocated to the requesting job.
    The maximum number of slots available equals the number of hosts
    with available slots

impi
    Probably the best general use PE, allocates all slots on a node
    until the node is full (see $fill\_up above)

    Currently when using impi, an execution host file must be built, to
    build the file insert the following into the job submission script

    .. code-block:: bash

       # make host file
       MakeMachineFile()
       {
           cat $1 | while read line; do
              host=`echo $line|cut -f1 -d" "|cut -f1 -d"."`
              nprocs=`echo $line|cut -f2 -d" "`
              echo "$host:$nprocs"
           done
       }
       MakeMachineFile $PE_HOSTFILE >machines.$JOB_ID

ompi
    A copy of impi

make
    Does $round\_robin slot allocation