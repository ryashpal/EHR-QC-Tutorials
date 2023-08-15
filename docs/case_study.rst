##########
Case Study
##########

Extraction and preparation of Sepsis data for Machine Learning applications.

*******
Outline
*******

#. Introduction
#. Set-up
#. Cohort Selection
#. Data Standardisation
#. Data Preperation
#. Data Pre-processing
#. Data Preparation
#. Conclusion

1. Introduction
===============

In this case study, our main objective is to showcase the effectiveness of EHR-QC. We achieve this by employing the toolkit to handle EHR data comprehensively, preparing it for utilization in Machine Learning applications. To illustrate, we select a group of patients who have been diagnosed with Sepsis from the public MIMIC IV EHR database. Subsequently, we employ the EHR-QC standardization module to standardise the EHR records for these patients, converting them into the OMOP-CDM schema. Following this, we employ the EHR-QC data pre-processing module. This involves extracting information from the standardized schema, generating exploratory reports, and identifying as well as rectifying any anomalies present in the data.

2. Set-up
=========

In this case study, we utilizeed the Dockerized EHR-QC. For comprehensive instructions on configuring the Docker environment, please consult the documentation provided at the following link: https://ehr-qc-tutorials.readthedocs.io/en/latest/install.html#docker

3. Cohort selection
===================

From the MIMIC IV dataset, we've identified all patients and admissions related to Sepsis. This selection involves utilizing ICD-9 codes ``995.91``, ``995.92``, and ``785.52``, as well as ICD-10 codes ``A419``, ``R6520``, and ``R6521`` which pertain to Sepsis, Severe Sepsis, and Septic Shock. Subsequently, we've extracted the complete electronic health record (EHR) data associated with these patients and admissions, converting them into csv files.

This process yielded a total of ``12,276`` patients corresponding to ``14,870`` admissions, along with their respective EHR data.

4. Data standardisation
=======================

In the subsequent phase, the EHR data associated with the Sepsis cohort, as contained in the CSV files, is standardized by being structured according to the OMOP-CDM schema. This task is accomplished through the utilization of the EHR-QC utility, which carries out a series of sequential steps, culminating standard EHR representation. The procedure involves the following stages:

#. Incorporating the Standard Vocabulary (Athena)
#. Importing EHR data from the CSV files
#. Staging the data within staging tables
#. Integrating custom concept mappings for concepts that deviate from the standard
#. Executing the migration process
#. Transitioning to the OMOP-CDM schema

For more comprehensive insights into each of these stages, please consult the following link: https://ehr-qc-tutorials.readthedocs.io/en/latest/migrate.html#omop-cdm-migration.

This culminated in the successful migration of the entire cohort (100 %), encompassing all the ``12,276`` patients and ``14,870`` admissions, alongside their respective EHR data in a fully automated manner.

Utilizing well-established, compatible tools and techniques becomes notably more straightforward when working with data that has been transformed into a standardized format.

5. Data Extraction
==================

During this stage, we retrieve the demographics, vital signs, and lab measurements of the Sepsis cohort from the standardized OMOP-CDM schema using EHR-QC pre-processing module.

Successful extraction yield the following data:

#. Demographics data for ``12,276`` patients, encompassing 7 attributes: ``Age``, ``Weight``, ``Height``, ``Gender``, ``Ethnicity``, ``Date of Birth``, and ``Date of Death`` (if applicable)
#. Vital signs data for ``8,436`` patients, comprising 10 attributes: ``Heart rate``, ``Systolic Blood Pressure``, ``Diastolic Blood Pressure``, ``Mean Blood Pressure``, ``Respiratory rate``, ``Body Temperature``, ``Oxygen Saturation (SpO2)``, ``Glasgow Coma Scale (GCS) Eye score``, ``GCS Verbal score``, and ``GCS Motor score``
#. Lab measurements for ``12,169`` patients, involving 29 attributes: ``Lactate``, ``Blood Carbon Dioxide``, ``Albumin``, ``Urine Glucose``, ``Band Form Neutrophils``, ``Blood Base Excess``, ``Blood Potassium``, ``Blood pH``, ``Serum Chloride``, ``Serum Carbon Dioxide``, ``Bilirubin``, ``Blood Auto Leukocytes``, ``Creatinine``, ``INR (International Normalized Ratio)``, ``Serum Sodium``, ``Blood Sodium``, ``Hemoglobin``, ``Body Fluid pH``, ``Platelet Count``, ``Urea Nitrogen``, ``Serum Glucose``, ``Blood Chloride``, ``Oxygen``, ``Bicarbonate``, ``Serum Potassium``, ``Anion Gap``, ``Manual Blood Leukocytes``, ``Hematocrit``, and ``aPTT (Activated Partial Thromboplastin Time)``

It's worth noting that some patients lack recorded values for the listed vital signs or lab measurements attributes. Consequently, these patients are excluded from the extracted files, resulting in a reduction in the total number of rows after this stage. Specifically, our efforts yield complete demographic data for the entire Sepsis cohort of ``12,276`` patients, while lab measurements are available for ``12,169`` patients, and vital signs data is present for approximately ``8,436`` patients only.

