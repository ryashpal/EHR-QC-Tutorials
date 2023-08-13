Case Study
**********

Extraction and preparation of Sepsis data for Machine Learning applications.

Outline
=======

1. Introduction
2. Set-up
3. Cohort selection
4. Data standardisation
5. Data preperation
6. Conclusion

1. Introduction
===============

In this case study, our main objective is to showcase the effectiveness of EHR-QC. We achieve this by employing the toolkit to handle EHR data comprehensively, preparing it for utilization in Machine Learning applications. To illustrate, we select a group of patients who have been diagnosed with Sepsis from the public MIMIC IV EHR database. Subsequently, we employ the EHR-QC standardization module to standardise the EHR records for these patients, converting them into the OMOP-CDM schema. Following this, we employ the EHR-QC data pre-processing module. This involves extracting information from the standardized schema, generating exploratory reports, and identifying as well as rectifying any anomalies present in the data.


2. Set-up
=========

We will be using the Dockerised EHR-QC for this case study by following the below steps;

Change directory
----------------

From the home directory which will be open by default, change to a suitable directory on your computer where the utility needs to be installed. For example, in this tutorial we have changed to ``workspace`` directory.

.. code-block:: console

   user@hostname:~$ cd workspace


Clone
-----

In the destination folder, clone the current version of EHR-QC repository from the GitHub.

.. code-block:: console

   user@hostname:~/workspace$ git clone https://github.com/ryashpal/EHRQC.git


Open EHR-QC
-----------

Open the EHR-QC directory that is downloaded from GitHub after cloning.

.. code-block:: console

   user@hostname:~/workspace$ cd EHRQC

Verify
------

Verify the installation by running the following command. The expected output should contain ``EHRQC <version number>``.

.. code-block:: console

   (.venv) user@hostname:~/workspace/EHRQC$ python -m EHRQC -v
   EHRQC 1.0

Install Docker
--------------

Before starting, we need to ensure the Docker engine is intalled.
`Follow the installation instructions: <https://docs.docker.com/engine/install/>`_


Build the contaner
------------------

The containers are to be built first when using for the first time.

.. code-block:: console

   app_user@hostname:~$sh snippets/shell/build.sh

Start the contaner
------------------

This script can be used to start the container if the image is already built.

.. code-block:: console

   app_user@hostname:~$sh snippets/shell/start.sh

Update the contaner
------------------

To update the container by taking latest code from Git.

.. code-block:: console

   app_user@hostname:~$sh snippets/shell/update.sh

3. Cohort selection
===================

4. Data standardisation
=======================

5. Data preperation
===================

6. Conclusion
=============
