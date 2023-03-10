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

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Plot demographics_explore temp/mimic_demographics.csv temp/mimic_demographics_explore.html -c {<"optional mapping information">}

This function expects the file to contain the information under the following columns;

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

`Example Demographics Plots <https://ryashpal.github.io/EHRQC/demographics.html>`_


Explore Vitals Plots
~~~~~~~~~~~~~~~~~~~~

To generate QC plots from the vitals data obtained from the `source_path` and save it in the `save_path`. If the source csv file is not in a standard format, then a `column_mapping` needs to be provided.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Plot vitals_explore temp/mimic_vitals.csv temp/mimic_vitals_explore.html -c {<"optional mapping information">}

This function expects the file to contain the information under the following columns;

+----------------------+--------------------------------------+
| Expected Column Name | Column Details                       |
+======================+======================================+
| heartrate            | Heart Rate                           |
+----------------------+--------------------------------------+
| sysbp                | Systolic Blood Pressure              |
+----------------------+--------------------------------------+
| diabp                | Diastolic Blood Pressure             |
+----------------------+--------------------------------------+
| meanbp               | Mean Blood Pressure                  |
+----------------------+--------------------------------------+
| resprate             | Respiratory Rate                     |
+----------------------+--------------------------------------+
| tempc                | Temperature                          |
+----------------------+--------------------------------------+
| spo2                 | Oxygen Saturation                    |
+----------------------+--------------------------------------+
| gcseye               | Glasgow Coma Scale - Eye Response    |
+----------------------+--------------------------------------+
| gcsverbal            | Glasgow Coma Scale - Verbal Response |
+----------------------+--------------------------------------+
| gcsmotor             | Glasgow Coma Scale - Motor Response  |
+----------------------+--------------------------------------+

`Example Vitals Plots <https://ryashpal.github.io/EHRQC/vitals.html>`_


Explore Lab measurements Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To generate QC plots from the lab measurements data obtained from the `source_path` and save it in the `save_path`. If the source csv file is not in a standard format, then a `column_mapping` needs to be provided.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Plot lab_measurements_explore temp/mimic_lab_measurements.csv temp/mimic_lab_measurements_explore.html -c {<"optional mapping information">}


This function expects the file to contain the information under the following columns;

+----------------------+--------------------------------------------+
| Expected Column Name | Column Details                             |
+======================+============================================+
| glucose              | Glucose                                    |
+----------------------+--------------------------------------------+
| hemoglobin           | Hemoglobin                                 |
+----------------------+--------------------------------------------+
| anion_gap            | Anion Gap                                  |
+----------------------+--------------------------------------------+
| bicarbonate          | Bicarbonate                                |
+----------------------+--------------------------------------------+
| calcium_total        | Calcium Total                              |
+----------------------+--------------------------------------------+
| chloride             | Chloride                                   |
+----------------------+--------------------------------------------+
| creatinine           | Creatinine                                 |
+----------------------+--------------------------------------------+
| magnesium            | Magnesium                                  |
+----------------------+--------------------------------------------+
| phosphate            | Phosphate                                  |
+----------------------+--------------------------------------------+
| potassium            | Potassium                                  |
+----------------------+--------------------------------------------+
| sodium               | Sodium                                     |
+----------------------+--------------------------------------------+
| urea_nitrogen        | Urea Nitrogen                              |
+----------------------+--------------------------------------------+
| hematocrit           | Hematocrit                                 |
+----------------------+--------------------------------------------+
| mch                  | Mean Cell Hemoglobin                       |
+----------------------+--------------------------------------------+
| mchc                 | Mean Corpuscular Hemoglobin Concentration  |
+----------------------+--------------------------------------------+
| mcv                  | Mean Corpuscular Volume                    |
+----------------------+--------------------------------------------+
| platelet_count       | Platelet Count                             |
+----------------------+--------------------------------------------+
| rdw                  | Red cell Distribution Width                |
+----------------------+--------------------------------------------+
| red_blood_cells      | Red Blood Cells                            |
+----------------------+--------------------------------------------+
| white_blood_cells    | White Blood Cells                          |
+----------------------+--------------------------------------------+

`Example Lab measurements Plots <https://ryashpal.github.io/EHRQC/lab_measurements.html>`_


Vitals Outlier Plots
~~~~~~~~~~~~~~~~~~~~

To generate QC plots from the vitals data obtained from the `source_path` and save it in the `save_path`. If the source csv file is not in a standard format, then a `column_mapping` needs to be provided.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Plot vitals_outliers temp/mimic_vitals_imputed.csv temp/mimic_vitals_outliers.html

This function expects the file to contain the information under the following columns;

