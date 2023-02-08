Installation
============

Follow the below steps to install EHR-QC in your computer.


Login
------

Upon login to a system and opening a terminal, the following prompt should appear, where the ``user`` is the user name and the ``hostname`` is the hostname of the system.

.. code-block:: console

   user@hostname:~$


Change directory
----------------

From the home directory which will be open by default, change to a suitable directory on your computer where the utility needs to be installed. For example, in this tutorial we have changed to ``workspace`` directory.

.. code-block:: console

   user@hostname:~$ cd workspace


Clone
-----

In the destination folder, clone the current version of EHR-QC repository from the GitHub.

.. code-block:: console

   user@hostname:~/workspace$ git clone git@github.com:ryashpal/EHRQC.git


Open EHR-QC
-----------

Open the EHR-QC directory that is downloaded from GitHub after cloning.

.. code-block:: console

   user@hostname:~/workspace$ cd EHRQC


Create virtual environment
--------------------------

Inside the EHR-QC directory, create a new Python virtual enviroment to conveniently manage all the dependencies required for the utility.

.. code-block:: console

   user@hostname:~/workspace/EHRQC$ python -m venv .venv


Activate virtual environment
----------------------------

After creating the Python virtual enviroment, activate the virtual enviroment to start using it for subsequent commands. The prompt will change with ``(.venv)`` appearing in front of it as shown below;

.. code-block:: console

   user@hostname:~/workspace/EHRQC$ source .venv/bin/activate
   (.venv) user@hostname:~/workspace/EHRQC$


Install dependencies
--------------------

Install all the required dependencies listed in the requirements.txt file in the newly created Python virtual environment.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ pip install -r requirements.txt


Verify
------

Verify the installation by running the following command. The expected output should contain ``EHRQC <version number>``.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ python -m EHRQC -v
   EHRQC 1.0
