Pre-processing
==============


Extract
-------

**Note 1: The extract module is required if the EHR data exists in a relational database**

**Note 2: If the EHR data is in the flat file (.csv), please skip this section and proceed to next sections**


Help menu
~~~~~~~~~

To display the help menu of the Extract functionality.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.extract.Extract -h


or

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.extract.Extract --help


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

    (.venv) app_user@hostname:~$python -m ehrqc.extract.Extract temp/omop_demograpics.csv omop demographics omop_cdm


Extract OMOP Vitals
~~~~~~~~~~~~~~~~~~~

To extract the vitals data from omop schema and store it in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.extract.Extract temp/omop_vitals.csv omop vitals omop_cdm


Extract OMOP Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To extract the lab measurements data from omop schema and store it in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.extract.Extract temp/omop_lab_measurements.csv omop lab_measurements omop_cdm


Extract MIMIC Demographics
~~~~~~~~~~~~~~~~~~~~~~~~~

To extract the demographics data from mimic schema and store it in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.extract.Extract temp/mimic_demographics.csv mimic demographics mimiciv


Extract MIMIC Vitals
~~~~~~~~~~~~~~~~~~~~

To extract the vitals data from mimic schema and store it in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.extract.Extract temp/mimic_vitals.csv mimic vitals mimiciv


Extract MIMIC Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To extract the lab measurements data from mimic schema and store it in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.extract.Extract temp/mimic_lab_measurements.csv mimic lab_measurements mimiciv


Exploration Plots
-----------------


Help menu
~~~~~~~~~

To display the help menu of the Exploration Plot functionality.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Plot -h


or

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Plot --help


Output

.. code-block:: console

    usage: Plot.py [-h] [-c COLUMN_MAPPING] plot_type source_path save_path

    EHRQC

    positional arguments:
    plot_type             Type of plot to generate [demographics_explore, vitals_explore, lab_measurements_explore]
    source_path           Source data path
    save_path             Path of the file to store the output

    optional arguments:
    -h, --help            show this help message and exit
    -c COLUMN_MAPPING, --column_mapping COLUMN_MAPPING


The column mapping has to be in json format as shown below;

.. code-block:: json

    '{"expected_column_name": "custom_column_name"}'

For instance, if the "Age" attribute in demographics csv file is under the column name "Number of Years" instead of the expected "age" column name as shown below.

+------------+-----------------+
| Patient ID | Number of Years |
+------------+-----------------+
| 00001      | 57              |
+------------+-----------------+
| 00002      | 45              |
+------------+-----------------+
| 00003      | 78              |
+------------+-----------------+
| 00004      | 35              |
+------------+-----------------+
| 00005      | 83              |
+------------+-----------------+

The following mapping can be applied;

.. code-block:: json

    '{"age": "Number of Years"}'

Similarly, more than one columns can be mapped in this manner;

For instance, if the demographics csv file contains "Age", "Sex", and "Date of Birth" column names inplace of "age", 'gender', and 'dob' names that are expected.

+------------+-----------------+-------+---------------+
| Patient ID | Number of Years | Sex   | Date of Birth |
+------------+-----------------+-------+---------------+
| 00001      | 57              | Male  | 04-02-1966    |
+------------+-----------------+-------+---------------+
| 00002      | 45              | Female| 04-02-1975    |
+------------+-----------------+-------+---------------+
| 00003      | 78              | Female| 04-02-1945    |
+------------+-----------------+-------+---------------+
| 00004      | 35              | Male  | 04-02-1988    |
+------------+-----------------+-------+---------------+
| 00005      | 83              | Male  | 04-02-1940    |
+------------+-----------------+-------+---------------+

The following mapping can be applied;

.. code-block:: json

    '{"age": "Number of Years", "gender": "Sex", "dob": "Date of Birth"}'


Explore Demographics Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~

To generate QC plots from the demograhic data obtained from the `source_path` and save it in the `save_path`. If the source csv file is not in a standard format, then a `column_mapping` needs to be provided.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Plot demographics_explore temp/mimic_demographics.csv temp/mimic_demographics_explore.html -c {<"optional mapping information">}

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

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Plot vitals_explore temp/mimic_vitals.csv temp/mimic_vitals_explore.html -c {<"optional mapping information">}

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

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Plot lab_measurements_explore temp/mimic_lab_measurements.csv temp/mimic_lab_measurements_explore.html -c {<"optional mapping information">}


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


Outlier Plots
-------------


Help menu
~~~~~~~~~

To display the help menu of the Outlier Plot functionality.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Outliers -h


or

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Outliers --help


Output

