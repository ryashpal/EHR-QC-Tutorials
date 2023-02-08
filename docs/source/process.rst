Pre-processing
==============


Extract
-------

**Note 1: The extract module is required if the EHR data exists in a relational database**

**Note 2: If the EHR data is in the flat file (.csv), please proceed to next sections**


Help menu
~~~~~~~~~

To display the help menu of the Extract functionality.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.extract.Extract -h


or

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.extract.Extract --help


Output

.. code-block:: console
    usage: Extract.py [-h] save_path source_db data_type schema_name

    EHRQC

    positional arguments:
    save_path    Path of the file to store the outputs
    source_db    Source name [mimic, omop]
    data_type    Data type name [demographics, vitals, lab_measurements]
    schema_name  Source schema name

    optional arguments:
    -h, --help   show this help message and exit


Extract OMOP Demographics
~~~~~~~~~~~~~~~~~~~~~~~~~

To extract the demographics data from omop schema and store it in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.extract.Extract temp/omop_demograpics.csv omop demographics omop_cdm


Extract OMOP Vitals
~~~~~~~~~~~~~~~~~~~

To extract the vitals data from omop schema and store it in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.extract.Extract temp/omop_vitals.csv omop vitals omop_cdm


Extract OMOP Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To extract the lab measurements data from omop schema and store it in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.extract.Extract temp/omop_lab_measurements.csv omop lab_measurements omop_cdm


Extract MIMIC Demographics
~~~~~~~~~~~~~~~~~~~~~~~~~

To extract the demographics data from mimic schema and store it in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.extract.Extract temp/mimic_demographics.csv mimic demographics mimiciv


Extract MIMIC Vitals
~~~~~~~~~~~~~~~~~~~~

To extract the vitals data from mimic schema and store it in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.extract.Extract temp/mimic_vitals.csv mimic vitals mimiciv


Extract MIMIC Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To extract the lab measurements data from mimic schema and store it in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.extract.Extract temp/mimic_lab_measurements.csv mimic lab_measurements mimiciv


Plot
----


Help menu
~~~~~~~~~

To display the help menu of the Plot functionality.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Plot -h


or

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Plot --help


Output

.. code-block:: console

    usage: Plot.py [-h] [-c COLUMN_MAPPING] plot_type source_path save_path

    EHRQC

    positional arguments:
    plot_type             Type of plot to generate [demographics_explore, vitals_explore, lab_measurements_explore, vitals_outliers,
                            lab_measurements_outliers]
    source_path           Source data path
    save_path             Path of the file to store the output

    optional arguments:
    -h, --help            show this help message and exit
    -c COLUMN_MAPPING, --column_mapping COLUMN_MAPPING


The column mapping has to be in json format as shown below;

.. code-block:: json

    '{"expected_column_name": "custom_column_name"}'

For instance, if the "Age" attribute in demographics csv file is under the column name "Number of Years" instead of default "age" column name, then the following mapping can be applied;

.. code-block:: json

    '{"age": "Number of Years"}'

Similarly, more than one columns can be mapped in this manner;

.. code-block:: json

    '{"age": "Number of Years", "gender": "Sex"}'


Explore Demographics Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~

To generate QC plots from the demograhic data obtained from the `source_path` and save it in the `save_path`. If the source csv file is not in a standard format, then a `column_mapping` needs to be provided.

.. code-block:: json

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Plot demographics_explore temp/mimic_demographics.csv temp/mimic_demographics_explore.html -c {<"optional mapping information">}


This utility expects the file to contain the information under the following columns;

+----------------------+---------------------------+
| Expected Column Name | Column Details            |
+======================+===========================+
| age                  | Age of the person         |
+----------------------+---------------------------+
| weight               | Weight of the person      |
+----------------------+---------------------------+
| height               | Height of the person      |
+----------------------+---------------------------+
| gender               | Gender of the person      |
+----------------------+---------------------------+
| ethnicity            | Ethnicity of the person   |
+----------------------+---------------------------+

Example Output: 

`Demographics Plots`_

.. _Demographics Plots: (https://ryashpal.github.io/EHRQC/demographics.html)

