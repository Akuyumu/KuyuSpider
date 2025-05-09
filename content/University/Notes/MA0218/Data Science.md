---
tags:
  - y2s2-MA0218
status: Completed
---
## Data Analytic and Pipeline
---
### **What is Data Science?**
==Pipeline==
- ==Sample Collection==
    - Effectively sample real-world data
- ==Practical Motivation==
    - Identify and frame as a data science problem
- ==Data Preparation==
    - How to prepare raw data for analysis?
    - Data cleaning
- ==Problem Formulation==
    - How to construct the problem intelligently?
- ==Exploratory Analysis==
    - How to gain insights from data?
- ==Statistical Description==
    - How to represent the data numerically?
- ==Analytical Visualization==
    - How to present data meaningfully to humans?
- ==Pattern Recognition==
    - Identify structures and find intrinsic insights from data
- ==Algorithmic Optimization==
    - Developing effective learning algorithms
- ==Machine Learning==
    - How to learn patterns from data?
    - Training a model
- ==Information Presentation==
    - Communicate data analysis effectively
- ==Statistical Inference==
    - How to draw confident conclusions from data?
- ==Ethical Consideration==
    - Does the data analysis conform to ethical values?
- ==Intelligent Decision==
    
    - Solving real-world problems with results
    
      
    
---
### **Data Types**
**Structured Data**
- Numeric Data
    
    ![[image.png]]
    
- Categorical Data
    
    ![[image 1.png]]
    
- Mixed Data
    
    Numeric and Categorical
    
- Time series Data
    
    ![[image 2.png]]
    
- Network Data
    
    Nodes and Connections
    
    ![[image 3.png]]
    
**Unstructured Data**
- Text Data
- Image Data
- Video Data
- Voice Data
---
  
### **Data Science Problems & Solutions**
- Prediction: Numeric
    - How Much? How Many
    - is it profitable to make a sequel?
**Solution: Regression**
$$Model: Sales = f(variables)$$
Linear regression models | Tree Models for Regression | Neural network for Regression
---
- Prediction: Class
    - Type A or Type B
    - Probability of admitting to NTU?
**Solution: Classification**
$$Model: p(admit) = f(Variable)$$
Logistic regression | Tree Model for Classification | Neural Network for Classification
---
- Detection: Structure
    - How is this organised?
**Solution: Clustering**
Identifying groups of data points close together, and far from other groups, Without categories or labelling
k-Means Algorithm for clustering | Hierarchical Model for Clustering
---
- Detection: Anomaly
    - weird behaviours
    - is the engine safe to operate?
**Solution: Anomaly detection**
Cluster-Analysis based Detection | Nearest Neighbour Detection Model | Support Vector based Detection
---
- Decision: Action
    - what should be done next?
    - which action will be rewarded?
**Solution: Adaptive learning**
Model a Profit/Loss Function
$$Optimize - f(State,variable)$$
Reinforcement learning Approach | Monte-Carlo, State-Action-Reward | Q-learning, Deep Reinforcement
---
  
## Basic Statistics & Data Analysis
---
### Uni-Variate Statistics
Data Available: Average Value | Deviation from Average | Maximum and Minimum
- Central Tendencies (Mean)
    
    Sum of data / Count of data
    
    $$\bar x = \frac {x_1 +x_2+...+x_n} {n}$$
    
- Dispersion: Standard Deviation
    
    sum of deviation / count of data
    
    $$\sqrt {\frac{(x_1 - \bar x)^2 +(x_2 - \bar x)^2 + ...+(x_n - \bar x)^2}{n}}$$
    
- Central Tendencies (Median)
    
    $$N(x \le x_m) = N(x\ge x_m) = 0.5$$
    
- Dispersion: Quantiles
    
    Markers to divide the data 25:50:25
    
    $$N(x\le x_{q1}) = 0.25, N(x\ge x_{q2}) = 0.25,$$
    
---
### Uni-Variate Visualisation
Exploratory Analysis
- Box-Plot
    
    Inter-Quartile range (IQR) - between 25% and 75%
    
    Upper Whisker = 75% + IQR x 1.5
    
    Lower Whisker = 25% - IQR x 1.5
    
    ![[image 4.png]]
    
- Histogram
    
    ![[image 5.png]]
    
    ![[image 6.png]]
    
- Density Plot
    
    ![[image 7.png]]
    
- Violin Plot
    
    ![[image 8.png]]
    
---
  
### Bi-Variate Exploration
- Bi-Variate Joint plot
    
    ![[image 9.png]]
    
