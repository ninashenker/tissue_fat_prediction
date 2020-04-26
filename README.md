# Tissue Fat Prediction

Code can be found at GTex under RNASeq Data

## Project Description
We chose to tackle the metabolic-disorders challenge.  Our project aims to understand the relationship between gene expression and fat accumulation in the pancreas and liver.

#### Method
We framed the problem as a supervised learning regression task. Given features
containing: 
* Age
* Sex
* Hardy death scale,
* Normalized gene counts (TPM) for liver and pancreas samples

We predict Y: 
* Liver fat (%)
* Pancreas fat (%)

##### Dataset
We split the dataset into a train/val/test partition using sizes 85/10/5 % respectively. There is only 93 total patient records so the validation and test sets are at risk of not representing all feature classes. To address this we use stratified sampling to proportionally sample minority classes in each set.

All data was cleaned (remove duplicates, merge, format) and standardized before training. 

##### Models
We experimented with the following models and got the following MSEs for Pancreas fat percentage (please see slides for more results).
* Linear Regression: 0.1913
* ElasticNet: 0.2304
* Polynomial SVR: 0.0173
* Random Forest: 0.0094
* K-nearest neighbors: **0.0074**
* Gaussian Process: 0.0210

We further analyzed the best model: KNN. Analyzing prediction plots, we found that the classifications of the fat percentages (e.g. high/low) were predicted accuracy, however, the specific regression values within that classification aren't as accurate.

##### Gene importance analysis
To understand which gene expressions contribute the most to the prediction of fat percentage, we applied a feature analysis on the RandomForest tree splits. We found that the following gene IDs contribute most to predicting fat percentage:
* "ENSG000000274372.4"  for liver
* and "ENSG00000074317.10" for pancreas

Please see slides for full gene importance plots. 

#### Future Direction
* More research is needed to understand the important gene features and why they provide so much predictive power for fat tissue.
* We believe there's room to leverage unsupervised pretraining on unlabeled gene samples (found in GTEx) to learn richer feature representations for gene expressions. This would be particularly useful considering the low number of labeled fat samples in the dataset.

##### Conclusion
* We built a model to predict fat tissue from gene counts and subject metadata
* K Nearest Neighbors showed the best prediction accuracy particularly in
regards to high/low fat classification
* Feature importance analysis suggests that gene ID “ ENSG000000274372.4”
for liver and gene ID “ENSG00000074317.10” for pancreas are the most
important features for predicting fat tissue. 


# License
MIT License
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions: The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software. THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.