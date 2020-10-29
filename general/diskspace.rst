.. index::
   single: Diskspace
   :name: diskspace

=========
Diskspace
=========

We monitor the diskspace and inform you as soon you are using more diskspace than you have chosen in the cockpit.

You are most likely reading this page because you have received a diskspace notification.
Here you can find information about what this means.

Tools
=====

You can run these tools by login with the devop user (see :ref:`access_devop`).

* ``diskusage``: Starts `ncdu <https://en.wikipedia.org/wiki/Ncdu>`__, a disk space utility with which you can find large files or directories.
* ``df -h /``: Look at the "Used" column. This value must be below the value set in the cockpit.

FAQ
===

Which data belong to my diskspace?
----------------------------------

All data stored on the disk.

* This includes all data you see with ``diskusage``. This contains your web project, your databases, your docker containers, the underlying Linux and all other data stored on the same disk.
* The daily file system snapshots are also counted among your diskspace. These are stored in ``/snapshot``, but are not displayed in ``diskusage``.

How much storage space do the daily snapshots use?
--------------------------------------------------

For the daily file system snapshot (see :ref:`backup`) only the changed data occupies storage.
Depending on the use of the server, the consumption therefore varies.

Assuming you change 1GB of data every day, the snapshots then need 1GB every day (1GB x 30 days = 30GB in a month).

Unfortunately it is not possible to show how much disk space all snapshots need in total,
which is due to the way copy on write and Btrfs works.
However, you can calculate the actual consumption by subtracting the total of ``df -h /`` from ``diskusage``.

I have deleted many files. But the diskspace has not changed.
-------------------------------------------------------------

All files you delete are still referenced in the snapshots and therefore still occupy disk space.
By default, snapshots are kept for 30 days. So the diskusage of deleted files are taken in account in 30 days.

Can I delete snapshots?
-----------------------

No. In most cases it would not help much either.

The cleaned up or deleted files are in most cases older than 30 days and therefore referenced in all snapshots.
So we would have to delete all snapshots, which also affects the backup (see :ref:`backup`).
We recommend adjusting the diskspace in the cockpit and checking it again in 30 days.