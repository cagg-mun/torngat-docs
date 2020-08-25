Power Cycle Torngat
===================

Shutdown
--------

#. Login to glauce (as yourself) and sudo to root
#. Setup the ansible environment, the easiest way might be to go through
   the history (up-arrow) to find the commands

       ``cd ~/ansible; . hacking/env-setup; export``
       ``ANSIBLE_HOSTS=~/clusterhosts; export``
       ``ANSIBLE_HOST_KEY_CHECKING=False``

#. Shutdown the compute nodes.

   #. To power the machines off elegantly run:

          ``ansible 'cn' -a poweroff``
          This command will run in parallel so the command will return
          quickly.

   #. **Wait 5 minutes for the systems actually power off**
   #. Run the command:

          ``ansible 'ilo' -m raw -a power``
          ``|grep -E '(localdomain|server power|On)'``
          The command will simply show the power status for the nodes
          using the management interface. The last word of the status
          line should be “Off”. With any luck, any systems that are on,
          will have the word “On” in green . Check for any nodes that
          show power “On”, skip down below for instructions on powering
          them off.

#. Power off the head nodes.

   #. First power off the secondary head node, which is actually called
      torngat. To do that use the command:

          ``ansible 'hn02*;' -m raw -a poweroff``

   #. ***Wait 5 minutes for the system to power off***
   #. Run the command:

          ``ansible 'mphn02*;' -m raw -a power``
          The command should return that the server power is off. If not
          wait another 5 minutes and check again. If the system is still
          not off, use the instructions for forcing power off on a
          compute node.

   #. Now power off the primary head node, avalon. Use the command:

          ``ansible 'hn01*;' -m raw -a poweroff``

   #. ***Wait 5 minutes for the system to power off***
   #. Run the command:

          ``ansible 'mphn01*;' -m raw -a power``
          The command should return that the server power is off. If not
          wait another 5 minutes and check again. If the system is still
          not off, use the instructions for forcing power off on a
          compute node.

#. Lastly glauce can be powered off (the system used from steps 1-4),
   just run the command “poweroff”
#. Power off the UPS, press the power switch on the front.
#. Turn off the 8 PDU master switches. This action will shutdown the
   network devices, compute node chassis and storage chassis.
   
#. Finished

Startup
-------

The startup is essentially the reverse of shutdown, with more physical
presense needed.

#. Power on the PDU devices (8 of them). The network, storage chassis
   and compute node chassis will power up.
#. Power on the UPS.
#. **Wait for 10 minutes for the switches and chassis to settle.**
#. Power on glauce (don't need to wait, continue on)
#. Power on avalon, the storage management and primary head node.
#. **WAIT for the console in the datacentre to show the system login screen.**
#. Power on torngat, there is no console for this, so ...
#. **Wait 5 minutes**
#. Log into glauce (it should be up by now) as yourself and sudo to
   root.
#. Setup the ansible environment as per step 2 of shutdown.
#. Power on the compute nodes by running the command:

       ``ansible 'ilo' -m raw -a 'power on'``

#. **Wait 10 minutes for the systems to settle**
#. Now validate that the systems are accessible by running:

       ``ansible 'cn' -m ping``
       This runs in parallel so the results may be out of order. Check
       that each of the 42 nodes responds with a success and a pong. The
       node name should show success, and the ping should have a
       corresponding pong. For nodes that are not up, each one must be
       dealt with individually, see troubleshooting

#. Craig Squires will check that the queuing is functioning correctly
#. 

   .. raw:: mediawiki

      {{hl | Restart MATLAB license server}}

#. 

   .. raw:: mediawiki

      {{hl | Restart CMG license server}}

Finished

For systems that auto power up

If a system starts up automatically, there are 2 choices.

#. Shut the system down before beginning startup procedures. The shut
   down can be done with a long press of the power button, or the remote
   management, as per shutdown steps (glauce would need to be on)
#. Proceed with the startup, and reset/reboot the node after all power
   is up (dealing with troublesome nodes)

Troublesome nodes
-----------------

Forcefully powering down a node
"""""""""""""""""""""""""""""""

If for some reason the operating system has hung, the nodes can still be
forcefully powered off. There are 2 ways to achieve this, with a
physical power switch, or using remote management.

Remote Management
'''''''''''''''''

This can be done with ansible or direct ssh.

-  Using ansible the command is

       ``ansible`` ``'mpcn<node`` ``num>*;'`` ``-m`` ``raw`` ``-a``
       ``'power`` ``off`` ``hard'``
       For example: ``ansible`` ``'mpcn42*;'`` ``-m`` ``raw`` ``-a``
       ``'power`` ``off`` ``hard'``

-  Using ssh, simply ssh to the node and run 'power off hard'. For
   example: ``ssh`` ``admin@mpcn42`` ``power`` ``off`` ``hard``

Physically
''''''''''

Locate the node that still has power by the light in front, and press
and hold the power button until the power is off.

Restoring nodes that do not return to normal operating status
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Most of these operations will be done from a terminal on glauce, and the
ansible setup from [onenote:Cluster.one Shutdown Plan] should have been
run before beginning this.

#. Check that the node is powered on:

       ``ansible 'mpcn<##>;' -m raw -a power``

#. Check the node console for error messages:

       ``ssh admin@mpcn<##>``

   #. Run the command “vsp” which will show a serial console
   #. If there is no login prompt

      #. Use the exit from the serial console, it should be on the
         screen ( ESC+( )
      #. Command: ``power off hard``
      #. Wait for the node power to go off, 2-5 minutes.
      #. Command: ``power on``
      #. Immediately type ``vsp`` and wait for the BIOS and boot messages
         to start scrolling by. This can take a while so be patient.

   #. Else there is a login prompt so:

      #. Login to the node as root
      #. Use the ``reboot`` command

#. If the error condition can not be resolved, then notify the users
   group that a node is out, I'll repair it when I get back.
