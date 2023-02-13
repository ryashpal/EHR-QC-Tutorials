Anomalies
=========


Help menu
---------

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
----------------

To detect missing data and outliers in the data from the ``source_path`` and save it as a html file at the ``save_path`` with the file prefix ``save_prefix``. To visualise missing data, optional argument ``-dm`` needs to be provided. For detecting outliers, optional argument ``-do`` needs to be provided.

Example:

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Anomalies 'test_data.csv' 'testing' 'test_001' -dm -do


Correct Anomalies
----------------

To correct missing data and outliers in the data from the ``source_path`` and save it as a csv file at the ``save_path`` with the file prefix ``save_prefix``. To correct missing data, optional argument ``-cm`` needs to be provided. For correcting outliers, optional argument ``-co`` needs to be provided.

Example:

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.qc.Anomalies 'test_data.csv' 'testing' 'test_001' -cm -co
