# Network Intrusion Detection System (NIDS) using Random Forest and NSL-KDD

## Project Overview

This project implements a Machine Learning-based Network Intrusion Detection System (NIDS) capable of identifying malicious network activity from normal network traffic.

The system analyzes network connection records and learns patterns that distinguish legitimate behavior from cyber attacks. Using the NSL-KDD dataset and a Random Forest classifier, the model predicts whether a network connection is normal or malicious.

The goal is not only to achieve high prediction performance but also to understand:

* How network intrusion detection works
* How cybersecurity datasets are structured
* How machine learning can assist security analysts
* Which network behaviors are most indicative of attacks

---

# What is a Network Intrusion Detection System?

A Network Intrusion Detection System (NIDS) continuously monitors network traffic and attempts to identify suspicious or malicious activity.

Think of it as a security guard for a computer network.

Normal users generate legitimate traffic:

* Browsing websites
* Sending emails
* Accessing databases
* Using cloud services

Attackers generate abnormal traffic:

* Password attacks
* Port scanning
* Denial-of-Service attacks
* Privilege escalation attempts

A NIDS analyzes network connections and answers:

"Is this connection normal or suspicious?"

---

# Why Do Companies Use NIDS?

Organizations use intrusion detection systems because modern networks generate massive amounts of traffic that cannot be monitored manually.

Benefits include:

* Early attack detection
* Continuous network monitoring
* Faster incident response
* Protection of critical infrastructure
* Detection of unauthorized access attempts
* Security visibility across large networks

Without intrusion detection, attacks may remain unnoticed for weeks or months.

---

# Understanding Attack Categories

The NSL-KDD dataset contains many individual attack names. For practical machine learning, these attacks are grouped into major categories.

---

## 1. Normal Traffic

Legitimate network activity.

Examples:

* Web browsing
* Video calls
* Email communication
* Database access

These connections represent expected user behavior.

---

## 2. DoS (Denial of Service)

Goal:

Prevent legitimate users from accessing a service.

Examples:

* neptune
* smurf
* teardrop
* back

Attackers flood a system with excessive requests until resources become unavailable.

Real-world analogy:

Thousands of fake customers entering a restaurant and occupying all seats so real customers cannot enter.

---

## 3. Probe

Goal:

Gather information about a target before launching an attack.

Examples:

* satan
* ipsweep
* portsweep
* nmap

Activities include:

* Port scanning
* Host discovery
* Vulnerability scanning

Real-world analogy:

A burglar checking every door and window before attempting a break-in.

---

## 4. R2L (Remote to Local)

Goal:

Gain local access from outside the network.

Examples:

* guess_passwd
* ftp_write
* warezclient

The attacker initially has no access and attempts to enter the system.

Real-world analogy:

Someone outside a building repeatedly trying different keys until one works.

---

## 5. U2R (User to Root)

Goal:

Escalate privileges after already obtaining access.

Examples:

* buffer_overflow
* rootkit
* loadmodule

The attacker starts as a normal user and attempts to gain administrator privileges.

Real-world analogy:

A visitor obtaining the master key that opens every room in a building.

---

# Machine Learning Problem Definition

## Learning Category

Supervised Learning

The dataset already contains correct labels indicating whether traffic is normal or malicious.

The model learns from these labeled examples.

---

## Task Type

Classification

The objective is to predict the category of each network connection.

### Binary Classification

Classes:

* Normal
* Attack

This is the initial implementation.

---

### Multi-Class Classification (Future Extension)

Classes:

* Normal
* DoS
* Probe
* R2L
* U2R

This provides more detailed attack categorization.

---

# Why Random Forest?

Random Forest was selected because it performs exceptionally well on structured tabular datasets.

Advantages:

* Strong classification performance
* Resistant to overfitting
* Handles nonlinear relationships
* Works well with mixed feature types
* Provides feature importance analysis
* Requires relatively little tuning

Random Forest operates by combining many Decision Trees and using majority voting for predictions.

---

# Dataset

## NSL-KDD Dataset

This project uses the NSL-KDD dataset, an improved version of the older KDD Cup 1999 dataset.

Advantages:

* Reduced duplicate records
* Less dataset bias
* Widely used in intrusion detection research
* Suitable for learning and experimentation

