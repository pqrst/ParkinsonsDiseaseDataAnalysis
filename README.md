# Parkinsons Disease Data Analysis

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

![2](https://user-images.githubusercontent.com/5343403/43223622-5079b920-9019-11e8-8cba-3c46823e0b17.png)
![3](https://user-images.githubusercontent.com/5343403/43223623-508a541a-9019-11e8-86f9-23e546e01f0f.png)
![4](https://user-images.githubusercontent.com/5343403/43223624-509d9a2a-9019-11e8-88e4-907b184a64b3.png)
![5](https://user-images.githubusercontent.com/5343403/43223625-50b829ee-9019-11e8-9317-fed790ae3654.png)
![6](https://user-images.githubusercontent.com/5343403/43223626-50ccfc66-9019-11e8-8b61-4cf5c4e70d3a.png)
![1](https://user-images.githubusercontent.com/5343403/43223627-50e03d62-9019-11e8-8320-819664db37d0.png)

In our scattered plot between total_UPDRS and Jitter, it looks like, we can see out outlier observations in our data. Similarly, in our plots with total_UPDRS vs Shimmer, total_UPDRS vs NHR, total_UPDRS vs RPDE, total_UPDRS vs DFA, and total_UPDRS vs PPE, we can see some outlier observations.

We will now look into bivariate boxplots in our data to look for outlier observations in our data.

![8](https://user-images.githubusercontent.com/5343403/43225213-41e41ea0-901e-11e8-88fd-23c5c2447b0e.png)
![9](https://user-images.githubusercontent.com/5343403/43225214-41f3a190-901e-11e8-9d7d-639c9f11f9c2.png)
![7](https://user-images.githubusercontent.com/5343403/43225215-4204cf56-901e-11e8-94ec-e2e1f98fd81f.png)

The bivariate boxplot is showing a lot of our observations as outliers. Thus, we want to check our results with Convex Hull method as we don’t want to change the distribution of our data by removing the outliers.

#### Convex Hull Method

![10](https://user-images.githubusercontent.com/5343403/43225372-8f077a56-901e-11e8-928c-08c207814417.png)

Next we have removed outlier observations according to Convex hull.

### Dimensionality Reduction:

Our next step is dimensionality reduction. The dataset is very large with 22 variables and some of the variables have high correlations between them. So we are expecting to reduce the number of dimensions for better interpretation of the data.

#### Multi-dimensional scaling

First we try Multi-dimensional scaling which can help us visualizing the variable relationships in 2D graphs.

![11](https://user-images.githubusercontent.com/5343403/43225541-fba3ee1a-901e-11e8-8bca-976efb614e25.png)

The MDS plot clearly shows that age is creating a deviation between the datasets with female on the right and male on the left
#this significant deviation is because the voice pictch, frequency and amplitude totally differs by being in different ranges for different genders.

Criterion 1 and criterion 2 suggests that the first two coordinates can represents majority of the data points since the cummulative proportion is above the threshold value of 0.8. Hence the MDS plot can be on a 2D scatterplot

![12](https://user-images.githubusercontent.com/5343403/43225634-42b1b04e-901f-11e8-9fe6-5592c17da6b5.png)

Below are the findings from multidimensional scaling on the parkinsons data:

The statitical technique of multi dimensional scaling through this plot has confirmed that attributes form groups with similar patterns 1. All jitter variables follow a pattern 
2. All Shimmer variables follow a patter 
3. PPE and NHR form a pattern 
4. total UPDRS and motor UPDRS form a pattern 
5. test time and sex form a pattern 
6. Age contributes as a seperate attribute to the variation in data 
7. HNR contributes as a seperate attribute to the variation in data

These findings can be logically understood as 
1. Jitter is related to frequency measure so they form a pattern and it is logically valid 
2. Shimmer is related to amplitude measure so they form a pattern and it is logically valid 
3. Pitch of voice cord and noise to harmonics ratio are having an underlying relationship and that is observable through this finding 
4. Motor UPDRS score is impacting the total score and it makes sense 
5. Test time and sex are two independent factors and they are showing correlation by coincidence and this inference can be ignored 
6. Age contributes as a seperate attribute to the variation in data 
7. HNR contributes as a seperate attribute to the variation in data

### Feature Selection with Random forest

To confirm that the observations in the multi dimensional scaling can be used to better identify patients with disease and ideal measures to estimate progression of the disease and interpret the similarity between cetain measures let us apply another technique called random forests algorithm that uses gini index which is another way of measuring dissimilarity in the data like multi dimensional scaling.

Random forest helps in measuring and identifying the correct measure that can aid in differentiating the data and better differentiate patients and ranking the different variables by there contribution to the variance of the dataset and also on their significance in measuring progression of the disease.

#### Importance of each predictor

##### age              107.481221
##### DFA               30.280552
##### Jitter.Abs.       13.233061
##### test_time         13.181421
##### HNR               13.179312
##### RPDE              12.354213
##### sex               10.586328
##### PPE               10.273227
##### NHR                7.622037
##### Shimmer.APQ11      6.193817
##### Shimmer.DDA        5.627689
##### Shimmer.APQ3       5.509867
##### Shimmer.APQ5       5.475710
##### Jitter...          5.042090
##### Jitter.PPQ5        5.010854
##### Jitter.DDP         4.843811
##### Shimmer            4.836342
##### Jitter.RAP         4.544362
##### Shimmer.dB.        4.343984

On applying random forest we can observe that certain attributes contribute higher to the split in the dataset i.e. certain observations help better in categorising patients based on UPDRS scores and contribute higher to disease progression or severity. below are some analysis on the output:

### Exploratory Factor Analysis

Next we try exploratory factor analysis on the data to identify important factors.

parkinson.EFA <- factanal(parkinsons[, c(2:5,8,16,18:22)], 3, n.obs = nrow(parkinsons), rotation="varimax", control=list(trace=T))
start 1 value: 0.261 uniqs: 0.9705 0.8226 0.9983 0.9623 0.0050 0.2976 0.0050 0.0777 0.5282 0.6720 0.2671

#### parkinson.EFA
 Call:
 factanal(x = parkinsons[, c(2:5, 8, 16, 18:22)], factors = 3,     n.obs = nrow(parkinsons), rotation = "varimax", control = list(trace = T))

#### Uniquenesses:
           age           sex     test_time   motor_UPDRS   Jitter.Abs. 
         0.971         0.823         0.998         0.962         0.005 
         
          Shimmer.APQ11           NHR           HNR          RPDE           DFA 
                   0.298         0.005         0.078         0.528         0.672 
           PPE 
         0.267 
 
#### Loadings:
                             Factor1 Factor2 Factor3
               age                    0.162         
               sex                           -0.416 
               test_time                            
               motor_UPDRS            0.187         
               Jitter.Abs.    0.910           0.408 
               Shimmer.APQ11  0.651   0.523         
               NHR            0.915   0.159  -0.365 
               HNR           -0.689  -0.657  -0.131 
               RPDE           0.478   0.430   0.241 
               DFA            0.145   0.161   0.530 
               PPE            0.692   0.354   0.359 
 
                                Factor1 Factor2 Factor3
                SS loadings      3.294   1.134   0.965
                Proportion Var   0.299   0.103   0.088
                Cumulative Var   0.299   0.403   0.490
 
 Test of the hypothesis that 3 factors are sufficient.
 The chi square statistic is 1506 on 25 degrees of freedom.
 The p-value is 7.7e-303
 print(parkinson.EFA$loadings, cut = 0.45)

 #### Loadings:
                             Factor1 Factor2 Factor3
               age                                  
               sex                                  
               test_time                            
               motor_UPDRS                          
               Jitter.Abs.    0.910                 
               Shimmer.APQ11  0.651   0.523         
               NHR            0.915                 
               HNR           -0.689  -0.657         
               RPDE           0.478                 
               DFA                            0.530 
               PPE            0.692                 
 
                                Factor1 Factor2 Factor3
                SS loadings      3.294   1.134   0.965
                Proportion Var   0.299   0.103   0.088
                Cumulative Var   0.299   0.403   0.490
 
First, when we try to do exploratory factor analysis with all the variables, the model doesn’t run. After some research we have come to the conclusion that due to high multicolinearity between some variables (specificaly jitter and shimmer), the algorithm is not converging. So we decided to reduce the values that have high correlation between them. From the correlation plot we can see that jitter and shimmer variables have high correlation (0.9+) between themselves. So we tried building the model with one jitter and one shimmer variable. From the random forest analysis, we saw that Jitter.Abs. and Shimmer.APQ11 have highest significance in their corresponding frequency and amplitude groups. So we took these 2 variables in the exploratory factor analysis. Also both the updrs variables have 0.9+ correlation between them. So we took one from that group too.

With the above mentioned variables we explored different number of factors. But if we take 2 or 3 factors then only 40-45% data is explained. Also the age, sex and test_time have very small factor coefficient and large (0.8+) uniqueness. If we have 5/6 factors then the uniqueness of these variables lessen but still they are greater than 0.7.

From 3 factor analysis we can see that jitter, shimmer, NHR, HNR, RPDE and PPE have higher coefficents with Factor 1. However, from the random forest analysis, we have seen that age and DFA are the most significant variables, which have really low coefficient in these analysis.

### Confirmatory Factor Analysis

Next we try confirmatory factor analysis to compare if the results from EFA are correct.

parkinson.EFA <- factanal(parkinsons[, c(2:8,17,18:22)], 2, n.obs = nrow(parkinsons), rotation="varimax", control=list(trace=T))

start 1 value: 2.27 uniqs: 0.906 0.993 0.994 0.102 0.005 0.102 0.140 0.446 0.332 0.353 0.671 0.894 0.332
parkinson.EFA

Call:
 factanal(x = parkinsons[, c(2:8, 17, 18:22)], factors = 2, n.obs = nrow(parkinsons),     rotation = "varimax", control = list(trace = T))
 
#### Uniquenesses:
         age         sex   test_time motor_UPDRS total_UPDRS   Jitter... 
       0.906       0.993       0.993       0.102       0.005       0.102 
       
       Jitter.Abs. Shimmer.DDA         NHR         HNR        RPDE         DFA 
             0.140       0.446       0.332       0.353       0.671       0.894 
         PPE 
       0.332 
 
#### Loadings:
                         Factor1 Factor2
             age                  0.303 
             sex                        
             test_time                  
             motor_UPDRS          0.946 
             total_UPDRS          0.996 
             Jitter...    0.947         
             Jitter.Abs.  0.927         
             Shimmer.DDA  0.743         
             NHR          0.817         
             HNR         -0.798  -0.106 
             RPDE         0.561   0.120 
             DFA          0.286  -0.154 
             PPE          0.811         
 
                                Factor1 Factor2
                SS loadings       4.68   2.052
                Proportion Var    0.36   0.158
                Cumulative Var    0.36   0.518
 
 Test of the hypothesis that 2 factors are sufficient.
 The chi square statistic is 13107 on 53 degrees of freedom.
 The p-value is 0
 print(parkinson.EFA$loadings, cut = 0.5)

#### Loadings:
                         Factor1 Factor2
             age                        
             sex                        
             test_time                  
             motor_UPDRS          0.946 
             total_UPDRS          0.996 
             Jitter...    0.947         
             Jitter.Abs.  0.927         
             Shimmer.DDA  0.743         
             NHR          0.817         
             HNR         -0.798         
             RPDE         0.561         
             DFA                        
             PPE          0.811         
 
                                Factor1 Factor2
                SS loadings       4.68   2.052
                Proportion Var    0.36   0.158
                Cumulative Var    0.36   0.518
                
                summary(parkinson_sem)
                
                Model Chisquare =  5902   Df =  21 Pr(>Chisq) = 0
                Goodness-of-fit index =  0.823
                Adjusted goodness-of-fit index =  0.621
                SRMR =  0.0841
                
                Normalized Residuals
                  Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
                -19.17   -4.40    0.00   -0.91    2.48   11.40 
                
                R-square for Endogenous Variables
         age         sex Jitter.Abs. Shimmer.dB.         NHR         HNR 
      0.0107      0.0953      0.6165      0.6784      0.6461      0.6802 
        RPDE         DFA         PPE 
      0.4444      0.0773      0.7139 
      
      Parameter Estimates
          Estimate Std Error z value Pr(>|z|)                              
          lambda1   0.103   0.02382      4.33  1.47e-05 age <--- person             
          lambda2  -0.309   0.06082     -5.08  3.85e-07 sex <--- person             
          lambda7   0.785   0.01121     70.05  0.00e+00 Jitter.Abs. <--- voice      
          lambda12  0.824   0.01099     74.92  0.00e+00 Shimmer.dB. <--- voice      
          lambda17 -0.804   0.01105    -72.77  0.00e+00 NHR <--- noice              
          lambda18  0.825   0.01093     75.49  0.00e+00 HNR <--- noice              
          lambda19  0.667   0.01225     54.43  0.00e+00 RPDE <--- cord              
          lambda20 -0.278   0.01247    -22.29 4.73e-110 DFA <--- noice              
          lambda21  0.845   0.01166     72.49  0.00e+00 PPE <--- cord               
          theta1    0.989   0.01887     52.43  0.00e+00 age <--> age                
          theta2    0.905   0.04039     22.40 4.02e-111 sex <--> sex                
          theta7    0.384   0.00807     47.51  0.00e+00 Jitter.Abs. <--> Jitter.Abs.
          theta12   0.322   0.00728     44.16  0.00e+00 Shimmer.dB. <--> Shimmer.dB.
          theta17   0.354   0.00746     47.47  0.00e+00 NHR <--> NHR                
          theta18   0.320   0.00701     45.65  0.00e+00 HNR <--> HNR                
          theta19   0.556   0.01158     47.99  0.00e+00 RPDE <--> RPDE              
          theta20   0.923   0.01708     54.03  0.00e+00 DFA <--> DFA                
          theta21   0.286   0.00991     28.88 2.04e-183 PPE <--> PPE                
          rho3      0.223   0.06229      3.58  3.48e-04 voice <--> person           
          rho4      0.205   0.05972      3.42  6.16e-04 noice <--> person           
          rho5      0.546   0.11309      4.83  1.39e-06 cord <--> person            
          rho13    -1.144   0.00551   -207.42  0.00e+00 noice <--> voice            
          rho14     1.005   0.00716    140.29  0.00e+00 cord <--> voice             
          rho15    -0.981   0.00713   -137.55  0.00e+00 cord <--> noice             
          
          Iterations =  65
          restricted Cor matrix
          rescor <- parkinson_sem$C
          
          non-restricted Cor matrix
          nonrescor <- parkinson_sem$S
          
          differences of the elements of the observed covariance matrix and the covariance matrix of the fitted model
          covresiduals <- round(parkinson_sem$S - parkinson_sem$C, 3)
          
          semPaths(parkinson_sem, "est",edge.label.cex=1.5)
          
   ![model_1](https://user-images.githubusercontent.com/5343403/43227123-68a68d2a-9023-11e8-9ab9-acf8e76a85a9.png)
          
          summary(parkinson_sem)
          
          Model Chisquare =  342   Df =  8 Pr(>Chisq) = 4.65e-69
          Goodness-of-fit index =  0.982
          Adjusted goodness-of-fit index =  0.952
          SRMR =  0.0329
          
          Normalized Residuals
     Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    -7.14   -0.18    0.00    0.02    0.77    4.65 
    
    R-square for Endogenous Variables
    Jitter.Abs.           DFA           PPE Shimmer.APQ11           HNR 
         0.736         0.160         0.851         0.636         0.954 
          RPDE 
         0.448 
         
         Parameter Estimates
         Estimate Std Error z value Pr(>|z|) 
         lambda1  0.8577  0.01092     78.54  0.00e+00
         lambda2  0.3998  0.01318     30.35 2.71e-202
         lambda3  0.9223  0.01051     87.72  0.00e+00
         lambda4 -0.7978  0.01117    -71.40  0.00e+00
         lambda5  0.9770  0.00999     97.83  0.00e+00
         lambda6 -0.6694  0.01186    -56.42  0.00e+00
         corr1   -0.8357  0.00563   -148.31  0.00e+00
         theta1   0.2644  0.00726     36.41 2.85e-290
         theta2   0.8401  0.01593     52.75  0.00e+00
         theta3   0.1493  0.00671     22.24 1.29e-109
         theta4   0.3635  0.00793     45.85  0.00e+00
         theta5   0.0456  0.00596      7.64  2.19e-14
         theta6   0.5518  0.01081     51.04  0.00e+00
                                         
         lambda1 Jitter.Abs. <--- frequency      
         lambda2 DFA <--- frequency              
         lambda3 PPE <--- frequency              
         lambda4 Shimmer.APQ11 <--- amplitude    
         lambda5 HNR <--- amplitude              
         lambda6 RPDE <--- amplitude             
         corr1   amplitude <--> frequency        
         theta1  Jitter.Abs. <--> Jitter.Abs.    
         theta2  DFA <--> DFA                    
         theta3  PPE <--> PPE                    
         theta4  Shimmer.APQ11 <--> Shimmer.APQ11
         theta5  HNR <--> HNR                    
         theta6  RPDE <--> RPDE                  
         
         Iterations =  21
         restricted Cor matrix
         rescor <- parkinson_sem$C
         
         non-restricted Cor matrix
         nonrescor <- parkinson_sem$S
         
         differences of the elements of the observed covariance matrix and the covariance matrix of the fitted model
         covresiduals <- round(parkinson_sem$S - parkinson_sem$C, 3)
         
         semPaths(parkinson_sem, "est",edge.label.cex=1.5)

![model_2](https://user-images.githubusercontent.com/5343403/43227877-a40d5e96-9025-11e8-9573-c25128f8b186.png)

Since age, sex have very high uniqueness, we didn’t include them in the model. Also NHR and HNR have high correlation (0.9), so we included one of them. By reducing the highly correlated and highly unique values we got only 6 variables. Then we tried exploratory factor analysis on them with 2 factors and found that shimmer, HNR and RPD have higher coefficients with factor 1. So we named factor 1 as amplitude. The jitter, DFA and PPE variables have higher coefficients with factor 2. So we named factor 2 as frequency. Next we tried to build the model for confirmatory factor analysis with these observations.

From the summary we can see that this model has GFI and AGFI index greater than 0.95, which indicates the model is good. SRMR is 0.032, which is less than 0.05. It also indicates that this is a good model.

However, we know age is the most significant variable to identify if a patient has parkinsons disease or not. It is the most important factor in calculating the updrs score that helps identifying parkinsons in a patient. But dimensionality reduction with factor analysis is not able to acknowledge age due to high uniqueness in the variable. Also high multicollinearity is another possible reason for which the factor analysis algorithm does not converge with all the variables of the dataset. So we can reach to the conclusion that exploratory and confirmatory factor analysis are not suitable dimensionality reduction techniques for this dataset.

### Principal Component Analysis:

Next we try pca which can be a possible solution for the multi-collinearity problem.

parkinsons_pca_corr <- princomp(covmat = p_corr)
summary(parkinsons_pca_corr, loadings = T)
 
 Importance of components:
 
                            Comp.1 Comp.2 Comp.3 Comp.4 Comp.5 Comp.6 Comp.7
    Standard deviation      3.376  1.492 1.3134 1.2095 1.0758 1.0009 0.9112
    Proportion of Variance  0.518  0.101 0.0784 0.0665 0.0526 0.0455 0.0377
    Cumulative Proportion   0.518  0.619 0.6976 0.7641 0.8167 0.8623 0.9000
                        
                           Comp.8 Comp.9 Comp.10 Comp.11 Comp.12 Comp.13
    Standard deviation     0.8349  0.712  0.5402 0.45626 0.40866 0.31880
    Proportion of Variance 0.0317  0.023  0.0133 0.00946 0.00759 0.00462
    Cumulative Proportion  0.9317  0.955  0.9680 0.97742 0.98502 0.98964
                        
                           Comp.14 Comp.15 Comp.16  Comp.17  Comp.18  Comp.19
    Standard deviation     0.29550 0.22600 0.20713 0.143734 0.112470 0.095625
    Proportion of Variance 0.00397 0.00232 0.00195 0.000939 0.000575 0.000416
    Cumulative Proportion  0.99360 0.99593 0.99788 0.998815 0.999390 0.999805
                         
                            Comp.20  Comp.21  Comp.22
    Standard deviation     0.065415 7.02e-04 1.49e-04
    Proportion of Variance 0.000195 2.24e-08 1.01e-09
    Cumulative Proportion  1.000000 1.00e+00 1.00e+00
 
#### Loadings:
                              Comp.1 Comp.2 Comp.3 Comp.4 Comp.5 Comp.6 Comp.7 Comp.8
               subject.             -0.212        -0.334  0.649               -0.111
               age                  -0.313         0.168 -0.302        -0.845       
               sex                          0.271 -0.599  0.229        -0.353       
               test_time                                        -0.974        -0.197
               motor_UPDRS          -0.616 -0.131                       0.195  0.189
               total_UPDRS          -0.624 -0.149                       0.183  0.145
               Jitter...      0.267        -0.225 -0.190 -0.133                     
               Jitter.Abs.    0.249        -0.335                                   
               Jitter.RAP     0.259        -0.224 -0.226 -0.155                     
               Jitter.PPQ5    0.265        -0.134 -0.218 -0.145                     
               Jitter.DDP     0.259        -0.224 -0.226 -0.155                     
               Shimmer        0.276         0.246                                   
               Shimmer.dB.    0.277         0.234                                   
               Shimmer.APQ3   0.269         0.257  0.110                       0.111
               Shimmer.APQ5   0.272         0.261                                   
               Shimmer.APQ11  0.258         0.237  0.166  0.103                     
               Shimmer.DDA    0.269         0.257  0.110                       0.111
               NHR            0.257               -0.224 -0.131               -0.154
               HNR           -0.257               -0.144 -0.181                0.158
               RPDE           0.168        -0.166  0.271  0.205  0.148        -0.715
               DFA                   0.186 -0.345  0.273  0.471 -0.116 -0.217  0.523
               PPE            0.229        -0.279  0.125  0.110        -0.135       
               
                             Comp.9 Comp.10 Comp.11 Comp.12 Comp.13 Comp.14 Comp.15
               subject.       0.626                                                
               age            0.217                                                
               sex           -0.590                                 -0.101         
               test_time                                                           
               motor_UPDRS   -0.196                                  0.112   0.541 
               total_UPDRS   -0.114                                 -0.161  -0.561 
               Jitter...                                             0.171         
               Jitter.Abs.                  -0.227           0.472  -0.573  -0.151 
               Jitter.RAP           -0.123  -0.224                   0.158   0.183 
               Jitter.PPQ5                   0.304          -0.210   0.395  -0.416 
               Jitter.DDP           -0.123  -0.224                   0.158   0.183 
               Shimmer                                                             
               Shimmer.dB.                           0.116                         
               Shimmer.APQ3                 -0.316          -0.254  -0.100         
               Shimmer.APQ5                  0.119                          -0.228 
               Shimmer.APQ11                 0.241   0.315   0.625   0.283         
               Shimmer.DDA                  -0.316          -0.254  -0.100         
               NHR                           0.642          -0.169  -0.496   0.243 
               HNR            0.188 -0.168           0.848  -0.216  -0.119         
               RPDE          -0.233 -0.393           0.236  -0.126                 
               DFA           -0.173 -0.331   0.222          -0.109                 
               PPE           -0.147  0.792           0.235  -0.312                 
               
                              Comp.16 Comp.17 Comp.18 Comp.19 Comp.20 Comp.21 Comp.22
               subject.                                                             
               age                                                                  
               sex                                                                  
               test_time                                                            
               motor_UPDRS   -0.411                                                 
               total_UPDRS    0.404                                                 
               Jitter...              0.136  -0.136   0.849  -0.143                 
               Jitter.Abs.   -0.397                  -0.104                         
               Jitter.RAP     0.311           0.156  -0.206          -0.707         
               Jitter.PPQ5   -0.426          -0.224  -0.342                         
               Jitter.DDP     0.311           0.156  -0.206           0.707         
               Shimmer                0.243          -0.161  -0.858                 
               Shimmer.dB.            0.771   0.216           0.433                 
               Shimmer.APQ3          -0.186  -0.311           0.126          -0.707 
               Shimmer.APQ5  -0.149  -0.430   0.715   0.175   0.113                 
               Shimmer.APQ11  0.223  -0.165  -0.329                                 
               Shimmer.DDA           -0.186  -0.311           0.126           0.707 
               NHR            0.196  -0.120                                         
               HNR                                                                  
               RPDE                                                                 
               DFA                                                                  
               PPE

Below are our findins from Principal Componenets Analysis:

#### Covariance Matrix Interpretation:

All of the variables showcase small magnitudes which can have positive or negative linear releationships.

#### Correlation Matrix Interpretation:
From the correlation matrix we have the following observatins:
1.	Variable HNR which is the ratio of noise to tonal components in the voice. This variable has an inverse releationship with all the variables.
2.	Variables containing the word “Shimmer” have high positive correlation values with each other.
3.	Variables containing the word “Jitter” have high positive correlation values with each other
4.	High correlation values between variables containing the word Shimer with variables containing the word “Jitter”
5.	The PPE variable represents a nonlinear measure of fundamental frequency variation. This variable has strong positive correlations with varaibles containing the word “jitters” or “Shimmers” and the variable RPDE. RPDE represents a nonlinear dynamical complexity measure.
6.	“total_UPDRS” and “motor_UPDRS” showcase a strong positive correlation. Where, “total_UPDRS” represents clinician’s total UPDRS score and “motor_UPDRS” the clinician’s motor UPDRS score both, linearly interpolated.

#### PCA Interpretation:
1.	The amount of components was determined according to the following rule. The total amount of variation that the components represent must be within 70% to 90%.
2.	According to this parameter components 1 through 4 where selected. These components amount to a total of 76% of the total variation.

### Pros and Cons of the study:
1.	From our study on the dataset, we have come to the conclusion that age, sex, test-time and DFA are the variables that are most difficult to capture in a factor analysis model. Though we know from Random forest analysis and research papers that these variables are most significant in deciding the UPDRS score.
2.	In PCA, the age variable has high coefficient in component 7. But if we consider principal components with 1+ standard deviation, we have to consider the first 5 components, discarding the 7th component. Accordingly, test time and DFA has high coefficient in 6th and 8th component.
3.	The data has high correlation between the variable groups “Jitter” and “Shimmer” which caused problems related to multi-collinearity during the analysis.
4.	Future study on the parkinsons dataset should include more detailed analysis on the above mentioned variables with high-uniqueness and how to tackle the issue.






