Concept Mapping
===============


Help menu
---------

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
-----------------

To create mappings for the concepts present in the ``concepts_path`` under the column ``concept_name_row`` and save it as a csv file.

.. code-block:: console

    .venv/bin/python -m ehrqc.standardise.migrate_omop.ConceptMapper '<Domain Name>' '<Vocabulary Name>' '<Concept Class Name>' '/path/to/concepts.csv' '<Concept Column Name>' '/path/to/output.csv' --model_pack_path='/path/to/model_pack.zip
