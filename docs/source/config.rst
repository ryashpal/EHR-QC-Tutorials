Configuration
=============

The pipeline might need some of the configurations below, depending on the functionality being used.


Standardisation
--------------

The following configurations mighe be required for migration to OMOP-CDM.


Migration schema names
~~~~~~~~~~~~~~~~~~~~~~

These configuration hold the names of the schema to be created to host the migrated tables. There are four such possible configurations.

1. lookup_schema_name
2. source_schema_name
3. etl_schema_name
4. cdm_schema_name

**Note: All four schema names can be separate if the data needs to be seggregated in different schemas to avoid mixing them up. Optionally they can also be the same in which case all the data will be stored in a single database schema. With this flexibility, it is also possible to group some types of data into a single schema while keeping the others separate. For examples, it is possible to store all the intermediate data in a single schema by providing the same name for ``lookup_schema_name``, ``source_schema_name``, and ``etl_schema_name`` but a different name for ``cdm_schema_name`` to keep the migrated EHR data in a separate schema**

The ``lookup_schema_name`` is required when importing standard vocabularies either in a standalone manner or as part of the pipeline. The utility will create a new schema with the name provided in the configuration file to host the imported vocabularies.

Example:

.. code-block:: json

    lookup_schema_name: 'lookup_test'

The ``source_schema_name`` is required when importing EHR files either in a standalone manner or as part of the pipeline. The utility will create a new schema with the name provided in the configuration file to host the imported EHR data.

**Note: If the EHR is already present in the database instead of a flat file, the database schema name where the EHR is hosted can be provided here along with the appropriate column mappings if needed (Refer below for details on providing column name configurations)**

Example:

.. code-block:: json

    source_schema_name: 'ehr_source'

The ``etl_schema_name`` is required when performing ETL operations either in a standalone manner or as part of the pipeline. The utility will create a new schema with the name provided in the configuration file to host the intermediate temporary ETL tables of the migration process.

Example:

.. code-block:: json

    etl_schema_name: 'etl_source'

The ``cdm_schema_name`` is required when the final migrated CDM data is needed to be stored either in a standalone manner or as part of the pipeline. The utility will create a new schema with the name provided in the configuration file to host the final CDM data.

Example:

.. code-block:: json

    cdm_schema_name: 'omop_migrated'


Vocabulary files path
~~~~~~~~~~~~~~~~~~~~~


CSV file column mapping
~~~~~~~~~~~~~~~~~~~~~~~


Pre-processing
--------------


Database
~~~~~~~~

The following database connection details needs to be updated in the configuration file for extracting any information from the standard schema;

.. code-block:: json

    # database connection details
    db_details = {
        "sql_host_name": 'localhost',
        "sql_port_number": 5434,
        "sql_user_name": 'postgres',
        "sql_password": 'mysecretpassword',
        "sql_db_name": 'mimic4',
    }
