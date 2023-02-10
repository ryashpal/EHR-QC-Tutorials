Configuration
=============

The pipeline might need some of the configurations below, depending on the functionality being used.


OMOP-CDM migration
------------------

The following configurations mighe be required for OMOP-CDM migration process.


Migration schema names
~~~~~~~~~~~~~~~~~~~~~~

These configurations hold the names of the schema to be created to host the migrated tables. There are four such possible configurations.

1. lookup_schema_name
2. source_schema_name
3. etl_schema_name
4. cdm_schema_name

**Note: All four schema names can be separate if the data needs to be seggregated in different schemas to avoid mixing them up. Optionally they can also be the same in which case all the data will be stored in a single database schema. With this flexibility, it is also possible to group some types of data into a single schema while keeping the others separate. For example, it is possible to store all the intermediate data in a single schema by providing the same name for ``lookup_schema_name``, ``source_schema_name``, and ``etl_schema_name`` but a different name for ``cdm_schema_name`` to keep the migrated EHR data in a separate schema**

The ``lookup_schema_name`` is required when importing standard vocabularies either in a standalone manner or as part of the OMOP-CDM migration pipeline. The utility will create a new schema with the name provided in the configuration file to host the imported vocabularies.

Example:

.. code-block:: json

    lookup_schema_name: 'lookup_test'

The ``source_schema_name`` is required when importing EHR files either in a standalone manner or as part of the OMOP-CDM migration pipeline. The utility will create a new schema with the name provided in the configuration file to host the imported EHR data.

**Note: If the EHR is already present in the database instead of a flat file, the database schema name where the EHR is hosted can be provided here along with the appropriate column mappings if needed (Refer below for details on providing column name configurations)**

Example:

.. code-block:: json

    source_schema_name: 'ehr_source'

The ``etl_schema_name`` is required when performing ETL operations either in a standalone manner or as part of the OMOP-CDM migration pipeline. The utility will create a new schema with the name provided in the configuration file to host the intermediate temporary ETL tables of the migration process.

Example:

.. code-block:: json

    etl_schema_name: 'etl_source'

The ``cdm_schema_name`` is required when the final migrated CDM data is needed to be stored either in a standalone manner or as part of the OMOP-CDM migration pipeline. The utility will create a new schema with the name provided in the configuration file to host the final CDM data.

Example:

.. code-block:: json

    cdm_schema_name: 'omop_migrated'


Vocabulary files path
~~~~~~~~~~~~~~~~~~~~~

The path of the standard ontology vocabulary files to be imported can be specified in this configuration. This configuration will be used for importing the external vocabulary files either in a standalone manner it as part of the OMOP-CDM migration pipeline.

Example:

.. code-block:: json

    vocabulary = {
        'concept': '/path/to/CONCEPT.csv',
        'vocabulary': '/path/to/VOCABULARY.csv',
        'domain': '/path/to/DOMAIN.csv',
        'concept_class': '/path/to/CONCEPT_CLASS.csv',
        'concept_relationship': '/path/to/CONCEPT_RELATIONSHIP.csv',
        'relationship': '/path/to/RELATIONSHIP.csv',
        'concept_synonym': '/path/to/CONCEPT_SYNONYM.csv',
        'concept_ancestor': '/path/to/CONCEPT_ANCESTOR.csv',
        'tmp_custom_mapping': '/path/to/tmp_custom_mapping.csv',
    }


CSV file column mapping
~~~~~~~~~~~~~~~~~~~~~~~

The paths of the CSV files containing the EHR data to be imported and the column mappings if the column names in the CSV file are not the expected column names for the pipeline. This configuration will be used for importing the external EHR files either in a standalone manner it as part of the OMOP-CDM migration pipeline.

In general, it takes the form;

.. code-block:: json

    patients = {

        file_name: Path for the csv file
        
        column_mapping: {
        
            -- column name in the file: standard column name,
            
        },
        
    }

For example, the mapping information for entity `Patients` will be as shown below;

.. code-block:: json

    patients = {
        'file_name': '/path/to/patients.csv',
        'column_mapping': {
            'subject_id': "<Subject ID column name in the csv file>",
            'gender': "<Gender column name in the csv file>",
            'anchor_age': "<Age column name in the csv file>",
            'anchor_year': "<Year column name in the csv file>",
            'dod': "<DOD column name in the csv file>"
        },
    }

A mapping is required, if an entity has non expected column name. All the different entities and their expected column names are given below.

**Entity: ``admissions``**

+----------------------+
| Expected Column Name |
+======================+
| subject_id           |
+----------------------+
| hadm_id              |
+----------------------+
| admittime            |
+----------------------+
| dischtime            |
+----------------------+
| deathtime            |
+----------------------+
| admission_type       |
+----------------------+
| admission_location   |
+----------------------+
| discharge_location   |
+----------------------+
| insurance            |
+----------------------+
| language             |
+----------------------+
| marital_status       |
+----------------------+
| ethnicity            |
+----------------------+
| edregtime            |
+----------------------+
| edouttime            |
+----------------------+
| hospital_expire_flag |
+----------------------+


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
