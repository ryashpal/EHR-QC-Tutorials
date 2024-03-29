EHR-QC
======

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


Docker
------

The EHR-QC is also available in Docker. Follow the instructions below to use EHR-QC as a Docker container.

Before starting, ensure the Docker engine is intalled.
`Follow the installation instructions: <https://docs.docker.com/engine/install/>`_

.. note::
   Please clone the repository as explained above and change to root EHR-QC directory before creating the docker container;

Build the container
~~~~~~~~~~~~~~~~~~~

Firstly, build the Dockerfile.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ docker-compose up -d

Output

.. code-block:: console

   [+] Running 1/1
    ! app Warning                                                                                                                                                    [+] Building 194.3s (16/16) FINISHED                                                                                                                               => [internal] load build definition from Dockerfile                                                                                                               => => transferring dockerfile: 32B                                                                                                                                 => [internal] load .dockerignore                                                                                                                                   => => transferring context: 34B                                                                                                                                   => [internal] load metadata for docker.io/library/python:3.9-slim                                                                                                 => [ 1/11] FROM docker.io/library/python:3.9-slim@sha256:a321a8513911c55888b9c1cc981a5ba646271447a82ece1b62e4a6a8ff1d431b                                         => [internal] load build context                                                                                                                                   => => transferring context: 348.07kB                                                                                                                               => CACHED [ 2/11] RUN useradd --create-home --shell /bin/bash app_user                                                                                             => CACHED [ 3/11] WORKDIR /home/app_user                                                                                                                           => CACHED [ 4/11] RUN apt-get update && apt-get install                                                                                                           => CACHED [ 5/11] COPY requirements.txt ./                                                                                                                         => CACHED [ 6/11] RUN pip install --no-cache-dir -r requirements.txt                                                                                               => CACHED [ 7/11] RUN mkdir /home/app_user/data                                                                                                                   => CACHED [ 8/11] RUN chown -R app_user.app_user /home/app_user/data                                                                                               => [ 9/11] COPY . .                                                                                                                                               => [10/11] RUN python -m venv .venv                                                                                                                               => [11/11] RUN .venv/bin/pip install --no-cache-dir -r requirements.txt                                                                                           => exporting to image                                                                                                                                             => => exporting layers                                                                                                                                             => => writing image sha256:790deade8232b27a423c61b06e1e43949b17810dac828777ca8aeaa4f5884bc4                                                                       => => naming to docker.io/library/ehr-qc                                                                                                            

Create the container
~~~~~~~~~~~~~~~~~~~~

Create the docker container. It is recommended to run the container in detached mode as it enables the container to be connected from multiple terminals.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ docker-compose up -d

Output

.. code-block:: console

   [+] Running 1/1
    ✔ Container ehrqc-app-1  Started


Start the container
~~~~~~~~~~~~~~~~~~~~

Connect to the container to use the EHR-QC functions.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ docker exec -it <Container ID> bash


The following prompt should appear, where ``hostname`` is the hostname of the system.

.. code-block:: console

   app_user@hostname:~$

Activate the python virtual environment which will change the prompt with (.venv) appearing in front of it as shown below;

.. code-block:: console

   app_user@hostname:~$ source .venv/bin/activate
   (.venv) app_user@hostname:~$

From here, the EHR-QC commands can be run as usual.

.. note::
   All the data that is saved in ``/home/app_user/data`` directory will be synced to ``~/workspace/EHRQC/data`` directory on the host machine.

.. note::
   The network conntections from the container is configured to be in ``host`` mode. This makes the container have the same network setup as the host system without a IP address of its own.

Verify
~~~~~~

Verify the installation by running the following command. The expected output should contain ``EHRQC <version number>``.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ python -m EHRQC -v
   EHRQC 1.0


Scripts
~~~~~~~

Build
^^^^^

Instead of running the commands manually, the containers can be handled by running the following scirpts.

To start the container by building the image:

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$sh snippets/shell/build.sh

This command will build the Docker image, create a container from the image, present the command prompt of the running container to the user (as shown below) by activating the python virtual environment.

.. code-block:: console

   (.venv) app_user@hostname:~$

Start
^^^^^

To start the container if the image is already built:

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$sh snippets/shell/start.sh

This command will start the pre-built Docker container, present the command prompt of the running container to the user (as shown below) by activating the python virtual environment.

.. code-block:: console

   (.venv) app_user@hostname:~$

Update
^^^^^^

To update the container by taking latest code from Git:

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$sh snippets/shell/update.sh

This command will update the EHR-QC source code by taking it from the Git repository, build the Docker image for the updated code, create a container from the image, present the command prompt of the running container to the user (as shown below) by activating the python virtual environment.

.. code-block:: console

   (.venv) app_user@hostname:~$

Custom volume mapping
~~~~~~~~~~~~~~~~~~~~~

If the mapped directory which will default to ``./data`` need to be changed to some other volume;

Open the ``docker-compose.yml`` at the EHR-QC base path, and make the changes shown below;

.. code-block:: console

   version: "3.8"
   services:
     app:
       build: .
       image: ehr-qc
       network_mode: "host"
       volumes:
         - ``custom/volume/path``:/home/app_user/data
       stdin_open: true
       tty: true

Then start the container by building the image:

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$sh snippets/shell/build.sh
