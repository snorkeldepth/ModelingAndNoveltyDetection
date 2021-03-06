# Modeling and Novelty Detection in EEG signals
## For detecting epilepsy abnormalities

Epilepsy affects approximately 1% of the world's population and the majority of them lives in the low and middle-income countries (LMICs). Epilepsy is usually diagnosed by a human interpreter that reads through an EEG recording. The main barrier for people being diagnosed and treated for epilepsy, in LMICs, is the limited accessibility of EEG and the lack of interpreters. McKenzie et al. (2017) describes a study were data from portable EEG scanners is sent abroad for analysis by voluntaries.
This thesis examines how to shorten the time spent manually interpreting the EEG recordings, by using novelty detection. A preprocessing pipeline is suggested and two methods for novelty detection are examined.  

The thesis uses two real EEG data sets to validate the process. The first data set is from the Children's Hospital in Boston and includes records with labeled seizures. The other one is recorded in Guinea with a portable EEG scanner(SBS2) and contains no labels.  The methods are first analyzed and developed with the labeled data. These methods are then tested on the data from the SBS2. In the preprocessing steps artifacts are removed by classifying Independent Components. Features are extracted and a Principal Component Analysis is used for dimension reduction. An interesting observation was made when the Median absolute deviation (MAD) of the signal was inspected between subjects. The MAD values were in general higher for subjects showing epileptic discharge, indicating that it could be used as a global discriminant. Two methods based on Gaussian distribution were used for novelty detection which showed similar results. The first method was to fit a Gaussian distribution to the data and the latter was to use a robust Gaussian Mixture Model based on the work from Roberts and Tarassenko (1994). Abnormal data points were detected, however, there was no difference between subjects with and without epileptiform discharges. 

These first steps of running experiments on the data from the SBS2 show promising results. They offer an option to implement; a data quality control, a global discriminant using MAD and novelty detection to localize the abnormal data points. From a practical point of view, this thesis contributes an analysis on how to shorten the time spent on interpreting the data. This analysis could be used as preliminary work for future studies on the interpretation of SBS2 data from epilepsy patients in the LMICs.


### Preprocessing folder:
Preprocessing is mostly done in the script Main and Preprocess_SBS2. These following functions are used there:

Main.m and Preprocess_SBS2 includes:
 * GetData.m:  Extract data, adds channel location and transfer data from bipolar to unipolar if necessary
    * unipolar.m: Transform data from bipolar to unipolar
 * ReconstructData.m: PCA used to help with ranking issues.
 * cleanData.m: Run ICA and remove artifacts
    * remove_artifacts.m: remove artifacts, uses functions from  http://www2.imm.dtu.dk/ lf-fr/publications/indexpub.php
* GetFeatures.m: Extract the PSD features and Energy of the signal 
* GetFeatures1.m: Extract the Energy of the signal

### Gaussian folder:
* The scripts Main_Model1.m and Main_Model1_SBS2.m were used to generate all the results for the Maximum log likelihood model
   * Log_normal_clean.m computes the likelihood and plots up the zero-one signal
   * ROC_points.m computes TPR and FPR based on the likelihood
   * QplotNew.m used to make the Qplots

### GMM folder:
* Model2_new_cooling.m: The robust GMM model
   * gm_init.m used to initialize the first component
* Model2_Parameter_Validate.m: script to validate parameters
   * Model2_eMax.m used to find optimal e_max
   * Model2_alpha_t.m used to find optimal tau_alpha and alpha_0
* Model2_results.m used to generate final results
* Main_Model2.m used to make explanatory plots and small tests.  



