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

In this case study, we utilizeed the Dockerized EHR-QC. For comprehensive instructions on configuring the Docker environment, please consult the documentation provided at the following link: https://ehr-qc-tutorials.readthedocs.io/en/latest/install.html#docker

3. Cohort selection
===================

All the patients and admissions with Sepsis are identified from the MIMIC IV dataset. For that, ICD codes 9 codes 995.91, 995.92 and 785.52, and ICD 10 codes A419, R6520 and R6521 corresponding to Sepsis, Severe Sepsis, and Septic Shock are used to select patients. The entire EHR data corresponding to these patients and admissions are extracted to flat files.

This resulted in 12277 patients corresponding to 14871 admissions and their EHR data.

4. Data standardisation
=======================

The Sepsis cohort selected in the previous step is standardised to OMOP-CDM specification;

Configuration
-------------

The below configuration is done to direct EHR-QC to fetch data from database where MIMIC dataset is hosted. In addition to the source details, the configuration file also specifies the location to store intermediate tables and the final OMOP-CDM tables;

.. code-block:: console
   # database connection details
   db_details = {
       "sql_host_name": 'localhost',
       "sql_port_number": 5434,
       "sql_user_name": 'postgres',
       "sql_password": '***************',
       "sql_db_name": 'mimic4',
   }

   # new schema to host the migrated tables

   lookup_schema_name = 'vocabulary_test_20230809'

   source_schema_name = 'omop_migration_source_20230809'

   etl_schema_name = 'omop_migration_etl_20230809'

   cdm_schema_name = 'omop_test_20230809'

Lookup
------

The Athena vocabulary and custom mapping are imported to create lookup.

.. code-block:: console
.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -l

Import
------

EHR data is imported from the csv files

.. code-block:: console
.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -f

Stage
------

Imported EHR data is staged on the ETL schema

.. code-block:: console
.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -s

Mapping
------

Imported custom mapping file containing mapping information of the concepts in the EHR to standard vocabulary.

.. code-block:: console
.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -c

Mapping
------

Imported custom mapping file containing mapping information of the concepts in the EHR to standard vocabulary.

.. code-block:: console
.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -c

5. Data preperation
===================

6. Conclusion
=============
