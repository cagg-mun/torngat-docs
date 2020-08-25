Paul S - Notes
**************
.. rst-class:: table-striped

+------------------+-------+-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Updated          | State | Task                                | Notes                                                                                                                                                                                                                                                                                                                                         |
+==================+=======+=====================================+===============================================================================================================================================================================================================================================================================================================================================+
| 2012-05-24 09:39 | 0%    | Migrate data from scratch partition | -  Torngat Scratch partition is on fast disk, once data is analyzed,                                                                                                                                                                                                                                                                          |
|                  |       | to archive partitions               |    can be moved to the slower disks, the archive partitions.                                                                                                                                                                                                                                                                                  |
|                  |       |                                     |                                                                                                                                                                                                                                                                                                                                               |
+------------------+-------+-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 2012-05-24 09:39 | 0%    | SGE upgrade                         | -  version not lagging by much, but may fix bugs                                                                                                                                                                                                                                                                                              |
+------------------+-------+-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 2013-07-3 16:14  | 0%    | MATLAB upgrade                      | -  Will certainly see benefit when GPUs are installed. The MATLAB currently licensed has components that will use GPU if installed and configured                                                                                                                                                                                             |
+------------------+-------+-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 2013-07-3 16:18  | 0%    | Reporting/usage                     | -  Presentation given about this at ISC13. Systems are so unique that homegrown reporting is common. The most commonly used system for reporting is rrdtool. Has some disadvantages related to timing of input data. An up and coming tool “graphite” was suggested. Will allow the data, once in the system, to be queried and live graphed. |
|                  |       |                                     | -  Setup a VM on glauce for this.                                                                                                                                                                                                                                                                                                             |
+------------------+-------+-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  `Reference to the fixed CSS for syntax highlights`_
-  `MPI Communicatoins`_

.. _ Reference to the fixed CSS for syntax highlights: MediaWiki:Geshi.css
.. _MPI Communicatoins: MPI_Communicatoins

.. todo::

   .. csv-table::
      :header-rows: 1

      "Created", "State", "Task", "Notes"
      today, 50%, "Do this first", "
      - and this is a subtask
      - with a list
      - hopefully"

.. todo::

   Do this second

.. todo::

   :Date: 2001-08-16
   :Version: 1
   :Authors: - Me
             - Myself
             - I
   :Indentation: Since the field marker may be quite long, the second
      and subsequent lines of the field body do not have to line up
      with the first line, but they must be indented relative to the
      field name marker, and they must line up with each other.
   :Parameter i: integer

.. todolist::


.. list-table:: Current State
   :class: table table-striped

   *  - Row 1 col 1
      - Row 1 col 2
      - Row 1 col 3
      - row 1 col 4
   *  - next row
      - still next row, but with a much longer cell to see what the wrapping will do, if anything.
      -
      -
