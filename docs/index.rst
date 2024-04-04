EHRQC
=====

EHR-QC is a complete end-to-end pipeline to standardise and preprocess Electronic Health Records (EHR) for downstream integrative machine learning applications. This utility has two distinct modules;

1. Standardisation
2. Pre-processing

Both the modules can be run as a single end-to-end pipeline or individual components can be run in a standalone manner.

This utility is primarily focussed to provide a domain specific toolset for performing commmon standardisation and pre-processing tasks while handling the healthcare data. A command line interface is designed to provide an abstraction over the internal implementation details while at the same time being easy to use for anyone with basic Linux skills.

.. image:: source/images/ehr-qc.PNG


.. topic:: Acknowledgements

   .. image:: source/images/monash.png
      :width: 20 %

   .. image:: source/images/alfred.png
      :width: 20 %

   .. image:: source/images/superbugai.png
      :width: 20 %

Cite
----

Yashpal Ramakrishnaiah, Nenad Macesic, Geoffrey I. Webb, Anton Y. Peleg, Sonika Tyagi,
*EHR-QC: A streamlined pipeline for automated electronic health records standardisation and preprocessing to predict clinical outcomes,
Journal of Biomedical Informatics*,
Volume 147,
2023,
104509,
ISSN 1532-0464,
https://doi.org/10.1016/j.jbi.2023.104509.
(https://www.sciencedirect.com/science/article/pii/S1532046423002307)

Contents
--------

.. toctree::

   install_ehrqc
   install_ehrqc_preprocess
   install_ehrqc_standardise
   config
   migrate
   process
   use_cases
   case_study