.. code-block:: console

    usage: Outliers.py [-h] [-c [COMBINATIONS ...]] source_file save_path
    
    EHRQC
    
    positional arguments:
      source_file           Source data file path
      save_path             Path of the directory to store the output
    
    optional arguments:
      -h, --help            show this help message and exit
      -c [COMBINATIONS ...], --combinations [COMBINATIONS ...]
                            Column combinations to plot (can have multiple column pairs).


.. note::

    Please ensure the csv file does not contain any missing data before using these functions.


.. note::

    There are two ways to call upon this function:

    1. The first approach involves providing the column combinations as command line arguments. Keep in mind that due to computational limitations, a maximum of 10 column pairs can be designated for plotting outliers using this method.

    2. Alternatively, in the second method, you need not specify the column combinations explicitly. In this scenario, the function derives column combinations for all possible pairs. It's important to note that, due to computational restrictions, the file can contain a maximum of 5 columns. This limitation results in 10 column combination pairs available for outlier plotting using this method.

    For more comprehensive information about each of these techniques, please consult the details below:


Plot specifying the combinations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To generate outlier plots from the data obtained from the `source_path` and save it in the `save_path` with a file named `outlier_report.html`, you can utilize the optional -c argument to specify column pairs. You have the flexibility to include multiple pairs by reusing this argument multiple times up to a maximum of 10 different column pairs.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Outliers /path/to/source_file.csv /path/to/save/ -c col1 col2 -c col2 col3 -c col3 col1

Plot without specifying the combinations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To generate outlier plots from the data obtained from the `source_path` and save it in the `save_path` with a file named `outlier_report.html`. The source file should not contain more than 5 columns.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Outliers /path/to/source_file.csv /path/to/save/

Generated outputs
~~~~~~~~~~~~~~~~~

After the function runs successfully, it will generate an HTML file named `outlier_report.html` in the `save_path`. This file will contain outlier plots, illustrating the relation between attributes, considering 2 attributes at a time. The points in these plots are color-coded based on their outlier scores.


`Example Vitals Outlier Plots <https://ryashpal.github.io/EHRQC/vitals_outliers.html>`_


`Example Lab measurements Outlier Plots <https://ryashpal.github.io/EHRQC/lab_measurements_outliers.html>`_


Impute
------


Help menu
~~~~~~~~~

To display the help menu;

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Impute -h

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

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Impute 'compare' temp/mimic_vitals.csv


Imputation
~~~~~~~~~~

To impute missing values in the data obtained from the `source_path` using the specified algorithm and save it in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Impute impute '/path/to/data.csv' -sp='/path/to/data_imputed.csv' -a=<algorithm name>

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

To display the help menu;

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Anomalies -h

or

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Anomalies --help

Output

.. code-block:: console

    usage: Anomalies.py [-h] [-dm] [-do] [-de] [-di] [-cm] [-co] source_path save_path save_prefix

    Detect and Correct Anomalies

    positional arguments:
    source_path           Source data path
    save_path             Path to save the data
    save_prefix           Prefix to the saved file

    optional arguments:
    -h, --help            show this help message and exit
    -dm, --detect_missing
                            Detect Missing Values in the dataframe
    -do, --detect_outliers
                            Detect Outliers in the dataframe
    -de, --detect_errors  Detect Errors in the dataframe
    -di, --detect_inconsistencies
                            Detect Inconsistencies in the dataframe
    -cm, --correct_missing
                            Correct Missing Values in the dataframe
    -co, --correct_outliers
                            Correct Outliers in the dataframe


Detect Anomalies
~~~~~~~~~~~~~~~~

To detect missing data, outliers, errors, and inconsistencies in the data from the ``source_path`` and save it as a html file at the ``save_path`` with the file prefix ``save_prefix``. To visualise missing data, optional argument ``-dm`` needs to be provided. For detecting outliers, optional argument ``-do`` needs to be provided.

Example:

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Anomalies 'test_data.csv' 'testing' 'test_001' -dm -do


Correct Anomalies
~~~~~~~~~~~~~~~~~

To correct missing data and outliers in the data from the ``source_path`` and save it as a csv file at the ``save_path`` with the file prefix ``save_prefix``. To correct missing data, optional argument ``-cm`` needs to be provided. For correcting outliers, optional argument ``-co`` needs to be provided.

Example:

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Anomalies 'test_data.csv' 'testing' 'test_001' -cm -co

Data using the raw data;

`Raw data <https://ryashpal.github.io/EHRQC/vitals_raw.html>`_

After imputing missing values;

`Imputed data <https://ryashpal.github.io/EHRQC/vitals_imputed.html>`_

