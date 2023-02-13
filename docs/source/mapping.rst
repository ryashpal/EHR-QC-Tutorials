Concept Mapping
===============

The EHR-QC provides option to perform custim mapping in two different ways;

1. In a standalone manner
-------------------------

When invoked in a standalone manner, the results will include mappings from basic algorithms namely ``Fuzzy``, ``Reverse Index``, and ``Medcat``. The results are stored in a csv file for the user to review the concept mappings from different algorithms and feed it to the migration pipeline manually. The mappings are grouped together to assign different confidence levels like ``Low``. ``Medium``, and ``High`` based on the number of algorithms in support of the concept as shown in the table below;

+---------+-----------+-------------------+---------------+------------+------------+
|Case     | Fuzzy     | Semantic (Medcat) | Reverse Index | Output     | Confidence |
+=========+===========+===================+===============+============+============+
|Case 1   | Con 1     | Con 1             | Con 1         | Con 1      | High       |
+---------+-----------+-------------------+---------------+------------+------------+
|Case 2A  | Con 1     | Con 1             | Con 2         | Con 1      | Medium     |
+---------+-----------+-------------------+---------------+------------+------------+
|Case 2B  | Con 1     | Con 1             | Con 2         | Con 2      | Low        |
+---------+-----------+-------------------+---------------+------------+------------+
|Case 3A  | Con 2     | Con 1             | Con 1         | Con 1      | Medium     |
+---------+-----------+-------------------+---------------+------------+------------+
|Case 3B  | Con 2     | Con 1             | Con 1         | Con 2      | Low        |
+---------+-----------+-------------------+---------------+------------+------------+
|Case 4A  | Con 1     | Con 2             | Con 1         | Con 1      | Medium     |
+---------+-----------+-------------------+---------------+------------+------------+
|Case 4B  | Con 1     | Con 2             | Con 1         | Con 2      | Low        |
+---------+-----------+-------------------+---------------+------------+------------+
|Case 5A  | Con 1     | Con 2             | Con 3         | Con 1      | Low        |
+---------+-----------+-------------------+---------------+------------+------------+
|Case 5B  | Con 1     | Con 2             | Con 3         | Con 2      | Low        |
+---------+-----------+-------------------+---------------+------------+------------+
|Case 5C  | Con 1     | Con 2             | Con 3         | Con 3      | Low        |
+---------+-----------+-------------------+---------------+------------+------------+

The concept mapper utility as part of the EHR-QC provides functions to perform the concept mapping in a standalone manner.

Help menu
~~~~~~~~~

To display the help menu of the OMOP-CDM migration utility.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.ConceptMapper -h

or

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.ConceptMapper --help

Output

.. code-block:: console

    usage: ConceptMapper.py [-h] [--vocab_path VOCAB_PATH] [--cdb_path CDB_PATH] [--mc_status_path MC_STATUS_PATH] [--model_pack_path MODEL_PACK_PATH]
                            domain_id vocabulary_id concept_class_id concepts_path concept_name_row mapped_concepts_save_path

    Perform concept mapping

    positional arguments:
    domain_id             Domain ID of the standard vocabulary to be mapped
    vocabulary_id         Vocabulary ID of the standard vocabulary to be mapped
    concept_class_id      Concept class ID of the standard vocabulary to be mapped
    concepts_path         Path for the concepts csv file
    concept_name_row      Name of the concept name row in the concepts csv file
    mapped_concepts_save_path
                            Path for saving the mapped concepts csv file

    optional arguments:
    -h, --help            show this help message and exit
    --vocab_path VOCAB_PATH
                            Path for the Medcat vocab file
    --cdb_path CDB_PATH   Path for the Medcat cdb file
    --mc_status_path MC_STATUS_PATH
                            Path for the Medcat mc_status folder
    --model_pack_path MODEL_PACK_PATH
                            Path for the Medcat model_pack_path zip file

Generate mappings
~~~~~~~~~~~~~~~~~

To create mappings for the concepts present in the ``concepts_path`` under the column ``concept_name_row`` and save it as a csv file.

.. code-block:: console

    (.venv) user@hostname:~/workspace/EHRQC$.venv/bin/python -m ehrqc.standardise.migrate_omop.ConceptMapper '<Domain Name>' '<Vocabulary Name>' '<Concept Class Name>' '/path/to/concepts.csv' '<Concept Column Name>' '/path/to/output.csv' --model_pack_path='/path/to/model_pack.zip


2. Autonmatically as part of the OMOP-CDM migration pipeline
------------------------------------------------------------

To automatically invoke the concept mapping as part of the OMOP-CDM migration pipeline, please refer to the `Custom Mapping <https://ehr-qc-tutorials.readthedocs.io/en/latest/config.html#custom-mapping>`_ section in the `Configuration Page <https://ehr-qc-tutorials.readthedocs.io/en/latest/config.html#>`_.
