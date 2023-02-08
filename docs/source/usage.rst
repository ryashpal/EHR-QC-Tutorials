Installation
============

Follow the below steps to install EHR-QC in your computer.


Login to a system and open a terminal
---------------------------------------------

Upon login, the following prompt should appear, where the ``user`` is the user name and the ``hostname`` is the hostname of the system.

.. code-block:: console
   user@hostname:~$


Change directory to a suitable location
---------------------------------------

From the home directory, change to a suitable directory on your computer where the utility needs to be installed. For example, in this tutorial we have changed to ``workspace`` directory.

.. code-block:: console

   user@hostname:~$ cd workspace


Clone the repository from GitHub.
---------------------------------

In the destination folder, clone the current version of EHR-QC repository from the GitHub.

.. code-block:: console

   user@hostname:~/workspace$ git clone git@github.com:ryashpal/EHRQC.git


Open EHR-QC directory
---------------------

Open the EHR-QC directory.

.. code-block:: console

   user@hostname:~/workspace$ cd EHRQC


Create a python virtual environment
-----------------------------------

Inside the EHR-QC directory, create a new virtual enviroment to install all the dependencies required for the utility.

.. code-block:: console

   user@hostname:~/workspace/EHRQC$ python -m venv .venv


Activate the python virtual environment
---------------------------------------

After creating the virtual enviroment, activate the virtual enviroment to start using it for subsequent commands. The prompt will change with ``(.venv)`` appearing in front of it as shown below;

.. code-block:: console

   user@hostname:~/workspace/EHRQC$ source .venv/bin/activate
   (.venv) user@hostname:~/workspace/EHRQC$


Install the required dependencies
---------------------------------

Install all the required dependencies listed in the requirements.txt file in the newly created python virtual environment.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ pip install -r requirements.txt


Verify the installation
-----------------------

Verify the installation by running the following command. The expected output should contain ``EHRQC <version number>``.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ python -m EHRQC -v
   EHRQC 1.0