+----------------------+--------------------------------------+
| Expected Column Name | Column Details                       |
+======================+======================================+
| heartrate            | Heart Rate                           |
+----------------------+--------------------------------------+
| sysbp                | Systolic Blood Pressure              |
+----------------------+--------------------------------------+
| diabp                | Diastolic Blood Pressure             |
+----------------------+--------------------------------------+
| meanbp               | Mean Blood Pressure                  |
+----------------------+--------------------------------------+
| resprate             | Respiratory Rate                     |
+----------------------+--------------------------------------+
| tempc                | Temperature                          |
+----------------------+--------------------------------------+
| spo2                 | Oxygen Saturation                    |
+----------------------+--------------------------------------+
| gcseye               | Glasgow Coma Scale - Eye Response    |
+----------------------+--------------------------------------+
| gcsverbal            | Glasgow Coma Scale - Verbal Response |
+----------------------+--------------------------------------+
| gcsmotor             | Glasgow Coma Scale - Motor Response  |
+----------------------+--------------------------------------+

`Example Vitals Plots <https://ryashpal.github.io/EHRQC/vitals_outliers.html>`_


Lab measurements Outlier Plots
~~~~~~~~~~~~~~~~~~~~

To generate QC plots from the lab measurements data obtained from the `source_path` and save it in the `save_path`. If the source csv file is not in a standard format, then a `column_mapping` needs to be provided.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Plot lab_measurements_outliers temp/mimic_lab_measurements_imputed.csv temp/mimic_lab_measurements_outliers.html

This function expects the file to contain the information under the following columns;

+----------------------+--------------------------------------------+
| Expected Column Name | Column Details                             |
+======================+============================================+
| glucose              | Glucose                                    |
+----------------------+--------------------------------------------+
| hemoglobin           | Hemoglobin                                 |
+----------------------+--------------------------------------------+
| anion_gap            | Anion Gap                                  |
+----------------------+--------------------------------------------+
| bicarbonate          | Bicarbonate                                |
+----------------------+--------------------------------------------+
| calcium_total        | Calcium Total                              |
+----------------------+--------------------------------------------+
| chloride             | Chloride                                   |
+----------------------+--------------------------------------------+
| creatinine           | Creatinine                                 |
+----------------------+--------------------------------------------+
| magnesium            | Magnesium                                  |
+----------------------+--------------------------------------------+
| phosphate            | Phosphate                                  |
+----------------------+--------------------------------------------+
| potassium            | Potassium                                  |
+----------------------+--------------------------------------------+
| sodium               | Sodium                                     |
+----------------------+--------------------------------------------+
| urea_nitrogen        | Urea Nitrogen                              |
+----------------------+--------------------------------------------+
| hematocrit           | Hematocrit                                 |
+----------------------+--------------------------------------------+
| mch                  | Mean Cell Hemoglobin                       |
+----------------------+--------------------------------------------+
| mchc                 | Mean Corpuscular Hemoglobin Concentration  |
+----------------------+--------------------------------------------+
| mcv                  | Mean Corpuscular Volume                    |
+----------------------+--------------------------------------------+
| platelet_count       | Platelet Count                             |
+----------------------+--------------------------------------------+
| rdw                  | Red cell Distribution Width                |
+----------------------+--------------------------------------------+
| red_blood_cells      | Red Blood Cells                            |
+----------------------+--------------------------------------------+
| white_blood_cells    | White Blood Cells                          |
+----------------------+--------------------------------------------+

`Example Lab measurements Plots <https://ryashpal.github.io/EHRQC/lab_measurements_outliers.html>`_


Impute
------


Help menu
~~~~~~~~~

To display the help menu;

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Impute -h

Output

.. code-block:: console

    usage: Impute.py [-h] [-sp SAVE_PATH] [-a ALGORITHM] action source_path

    EHRQC

    positional arguments:
    action                Action to perform [compare, impute]
    source_path           Source data path

    optional arguments:
    -h, --help            show this help message and exit
    -sp SAVE_PATH, --save_path SAVE_PATH
                            Path of the file to store the outputs (required only for action=impute)
    -a ALGORITHM, --algorithm ALGORITHM
                            Missing data imputation algorithm [mean, median, knn, miss_forest, expectation_maximization, multiple_imputation]


Compare imputation
~~~~~~~~~~~~~~~~~~

To create a random missingness in the data given by the file at ``source_path`` and compare 6 different missing data algorithms [``mean``, ``median``, ``knn``, ``miss forest``, ``expectation maximisation``, ``multiple imputation``] and report their reconstriction r-squared scores. If the non-numeric feilds from the data obtained from ``source_path`` are ignored for imputation. Further, the rows corresponding to the missing values in the data are ignored, instead a random missingness is created of the same proportion as that of original data.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Impute 'compare' temp/mimic_vitals.csv


Imputation
~~~~~~~~~~

To impute missing values in the data obtained from the `source_path` using the specified algorithm and save it in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Impute impute '/path/to/data.csv' -sp='/path/to/data_imputed.csv' -a=<algorithm name>

This function support the following algorithms

- mean
- median
- knn
- miss forest
- expectation maximisation
- multiple imputation


Anomalies
---------


Help menu
~~~~~~~~~

To display the help menu of the OMOP-CDM migration utility.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Anomalies -h

or

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Anomalies --help

