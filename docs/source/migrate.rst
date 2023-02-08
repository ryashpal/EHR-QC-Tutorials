OMOP-CDM migration
==================


Help menu
---------

To display the help menu of the OMOP-CDM migration utility.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -h

or

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run --help

Output

.. code-block:: console

    usage: Run.py [-h] [-l] [-f] [-s] [-m] [-c] [-e] [-u]

    Migrate EHR to OMOP-CDM

    optional arguments:
    -h, --help            show this help message and exit
    -l, --create_lookup   Create lookup by importing Athena vocabulary and custom mapping
    -f, --import_file     Import EHR from a csv files
    -s, --stage           Stage the data on the ETL schema
    -m, --generate_mapping
                            Generate custom mapping of concepts from the data
    -c, --import_custom_mapping
                            Import custom mapping file
    -e, --perform_etl     Perform migration Extract-Transform-Load (ETL) operations
    -u, --unload          Unload data to CDM schema


Import Vocabulary
-----------------

To import standard vocabulary files from the path specified in the configuration files under `vocabulary` attribute in to the lookup schema specified by `lookup_schema_name`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -l


Import EHR
----------

To import EHR data from csv files from the path specified in the configuration files under every entity in to the source schema specified by `source_schema_name`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -f


Stage data
----------

To stage the data from source schema into the etl schema specified by `etl_schema_name` attrbibute in the configuration file.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -s


Generate custom mappings
------------------------

To automatically generate mappings for the specified vocabularies in the configuration file under `customMapping` attribute and update the vocabulary in the database with mapped automatically concepts.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -m


Import custom mapping
---------------------

To import manually generated custom mappings from the csv file specified under `vocabulary.tmp_custom_mapping` attribute in the configuration file and update the vocabulary in the database with manually mapped concepts.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -c


Perform migration
-----------------

To perform the Extract-Transform-Load (ETL) operations necessary to format the source data as per the OMOP-CDM schema and stores the final tables in etl schema.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -e


Unload data
-----------

To unload the final tables from the lookup and etl shema to the destination schema called cdm schema.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -u


Migrate Pipeline
----------------

To run the entire pipeline in an end-to-end fashion.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.Run -l -f -s -m -c -e -u