After removing outliers;

`No outlier data <https://ryashpal.github.io/EHRQC/vitals_no_outliers.html>`_


Rescale
---------

Help menu
~~~~~~~~~

To display the help menu;

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Rescale -h

or

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Rescale --help

Output

.. code-block:: console

    usage: Rescale.py [-h] [-c COLUMNS] [-ssp SCALER_SAVE_PATH] [-mi MIN] [-ma MAX] source_path save_path

    EHRQC-Rescale

    positional arguments:
    source_path           Source data path (csv file)
    save_path             Path of a file to store the rescaled output

    optional arguments:
    -h, --help            show this help message and exit
    -c COLUMNS, --columns COLUMNS
                            Names of the columns to be scaled, enclosed in double quotes and seperated by comma
    -ssp SCALER_SAVE_PATH, --scaler_save_path SCALER_SAVE_PATH
                            Path of the scaler to save
    -mi MIN, --min MIN    Minimum value for the scaler (Default = 0)
    -ma MAX, --max MAX    Maximum value for the scaler (Default = 1)


Rescale Data
~~~~~~~~~~~~

To rescale the data from the ``source_path`` and save it as a csv file at the ``save_path`` . The optional argument ``columns`` can be provided to specify the columns to be rescaled. The optional argument ``scaler_save_path`` can be provided to save the scaler in a file. Mininum and Maximum values to the scalers by default is 0 and respectively, but they can be changed by passing ``--min``, and ``--max`` arguments.

Example:

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Rescale temp/omop_vitals_no_anomalies.csv temp/omop_vitals_rescaled.csv

Before rescaling;

`Original scale data <https://ryashpal.github.io/EHRQC/vitals_no_outliers.html>`_

After rescaling;

`Rescaled data <https://ryashpal.github.io/EHRQC/vitals_rescaled.html>`_


Standardise
-----------

Help menu
~~~~~~~~~

To display the help menu;

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Standardise -h

or

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Standardise --help

Output

.. code-block:: console

    usage: Standardise.py [-h] [-c COLUMNS] [-ssp SCALER_SAVE_PATH] source_path save_path

    EHRQC-Standardise

    positional arguments:
    source_path           Source data path (csv file)
    save_path             Path of a file to store the standardised output

    optional arguments:
    -h, --help            show this help message and exit
    -c COLUMNS, --columns COLUMNS
                            Names of the columns to be scaled, enclosed in double quotes and seperated by comma
    -ssp SCALER_SAVE_PATH, --scaler_save_path SCALER_SAVE_PATH
                            Path of the scaler to save


Standardise Data
~~~~~~~~~~~~~~~~

To standardise the data from the ``source_path`` and save it as a csv file at the ``save_path`` . The optional argument ``columns`` can be provided to specify the columns to be standardised. The optional argument ``scaler_save_path`` can be provided to save the scaler in a file.

Example:

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Standardise temp/omop_vitals_no_anomalies.csv temp/omop_vitals_rescaled.csv

Before standardising;

`Original scale data <https://ryashpal.github.io/EHRQC/vitals_no_outliers.html>`_

After standardising;

`Rescaled data <https://ryashpal.github.io/EHRQC/vitals_standardised.html>`_


Large file handling
-------------------

Frequently, during the initial stages of analyzing Electronic Health Record (EHR) data, we come across files of considerable size. A primary factor contributing to the file's largeness is the data's sparseness, where many cells lack values. Typically, this sparseness manifests in certain attributes (columns) within the EHR. For instance, attributes like temperature and heart rate might exhibit substantial coverage in the EHR, while attributes like SPO2 could have only a few recorded values. In such instances, it might be necessary to exclude the sparse attributes from further analysis if they don't contribute meaningful information for modeling purposes.

This tool provides the capability to manage large files by breaking them down into smaller segments. The initial function generates a report on missing data, indicating the percentage of missing values for all attributes within a specified file. The subsequent function eliminates attributes exceeding the specified missing data threshold and then saves the remaining data to an external file.


Help menu
~~~~~~~~~

To display the help menu;

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Coverage -h

or

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Coverage --help

Output

.. code-block:: console

    usage: Coverage.py [-h] [-d] [-p PERCENTAGE] [-sp SAVE_PATH] source_file chunksize id_columns [id_columns ...]
    
    Perform Coverage Analysis
    
    positional arguments:
      source_file           Source data file path
      chunksize             Number of chunks the input file should be fragmented into. By default: [chunksize=100]
      id_columns            List of ID columns. They are used to group the other columns to calculate missing percentage.
    
    optional arguments:
      -h, --help            show this help message and exit
      -d, --drop            Drop the columns
      -p PERCENTAGE, --percentage PERCENTAGE
                            Specify the cutoff percentage to drop the columns (required only for drop=True). By default: [-p=50]
      -sp SAVE_PATH, --save_path SAVE_PATH
                            Path of the file to store the outputs (required only for drop=True)


