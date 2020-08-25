... transfer data to/from ACE-net
---------------------------------
All file transfers must be initiated from placentia.

-  Log into placentia
-  To transfer placentia --> torngat

   -  ``scp <source file(s)> styx.ace-net.ca:<destination directory>``

-  To transfer torngat --> placentia

   -  ``scp styx.ace-net.ca:<source file(s)> <destination directory>``

Tips
~~~~

-  to perform the transfer without a password, append the ace-net
   account public key to torngat's authorized\_keys

   -  open two terminals, one on torngat, one on placentia
   -  on placentia ``cat ~/.ssh/id_rsa.pub``

      -  copy the lines that are output

   -  on torngat, edit ``~/.ssh/authorized_keys``

      -  If the file does NOT exist, it can be created, but must only be
         readable by the owner.
      -  append the copied lines

Notes
~~~~~

-  The file transfers are currently running at about 45MB/s, this is
   approximately 5 times faster than previously. If there is a need for
   increased speed, please contact cagg-systems@mun.ca