Output

.. code-block:: console

    usage: Anomalies.py [-h] [-dm] [-do] [-cm] [-co] source_path save_path save_prefix

    Detect and Correct Anomalies

    positional arguments:
    source_path           Source data path
    save_path             Path to save the data
    save_prefix           Path to save the data

    optional arguments:
    -h, --help            show this help message and exit
    -dm, --detect_missing
                            Detect Missing Values in the dataframe
    -do, --detect_outliers
                            Detect Outliers in the dataframe
    -cm, --correct_missing
                            Correct Missing Values in the dataframe
    -co, --correct_outliers
                            Correct Outliers in the dataframe

Detect Anomalies
~~~~~~~~~~~~~~~~

To detect missing data and outliers in the data from the ``source_path`` and save it as a html file at the ``save_path`` with the file prefix ``save_prefix``. To visualise missing data, optional argument ``-dm`` needs to be provided. For detecting outliers, optional argument ``-do`` needs to be provided.

Example:

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Anomalies 'test_data.csv' 'testing' 'test_001' -dm -do


Correct Anomalies
~~~~~~~~~~~~~~~~~

To correct missing data and outliers in the data from the ``source_path`` and save it as a csv file at the ``save_path`` with the file prefix ``save_prefix``. To correct missing data, optional argument ``-cm`` needs to be provided. For correcting outliers, optional argument ``-co`` needs to be provided.

Example:

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Anomalies 'test_data.csv' 'testing' 'test_001' -cm -co


Pre-processing Pipeline
-----------------------


Help menu
~~~~~~~~~

To display the help menu;

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline -h

or

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline --help

Output

.. code-block:: console

    usage: Pipeline.py [-h] [-d] [-i] save_path source_db data_type schema_name

    EHRQC

    positional arguments:
    save_path             Path of the folder to store the outputs
    source_db             Source name [mimic, omop]
    data_type             Data type name [demographics, vitals, lab_measurements]
    schema_name           Source schema name

    optional arguments:
    -h, --help            show this help message and exit
    -d, --draw_graphs     Draw graphs to visualise EHR data quality
    -i, --impute_missing  Impute missing values by automatically selecting the best imputation strategy for this data


Extract OMOP Demographics
~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_demographics_raw_data.csv` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp omop demographics omop_cdm


Extract OMOP Vitals
~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_vitals_raw_data.csv` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp omop vitals omop_cdm


Extract OMOP Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_lab_measurements_raw_data.csv` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp omop lab_measurements omop_cdm


Extract MIMIC Demographics
~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_demographics_raw_data.csv` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp mimic demographics mimiciv


Extract MIMIC Vitals
~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_vitals_raw_data.csv` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp mimic vitals mimiciv


Extract MIMIC Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_lab_measurements_raw_data.csv`, and a  in the `save_path`.
### To extract Lab Measurements data from MIMIC schema

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp mimic lab_measurements mimiciv


MIMIC Demographics Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_demographics_raw_data.csv`, and a html file containing the generated graphs with the name `mimic_demographics_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp mimic demographics mimiciv -d


OMOP Demographics Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_demographics_raw_data.csv`, and a html file containing the generated graphs with the name `omop_demographics_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp omop demographics omop_cdm -d


MIMIC Vitals Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_vitals_raw_data.csv`, and a html file containing the generated graphs with the name `mimic_vitals_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp mimic vitals mimiciv -d


OMOP Vitals Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_vitals_raw_data.csv`, and a html file containing the generated graphs with the name `omop_vitals_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp omop vitals omop_cdm -d


MIMIC Lab measurements Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_lab_measurements_raw_data.csv`, and a html file containing the generated graphs with the name `mimic_lab_measurements_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp mimic lab_measurements mimiciv -d


OMOP Lab measurements Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_lab_measurements_raw_data.csv`, and a html file containing the generated graphs with the name `omop_lab_measurements_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp omop lab_measurements omop_cdm -d


Impute MIMIC Vitals
~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_vitals_raw_data.csv`, a csv file containing the imputed data with the name `mimic_vitals_imputed_data.csv`, and a html file containing the generated graphs with the name `mimic_vitals_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp mimic vitals mimiciv -d -i


Impute OMOP Vitals
~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_vitals_raw_data.csv`, a csv file containing the imputed data with the name `omop_vitals_imputed_data.csv`, and a html file containing the generated graphs with the name `omop_vitals_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp omop vitals omop_cdm -d -i


Impute MIMIC Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_lab_measurements_raw_data.csv`, a csv file containing the imputed data with the name `mimic_lab_measurements_imputed_data.csv`, and a html file containing the generated graphs with the name `mimic_lab_measurements_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp mimic lab_measurements mimiciv -d -i


Impute OMOP Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_lab_measurements_raw_data.csv`, a csv file containing the imputed data with the name `omop_lab_measurements_imputed_data.csv`, and a html file containing the generated graphs with the name `omop_lab_measurements_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Pipeline temp omop lab_measurements omop_cdm -d -i