- Correlation Coefficient
    
    **Co-Variance / St. Dev Product**
    
    $$\frac {\sum_{}{(x_i - \bar x)(y_i - \bar y)}}{\sqrt{\sum_{}{(x_i - \bar x)^2}}\sqrt{\sum_{}{(y_i - \bar y)^2}}}$$
    
    No dependence - Corr = 0
    
    Perfect positive - Corr = 1
    
    Perfect negative = Corr = -1
    
- Correlation Matrix & Plot
    
    ![[image 10.png]]
    
---
### Multi-Variate Exploration
- Mutual Correlation and Plots
    
    ![[image 11.png]]
    
    ![[image 12.png]]
    
- Multi-Variate Pair Plot
    
    Basically mega joint plots
    
    ![[image 13.png]]
    
---
  
## Linear regression
---
### Machine learning
Building a prediction model
- Given - Variables
- Learn - Model for desired value
- Predict - Desired value for others
- Supervised Learning
    
    Regression | Classification
    
      
    
- Unsupervised Learning
    
    Clustering | Anomaly Detection
    
---
  
  
### Uni-Variate Linear Regression
Split the data set into:
- (Train) - to train the model
- (Test) - to test the model
Using (Train):
- Hypothesize a Linear model - Y = mX + C
- Algorithmic Optimization
    
    Minimise Cost Function to attain linear model (Best fit line)
    
    $$J(a,b) = \sum (y - \hat y)^2$$
    
- Goodness of Fit of Model
    
    Higher Explained Variance $R^2$ the better the model
    
    ==R^2 = 0 does not mean all predictions are incorrect==
    
    $$R^2= 1 - \frac { \sum (y-\hat y)^2}{\sum (y - \bar y)^2}$$
    
    Lower Mean Squared Error the better the model
    
    $$MSE = \frac{1}{n} \sum (y - \hat y)^2$$
    
    ---
    
## Decision Tree & Classification
---
### Binary Classification
Prediction of Class with an Independent variable
- Box and Swarm plot
    
    ![[image 14.png]]
    
- Decision tree algorithm
    
    - It repeatedly splits the dataset into subsets based on the feature  
        that minimizes impurity until it reaches a stopping criterion  
        
    - Leaf nodes: Final nodes in the decision tree
    - Setting a maximum depth helps prevent the tree from becoming  
        too complex and overfitting  
        
    
    ![[image 15.png]]
    
Consecutive binary decision are made based on **Gini Index - Measurement of impurity**
$$gini = \sum \frac {x_i}{n} (1- \frac {x_i}{n})$$
$$gini = 1-((\frac{x_1}{n})^2 +(\frac{x_2}{n})^2 +...)$$
- Confusion Matrix
    
    FN: False negative - true predict as false
    
    FP: False positive - false predict as true
    
    ![[image 16.png]]
    
Recall = True positive rate
Precision = Positive Prediction Accuracy
---
## Clustering
---
### Clustering Patterns
- K-Means Clustering Algorithm
    - To minimize the sum of squared distances between data points and their assigned cluster centroids
    - Parameter: Choose K - potential number of clusters
        - Poorly chosen K means non-meaningful clusters
    - Initialisation: Choose K cluster centroids from the dataset
    - Iteration:
        - for each point in the data set - Re-label according to nearest centroid
        - for each cluster of data points - Re-compute centroid of cluster
### Anomaly Detection
- Local Outlier Factor (LOF)
    - It compares the local density of a point with that of its neighbours to detect anomalies
    - High LOF - point density is smaller compared to neighbours
    - Parameter
        - Choose K - number of neighbours to “scan” for
    - Iteration - for each point in data set
        - find the K nearest neighbour in data (scan)
        - compute the local density by comparing distance between point and neighbours
- Visuals
- Computation:
    
    Reachability distance (RD) - distance between point and neighbour
    
    Local Reachability Density (LRD):
    
    $$LRD=\frac {1} {\sum RD(A,X)/k}$$
    
    LOF score:
    
    $$LOF = \frac {\sum LRD(X)/k}{LRD(A)}$$
    
---
## Visualisation and Presentation
---
To communicate complex data insights in a clear and effective manner
- Visualisation elements ranking (Accurate - Generic)
    
    Length (Aligned) | Length | Slope & Angles | Area and Colour Intensity | Volume | Colour hue
    
- Data Ink VS Non-data Ink
    - “Ink” that presents actual useful data VS “Ink” for aesthetics and formatting
    - Ratio should be as high as possible