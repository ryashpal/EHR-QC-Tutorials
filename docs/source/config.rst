Configuration
=============

The pipeline might need some of the configurations below, depending on the functionality being used;

Database
--------

The following database connection details needs to be updated in the configuration file for extracting any information from the standard schema;

.. code-block:: xml
    db_details = {
        "sql_host_name": 'localhost',
        "sql_port_number": 5434,
        "sql_user_name": 'postgres',
        "sql_password": 'mysecretpassword',
        "sql_db_name": 'mimic4',
    }