---

# Dataset Structure

Each network connection contains:

### Categorical Features

* protocol_type
* service
* flag

Examples:

protocol_type:

* TCP
* UDP
* ICMP

---

### Numerical Features

Examples:

* duration
* src_bytes
* dst_bytes
* wrong_fragment
* num_failed_logins
* count
* srv_count

These describe connection behavior and traffic statistics.

---

### Target Label

Indicates whether the connection is:

* Normal
* Attack Type

---

# Data Preprocessing Pipeline

Raw cybersecurity data cannot be used directly.

The preprocessing pipeline includes:

## Data Cleaning

* Remove invalid records
* Verify feature consistency
* Handle missing values

---

## Feature Encoding

Categorical values cannot be processed directly by machine learning algorithms.

Examples:

TCP
UDP
ICMP

These are converted using One-Hot Encoding.

---

## Feature Scaling

Numerical features may have very different ranges.

Examples:

duration = 2

src_bytes = 50000

Scaling helps create a more balanced feature representation.

---

# Exploratory Data Analysis (EDA)

Before training the model, the dataset must be understood.

Analysis includes:

* Class distribution
* Attack frequencies
* Feature distributions
* Correlation analysis
* Outlier investigation

Questions explored:

* Which attacks are most common?
* Which features differ most between normal and malicious traffic?
* Is the dataset imbalanced?

---

# Class Imbalance Problem

Cybersecurity datasets are rarely balanced.

Example:

90% Normal

10% Attack

A model could achieve high accuracy simply by predicting everything as normal.

Potential solutions:

* SMOTE
* Undersampling
* Class weighting

---

# Model Training

Primary model:

RandomForestClassifier

Important hyperparameters:

* n_estimators
* max_depth
* min_samples_split
* min_samples_leaf

The dataset is divided into:

* Training Set
* Testing Set

The model learns from training data and is evaluated on unseen testing data.

---

# Model Evaluation

Accuracy alone is not sufficient for cybersecurity applications.

Important metrics:

## Precision

Among all predicted attacks:

How many were actually attacks?

---

## Recall

Among all real attacks:

How many were detected?

This is the most important metric because undetected attacks are dangerous.

---

## F1 Score

Balances Precision and Recall.

---

## Confusion Matrix

Shows:

* True Positives
* False Positives
* True Negatives
* False Negatives

Provides detailed insight into model behavior.

---

## ROC-AUC

Measures the model's ability to distinguish between classes across different thresholds.

---

# Feature Importance Analysis

One of the biggest advantages of Random Forest is interpretability.

The model can reveal:

* Which features contribute most to predictions
* Which traffic patterns indicate attacks
* Which network behaviors are most suspicious

This helps transform the project from a black-box predictor into an explainable cybersecurity system.

---

# Project Workflow

NSL-KDD Dataset

↓

Data Cleaning

↓

Feature Engineering

↓

EDA

↓

Train/Test Split

↓

Random Forest Training

↓

Model Evaluation

↓

Feature Importance Analysis

↓

Future Enhancements

---

# Future Enhancements

## Multi-Class Attack Classification

Classify specific attack categories instead of simply normal vs attack.

---

## Advanced Models

Compare Random Forest with:

* XGBoost
* LightGBM
* SVM

---

## Hyperparameter Optimization

Use:

* GridSearchCV
* RandomizedSearchCV

---

## Anomaly Detection

Explore:

* Isolation Forest
* One-Class SVM

for detecting previously unseen attacks.

---

## Real-Time Dashboard

Develop a dashboard using:

* Streamlit
* Flask

for interactive monitoring and prediction.


---

# Tech Stack

Language:

* Python

Libraries:

* pandas
* numpy
* scikit-learn
* matplotlib
* seaborn
* imbalanced-learn

Optional:

* streamlit
* xgboost

---

# Key Project Goal

The objective is not merely to achieve high accuracy.

The goal is to build a reliable and interpretable intrusion detection system capable of identifying malicious network activity while understanding the reasoning behind its predictions.

A successful project should answer:

"Can machine learning effectively distinguish normal network behavior from cyber attacks, and what network features are most useful for making that decision?"

