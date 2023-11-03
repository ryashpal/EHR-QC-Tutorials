EHR-QC-Preprocess
=================

Follow the below steps to install EHR-QC-Preprocess in your computer.


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

   user@hostname:~/workspace$ git clone https://gitlab.com/superbugai/ehrqc.git


Open EHR-QC
-----------

Open the EHR-QC directory that is downloaded from GitHub after cloning.

.. code-block:: console

   user@hostname:~/workspace$ cd EHRQC


You have the option to set up EHR-QC either within a Python virtual environment or a Docker container. Please select one of these methods and follow the corresponding instructions for the initial setup. 

* For setting up EHR-QC using Python virtual environment, please use this `Link <https://ehr-qc-tutorials.readthedocs.io/en/latest/install.html#python-virtual-environment>`_
* For setting up EHR-QC using Docker container, please use this `Link <https://ehr-qc-tutorials.readthedocs.io/en/latest/install.html#docker>`_

.. note::
   All the subsequent instructions in this document apply uniformly to both setups.

Python virtual environment
--------------------------

The Python virtual environment encaptulates all the libraries required for the EHR-QC. All the necessary libraries listed in a requirements.txt file that can be found at the root of the repository. Below are the instructions to create and install dependancies in the Python virtual environment.

.. note::
   EHR-QC requires Python version 3.9 or higher. For installing Python, please refer the below link: https://www.python.org/downloads/


Create virtual environment
~~~~~~~~~~~~~~~~~~~~~~~~~~

Inside the EHR-QC directory, create a new Python virtual enviroment to conveniently manage all the dependencies required for the utility.

.. code-block:: console

   user@hostname:~/workspace/EHRQC$ python3 -m venv .venv


Activate virtual environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After creating the Python virtual enviroment, activate the virtual enviroment to start using it for subsequent commands. The prompt will change with ``(.venv)`` appearing in front of it as shown below;

.. code-block:: console

   user@hostname:~/workspace/EHRQC$ source .venv/bin/activate
   (.venv) user@hostname:~/workspace/EHRQC$


Install dependencies
~~~~~~~~~~~~~~~~~~~~

Install all the required dependencies listed in the requirements.txt file in the newly created Python virtual environment.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ pip install -r requirements.txt


Verify
~~~~~~

Verify the installation by running the following command. The expected output should contain ``EHRQC <version number>``.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ python -m EHRQC -v
   EHRQC 1.0