To understand the extraction capabilities offered by the EHR-QC, kindly consult the documentation provided at: https://ehr-qc-tutorials.readthedocs.io/en/latest/process.html#extract

6. Data Pre-processing
======================

Next, the exploration and anomaly reports are generated from the extracted data using EHR-QC pre-processing module. It will also highlight the presence of anomalous data, and provide specific pointers to correct them. Furthermore, it has the capability to automatically impute the missing values and remove the outliers.

More details on the EHR-QCs pre-processing utility can be found here: https://ehr-qc-tutorials.readthedocs.io/en/latest/process.html#pre-processing

In this section we illustrate a few use cases demonstrating the functionality of the module; 

Units Mix-up
------------

The analysis of demographic data reveled a multimodal distribution within the "Height" attribute. The generated plot in the demographic data exploration report clearly illustrates the overlap of two distributions. A closer examination of the value ranges within these distributions hints at the potential mix-up of two distinct units of measurement: ``inches`` and ``feet``.

.. image:: source/images/height_distribution_before.png
Figure 1: Histogram showing the distribution of ``Height`` attribute before unit standardisation

To preempt any downstream errors stemming from this mixed measurement scenario, we have rectified the situation to establish uniformity. Following these adjustments, a renewed exploration report was generated, showcasing the successful normalization of the "Height" attribute to a consistent unit of measurement.

.. image:: source/images/height_distribution_after.png
Figure 2: Histogram showing the distribution of ``Height`` attribute after unit standardisation

Empty attributes
----------------

The EHR-QC data exploration reports for lab measurements reveal certain attributes that lack any recorded values, while others exhibit low overall coverage. These attributes contribute insufficient information to enhance the predictive capability of the encompassing machine learning models. Additionally, they impede the efficacy of missing value imputation algorithms.

.. list-table:: Table 1: Coverage of all attributes in lab measurements
   :widths: 25 10
   :header-rows: 1

   * - Attribute
     - Count
   * - 	lactate
     - 	0
   * - 	carbondioxide_blood
     - 	0
   * - 	albumin
     - 	8643
   * - 	glucose_urine
     - 	1377
   * - 	band_form_neutrophils
     - 	5464
   * - 	base_excess_in_blood
     - 	0
   * - 	potassium_blood
     - 	0
   * - 	ph_blood
     - 	0
   * - 	chloride_serum
     - 	12142
   * - 	carbondioxide_serum
     - 	0
   * - 	bilirubin
     - 	10225
   * - 	leukocytes_blood_auto
     - 	0
   * - 	creatinine
     - 	12146
   * - 	inr
     - 	11001
   * - 	sodium_serum
     - 	12145
   * - 	sodium_blood
     - 	0
   * - 	hemoglobin
     - 	12152
   * - 	ph_bodyfluid
     - 	0
   * - 	platelet_count
     - 	12140
   * - 	urea_nitrogen
     - 	12133
   * - 	glucose_serum
     - 	12123
   * - 	chloride_blood
     - 	0
   * - 	oxygen
     - 	0
   * - 	bicarbonate
     - 	12143
   * - 	potassium_serum
     - 	12144
   * - 	anion_gap
     - 	12132
   * - 	leukocytes_blood_manual
     - 	12141
   * - 	hematocrit
     - 	12144
   * - 	aptt
     - 	10880

Consequently, in the context of this analysis, an arbitrary choice has been made to retain an attribute for subsequent analysis only if its overall coverage surpasses the threshold of 95%. Employing this criterion, slightly less than half of the total attributes, specifically 12 out of 29, have met the threshold and are retained for utilization in downstream tasks.

.. list-table:: Table 2: Coverage of retained attributes in lab measurements
   :widths: 25 10
   :header-rows: 1

   * - Attribute
     - Count
   * - 	chloride_serum
     - 	12142
   * - 	creatinine
     - 	12146
   * - 	sodium_serum
     - 	12145
   * - 	hemoglobin
     - 	12152
   * - 	platelet_count
     - 	12140
   * - 	urea_nitrogen
     - 	12133
   * - 	glucose_serum
     - 	12123
   * - 	bicarbonate
     - 	12143
   * - 	potassium_serum
     - 	12144
   * - 	anion_gap
     - 	12132
   * - 	leukocytes_blood_manual
     - 	12141
   * - 	hematocrit
     - 	12144

Missing Value Imputation
------------------------

The anomaly reports generated by EHR-QC have revealed the existence of missing values within the dataset. The report provides a breakdown of the number of missing values and their corresponding percentages for each attribute, as illustrated in the Table 3 below:

