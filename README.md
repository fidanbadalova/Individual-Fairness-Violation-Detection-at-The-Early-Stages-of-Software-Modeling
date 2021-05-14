# IFVD, Individual Fairness Violation Detection at The  Early Stages of Software Modeling 
## Introduction
The main goal of the research project is to create a tool for analyzing individual fairness. The analysis of individual fairness is implemented by generating temporal logic formulas. Furthermore,another target of the work is to define the proxies for protected characteristics automatically. The tool consists of the following contributions:
1. Automatic approach for generating the proxies 
information of protected characteristics
2. Analysis the verification results of LTL formulas 
to detect violation of individual fairness 

**1. _Generating the proxies information of protected characteristics_** 

For calculation of correlation between protected 
characteristics and proxies we use two types of metrics.
*  **Conditionally Entropy.** It is a method for measuring uncertainty with a defined dataset.  
   
*  **Conditionally Probability.** It is defined as the probability of an event happening or occurring, while taking into consideration the likelihood of another event occurring.

To generalize the code, the _Calculation method_, _Threshold_, and _Protected data_ are read from the 
"input.txt" file. After calculation of correlation between protected characteristics and proxies, the result stored in the dictionary is compared with the threshold value in the input file. If it is lower than the threshold, the result of the calculation is a low correlation, if it is more, then it is a high correlation. The result of the high correlation is stored in the excel file. 


**2. _Verification results of LTL formulas_**

Verification results of the formulas are analyzed for detecting violations of individual fairness. The function for detecting of individual fairness uses a set of generated batches of LTL formulas with named "ltlFormulas.xlsx" input file. . The result should be satisfied one of the following cases:
* If the formulas of one of the pairs in each
presented batch are fulfilled
* If all formulas of each presented batch are 
fulfilled.

The verification results of LTL formulas is displayed as "Result.html". 



## How to run
**First step** of the work is to run "calculationCorrelation.ipynb" file. For it we use 2 input files: _personalData.xlsx_ and _input.txt_. The excell file is consist of real statistic data and the input file is for defining _Calculation method_, _Threshold_, and _Protected data_. 

If the metric is defined as "conditionalEntropy" in the input file, the _conditionalEntropy_ function is called to calculate the correlation between the protected data and proxies from dataset, if the metric is defined as "conditionalProbability", then _conditionalProbability_ function is called. 

Regarding _Conditional Entropy_ formula, first of all functions such as **entropy**, **jEntropy**, **cEntropy** are defined to calculate _Entropy_, _Combined Entropy_ and _Conditional Entropy_ for the given variables. In the **conditionalEntropy** function, the protected and proxies are taken and these parameters are sent to the above mentioned **cEntropy** function to define the conditional entropy. Correlation between protected data and proxies is merely low after the result of calculation for conditional entropy compared with the threshold. 

_Conditional Probability_ is used for obtaining decent result for given dataset. After retrieving the protected data and threshold value from the input file, the data not in the "protected data" list is selected. Using this data, the count of each value of each column 
is calculated, and the result is divided by the number of 
all the values in each column. The result stored in the dictionary is compared with the threshold value in the input file. 

**Second step** of the work is to run "verificationLTLFormulas.ipynb" file. For it we use input file: _ltlFormulas.xlsx_. The **createDictionaries** function select the result of the LTL formulas and stored in dictionary for each batch and pair. Using stored data we can get the result of LTL formulas for obtaining decision about individual fairness. 