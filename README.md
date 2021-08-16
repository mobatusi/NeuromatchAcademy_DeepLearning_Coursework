# NeuromatchAcademy_DeepLearning_Coursework
Coursework from Aug2-20 Neuromatch Academy

There is emerging evidence that the temporal dynamics of brain activity can be classified into 4 states: 
   - Interictal (between seizures, or baseline), 
   - Preictal (prior to seizure), 
   - Ictal (seizure), and 
   - Post-ictal (after seizures). 
Seizure forecasting requires the ability to reliably identify a preictal state that can be differentiated from the interictal, ictal, and postictal state. 
The primary challenge in seizure forecasting is differentiating between the preictal and interictal states. 
The main goals of this ecosystem are to advance the accurate classification of the preictal brain state in humans with epilepsy and to advance our understanding of epilepsy.

The dataset contains iterictal and preictal data from the Melbourne-NeuroVista seizure trial and the Melbourne-University AES-MathWorks-NIH Seizure Prediction Challenge for the purposes of advancing seizure prediction research.
https://www.kaggle.com/c/melbourne-university-seizure-prediction
   - requires use of a Python-based API available on GitHub (for best results use the latest version) 
   - use the Python API to download data and store it to file once, rather than merging the API into your prediction algorithm or analysis code and unnecessarily repeatedly downloading large amounts 
   - Download data using the ‘neurovista_contest_data_downloader.py’ script.
   - You can view the data on the Seer web-browser-based data viewer, which also requires a Seer username and password for login. The viewer can be accessed https://app.seermedical.com/au 

The contest data challenge
   - Human brain activity was recorded in the form of intracranial EEG (iEEG) 
   - iEEG was sampled from 16 electrodes at 400 Hz, and recorded voltages were referenced to the electrode group average. 
   - The challenge is to distinguish between ten minute long data clips covering an hour prior to a seizure, and ten minute iEEG clips of interictal activity. 
   - Only lead seizures, defined here as seizures occurring four hours or more after another seizure, are included in the training and testing data sets.
   - interictal data segments were restricted to be at least four hours before or after any seizure.

The contest dataset
   - The iEEG data segments are downloaded to folders containing training and testing data for each human patient
   - Data can be downloaded by running neurovista_contest_data_downloader.py in the seer-py/Examples folder cloned from Github
   - Training data
      - The training data is organized into ten minute EEG clips labeled "Preictal" for pre-seizure data segments, or "Interictal" for non-seizure data segments.
      - Training data segments are numbered sequentially.
      - PatITrain_J_K - the Jth training data segment corresponding to the Kth class (K=0 for interictal, K=1 for preictal) for the Ith patient (there are three patients).
      - It is possible to determine which 10 minute segments belong to specific 1 hour blocks for the training data by grouping every 6 blocks based on the index J in 'PatITrain_J_K' (i.e. block index = ceil(J/6) ). 
         - Use the modulo operator (i.e. segment position = ((J-1) % 6)+1 ).
         - For preictal training segments 'PatITrain_J_1' for J > 150 this method cannot be applied either and these segments can be viewed as extra files and it is up to the user if they wish to use them in training.
   - Testing data
      - Testing data are in random order.
      - PatITest_J_0 - the Jth testing data segment corresponding to the Ith patient. (Note 0 in the filename does not indicate any class).
   - Preictal data
      - Preictal training and testing data segments are provided covering one hour prior to seizure with a five minute seizure horizon. (i.e. from 1:05 to 0:05 before seizure onset.) 
   - Interictal data
      - one hour sequences of interictal ten minute data segments are provided. 
      - The interictal data were chosen randomly from the full data record, with the restriction that interictal segments be at least 4 hours away from any seizure, to avoid contamination with preictal or postictal signals.
   - The class labels for the training and testing sets are provided as separate files:
      - contest_train_data_labels.csv – training set labels for all patients
      - contest_test_data_labels_public.csv – test set labels for all patients
      - only the ‘public’ test set (30% of the test set) labels from the ‘Melbourne-University AES-MathWorks-NIH Seizure Prediction Challenge’ are provided. 

Data Caveats
   - Any part of any 10-minute data segment can potentially contain “data drop-out” where the intracranial brain implant has temporarily failed to record data. This data drop-out corresponds to iEEG signal values of zeros across all channels at a given time sample. 
   - The data may also contain artifacts such as large amplitude rapid signal transitions that can be removed from analysis.

Algorithms
   - The code for the top algorithms from the ‘Melbourne-University AES-MathWorks-NIH Seizure Prediction Challenge’
      - https://github.com/epilepsyecosystem 
   -  To share code on https://github.com/epilepsyecosystem you must contact Dr Levin Kuhlmann (levin.kuhlmann@monash.edu) to be invited to become a member of the GitHub organisation.

Benchmarking
   - Contact Dr Levin Kuhlmann (levin.kuhlmann@monash.edu) to submit complete test set predictions (predictions should be scaled between 0 to 1 as an estimate of preictal probability) 
   - Submit a solution file and obtain Area Under the Curve (AUC) performance scores for algorithm for the private test set (as per the terms and conditions). 
   - Algorithms are ranked on the evolving ecosystem leaderboard.  
   - The top algorithms in the ecosystem will have the opportunity of being annually evaluated on the full dataset of 15 patients from the NeuroVista trial. 
   - To participate in the ultimate benchmark test, people are required to:
      - Prepare algorithms with Python 3 (preferably using Anaconda)
      - Make algorithms efficient such that the time taken to classify a 10 minute data segment is at most 30 seconds on a single core.
         - This duration needs to include all feature calculation and classification steps of a pretrained algorithm.
      - Make algorithms that utilise at most 100 MB of RAM when classifying a 10 minute data segment.
      - Submit code so that your algorithm can easily be retrained and tested on new data (using the same filename structure given for the contest data) and different data segment file durations by the independent evaluator.
      - CodeEvaluationDocs
         - https://github.com/epilepsyecosystem/CodeEvaluationDocs