Display Missingness Report
~~~~~~~~~~~~~~~~~~~~~~~~~~

To display missing value percentages of all the attributes (columns) within a large csv file, by breaking down it in to number of pieces as indicated by `chunksize`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Coverage <Source File> <Chunk Size> <ID Columns>

For Example, if a large csv file is stored at /path/to/large_file.csv containing two id columns id1 and id2, we can use the below command to display the missingness report.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Coverage /path/to/large_file.csv 100 id1 id2


Remove Sparse Attributes
~~~~~~~~~~~~~~~~~~~~~~~~

To display missing value percentages of all the attributes (columns) within a large csv file, by breaking down it in to number of pieces as indicated by `chunksize`. Additionally, this function also removes the sparse attributes that are having a high missingness (above the specified threshold `-p`) and saves the resulting file in `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Coverage <Source File> <Chunk Size> -d -p <Threshold in Percentage> -sp <Save Path>

For Example, if a large csv file is stored at /path/to/large_file.csv containing two id columns id1 and id2, we can use the below command to display the missingness report and remove the columns with coverage below 50 % at the specified save path /path/to/save/.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Coverage /path/to/large_file.csv 100 id1 id2 -d -p 50 -sp /path/to/save/


Pre-processing Pipeline
-----------------------


Help menu
~~~~~~~~~

To display the help menu;

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline -h

or

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline --help

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

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp omop demographics omop_cdm


Extract OMOP Vitals
~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_vitals_raw_data.csv` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp omop vitals omop_cdm


Extract OMOP Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_lab_measurements_raw_data.csv` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp omop lab_measurements omop_cdm


Extract MIMIC Demographics
~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_demographics_raw_data.csv` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp mimic demographics mimiciv


Extract MIMIC Vitals
~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_vitals_raw_data.csv` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp mimic vitals mimiciv


Extract MIMIC Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_lab_measurements_raw_data.csv`, and a  in the `save_path`.
### To extract Lab Measurements data from MIMIC schema

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp mimic lab_measurements mimiciv


MIMIC Demographics Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_demographics_raw_data.csv`, and a html file containing the generated graphs with the name `mimic_demographics_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp mimic demographics mimiciv -d


OMOP Demographics Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_demographics_raw_data.csv`, and a html file containing the generated graphs with the name `omop_demographics_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp omop demographics omop_cdm -d


MIMIC Vitals Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_vitals_raw_data.csv`, and a html file containing the generated graphs with the name `mimic_vitals_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp mimic vitals mimiciv -d


OMOP Vitals Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_vitals_raw_data.csv`, and a html file containing the generated graphs with the name `omop_vitals_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp omop vitals omop_cdm -d


MIMIC Lab measurements Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_lab_measurements_raw_data.csv`, and a html file containing the generated graphs with the name `mimic_lab_measurements_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp mimic lab_measurements mimiciv -d


OMOP Lab measurements Explore Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_lab_measurements_raw_data.csv`, and a html file containing the generated graphs with the name `omop_lab_measurements_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp omop lab_measurements omop_cdm -d


Impute MIMIC Vitals
~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_vitals_raw_data.csv`, a csv file containing the imputed data with the name `mimic_vitals_imputed_data.csv`, and a html file containing the generated graphs with the name `mimic_vitals_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp mimic vitals mimiciv -d -i


Impute OMOP Vitals
~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_vitals_raw_data.csv`, a csv file containing the imputed data with the name `omop_vitals_imputed_data.csv`, and a html file containing the generated graphs with the name `omop_vitals_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp omop vitals omop_cdm -d -i


Impute MIMIC Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `mimic_lab_measurements_raw_data.csv`, a csv file containing the imputed data with the name `mimic_lab_measurements_imputed_data.csv`, and a html file containing the generated graphs with the name `mimic_lab_measurements_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp mimic lab_measurements mimiciv -d -i


Impute OMOP Lab measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a csv file containing the raw data with the name `omop_lab_measurements_raw_data.csv`, a csv file containing the imputed data with the name `omop_lab_measurements_imputed_data.csv`, and a html file containing the generated graphs with the name `omop_lab_measurements_plots.html` in the `save_path`.

.. code-block:: console

    (.venv) app_user@hostname:~$python -m ehrqc.qc.Pipeline temp omop lab_measurements omop_cdm -d -i
