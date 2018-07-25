# ParkinsonsDiseaseDataAnalysis

## Introduction:
### Description and literature:

In this study, we will analyze the patients’ data who are diagnosed with the disease. Using speech data from subjects is expected to help the development of a noninvasive diagnostic. People with Parkinsonism (PWP) suffer from speech impairments like dysphonia (defective use of the voice), hypophonia (reduced volume), monotone (reduced pitch range), and dysarthria (difficulty with articulation of sounds or syllables). Therefore, our analysis in this project will be based on voice parameters of the affected. 

### Data:
The dataset was created by Athanasios Tsanas and Max Little of the University of Oxford, in collaboration with 10 medical centers in the US and Intel Corporation who developed the tele-monitoring device to record the speech signals.

This dataset is composed of a range of biomedical voice measurements from 42 people with early-stage Parkinson’s disease recruited to a six-month trial of a tele-monitoring device for remote symptom progression monitoring. The recordings were automatically captured in the patient’s homes.

Columns in the dataset contain subject number, subject age, subject gender, time interval from baseline recruitment date, motor UPDRS, total UPDRS, and 16 biomedical voice measures. Each row corresponds to one of 5,875 voice recording from these individuals.
The main aim of the data is to predict the motor and total UPDRS scores (‘motor_UPDRS’ and ‘total_UPDRS’) from the 16 voice measures.
The data is in ASCII CSV format. The rows of the CSV file contain an instance corresponding to one voice recording. There are around 200 recordings per patient, the subject number of the patient is identified in the first column. 

### Attribute Information:

Subject: Integer that uniquely identifies each subject
Age: Subject age
Sex: Subject gender ‘0’ - male, ‘1’ - female
Test_time: Time since recruitment into the trial. The integer part is the number of days since recruitment
Motor_UPDRS: Clinician’s motor UPDRS score, linearly interpolated
Total_UPDRS: Clinician’s total UPDRS score, linearly interpolated
Jitter (%), Jitter(Abs), Jitter. RAP, Jitter. PPQ5, Jitter. DDP: Several measures of variation in fundamental frequency (Frequency parameters)
Shimmer, Shimmer (dB), Shimmer. APQ3, Shimmer. APQ5, Shimmer. APQ11, Shimmer. DDA: Several measures of variation in amplitude (Amplitude parameters)
NHR, HNR: Two measures of ratio of noise to tonal components in the voice
RPDE: A nonlinear dynamical complexity measure
DFA: Signal fractal scaling exponent
PPE: A nonlinear measure of fundamental frequency variation

## Data Cleaning and Outlier Removal:

Our first step is going through the dataset and identify any missing value or outlier to take necessary measures. This step is essential to prepare the data for fruitful analysis. There are no missing values in our dataset.

### Correlations between the variables

![correlation_plot](https://user-images.githubusercontent.com/5343403/43222766-b46c0a58-9016-11e8-875a-780cb9e3ebe7.png)

We can see that all the jitter variables highly correlate with Shimmer variables.

### Outlier Detection

In this section we will look at some of the significant features and check if there are outliers available.

![3](https://user-images.githubusercontent.com/5343403/43223116-b20fb07e-9017-11e8-824a-9b7a7b489dc8.png)
![4](https://user-images.githubusercontent.com/5343403/43223118-b22a3b24-9017-11e8-8321-42f0ace4fd84.png)
![1](https://user-images.githubusercontent.com/5343403/43223119-b243299a-9017-11e8-8d6a-0d607e937d51.png)
![2](https://user-images.githubusercontent.com/5343403/43223120-b263fa6c-9017-11e8-9fc7-fd7e4c1de40b.png)
![5](https://user-images.githubusercontent.com/5343403/43223125-b761ac3a-9017-11e8-95aa-a99934930e55.png)
![6](https://user-images.githubusercontent.com/5343403/43223126-b772f5c6-9017-11e8-86b1-d18ffd0f1b7f.png)
![9](https://user-images.githubusercontent.com/5343403/43223146-c6dde1d8-9017-11e8-8e56-9c61aefe1e70.png)

In our scattered plot between total_UPDRS and Jitter, it looks like, we can see out outlier observations in our data. Similarly, in our plots with total_UPDRS vs Shimmer, total_UPDRS vs NHR, total_UPDRS vs RPDE, total_UPDRS vs DFA, and total_UPDRS vs PPE, we can see some outlier observations.

We will now look into bivariate boxplots in our data to look for outlier observations in our data.