.. list-table:: Table 3: Table showing the counts and percentage of missing value for vitals before imputation
   :widths: 25 30 30
   :header-rows: 1

   * - Attribute
     - Missing Count
     - Missing Percentage
   * - 	heartrate
     - 	11
     - 	0.13
   * - 	sysbp
     - 	47
     - 	0.56
   * - 	diabp
     - 	47
     - 	0.56
   * - 	meanbp
     - 	20
     - 	0.24
   * - 	resprate
     - 	9
     - 	0.11
   * - 	tempc
     - 	107
     - 	1.28
   * - 	spo2
     - 	24
     - 	0.29
   * - 	gcseye
     - 	50
     - 	0.6
   * - 	gcsverbal
     - 	57
     - 	0.68
   * - 	gcsmotor
     - 	62
     - 	0.74

While certain algorithms can accommodate missing data, others require complete datasets. In cases where algorithmic handling of missing values is not viable, the EHR-QC offers a missing data imputation utility function. This function allows for the specification of the desired imputation algorithm or the automatic simulation of missingness based on the same proportion as the input data, utilizing various algorithms and selecting the optimal one. Using this utility, we performed imputation to address missing values within the vitals and lab measurements. Consequently, the missing table was updated as depicted in the Table 4 below:

.. list-table:: Table 4: Table showing the counts and percentage of missing value for vitals after imputation
   :widths: 25 30 30
   :header-rows: 1

   * - Attribute
     - Missing Count
     - Missing Percentage
   * - 	heartrate
     - 	0
     - 	0
   * - 	sysbp
     - 	0
     - 	0
   * - 	diabp
     - 	0
     - 	0
   * - 	meanbp
     - 	0
     - 	0
   * - 	resprate
     - 	0
     - 	0
   * - 	tempc
     - 	0
     - 	0
   * - 	spo2
     - 	0
     - 	0
   * - 	gcseye
     - 	0
     - 	0
   * - 	gcsverbal
     - 	0
     - 	0
   * - 	gcsmotor
     - 	0
     - 	0

The missing data plots in the EHR-QC reports visualise the missingness in the data. Please refer to the provided figures (Figure 3 and Figure 4) showcasing the missing data plots before and after imputation.

.. image:: source/images/missing_value_plot_before.png
Figure 3: Missing data plot before imputation

.. image:: source/images/missing_value_plot_after.png
Figure 4: Missing data plot after imputation

Removal of Extreme Values (Outliers)
------------------------------------

Another class of anomalies, which has come to our attention through the anomaly reports (see Table 5), pertains to the presence of outliers. These outliers represent extreme values that deviate significantly from the norm, rendering them inappropriate due to their eccentric nature.

.. list-table:: Table 5: Table showing the counts and percentage of outliers for vitals before imputation
   :widths: 25 30 30
   :header-rows: 1

   * - Attribute
     - Outlier Count
     - Outlier Percentage
   * - 	heartrate
     - 	33
     - 	0.39
   * - 	sysbp
     - 	344
     - 	4.1
   * - 	diabp
     - 	179
     - 	2.13
   * - 	meanbp
     - 	281
     - 	3.34
   * - 	resprate
     - 	113
     - 	1.34
   * - 	tempc
     - 	476
     - 	5.71
   * - 	spo2
     - 	233
     - 	2.77
   * - 	gcseye
     - 	0
     - 	0
   * - 	gcsverbal
     - 	0
     - 	0
   * - 	gcsmotor
     - 	809
     - 	9.66

These observations can disproportionately impact the predictive capabilities of Machine Learning models and thus necessitate removal. Typically, this is achieved by establishing rigid thresholds using specific statistical measures. For instance, values that surpass 2.5 times the standard deviation (SD) or 1.5 times the interquartile range (IQR) are flagged as outliers. However, we acknowledge that these predefined thresholds lack nuance and often fail to consider the domain-specific intricacies of the data. To address this limitation, EHR-QC employs a technique known as Item Response Theory (IRT) to autonomously identify extreme values. Leveraging this approach, we have implemented this feature to detect and subsequently eliminate outliers from ensuing processes. The effectiveness of outlier removal is clearly demonstrated in the provided figures (Figure 5 and Figure 6), showcasing the successful elimination of all potentially disruptive outliers from the dataset, ensuring they do not interfere with downstream modeling endeavors.

.. image:: source/images/outliers_before.png
Figure 5: Distribution of heart rate before removing the outliers 

.. image:: source/images/outliers_after.png
Figure 6: Distribution of heart rate after removing the outliers

7. Data Preparation
===================

As a final step, we have used the data after correcting the anomalies (Refer Figure 7) to perform standardisation and normalisation using utlity functions of EHR-QC to create final data matrix.

.. image:: source/images/heartrate.png
Figure 7: Distribution of heart rate without anomalies

Standardisation refers to reshaping the data such that it follows a unit normal distribution with mean 0 and standard deviation 1 (Refer Figure 8).

.. image:: source/images/heartrate_standardised.png
Figure 8: Distribution of heart rate after standardisation

Normalisation refers to rescaling the data such that all the values lie between 0 and 1 (Refer Figure 8).

.. image:: source/images/heartrate_rescaled.png
Figure 9: Distribution of heart rate after normalisation

8. Conclusion
=============

Discuss the final counts available for performing Machine Learning applications.

Previously, we have identified and corrected anomalies using various functions provided by EHR-QC.
