## Tabular Data Preprocessing for Sequential Machine Learning Models

This repo contains the preprocessing steps and scripts to take business data to machine learning model ready time series and other sequential formats.

### Why Organize

We organized this pre-processing into three sequential functional steps with an associated script for each.  We organize these scripts separately so that we can deploy each script in turn in operation into SQL, while leaving us flexibility to iterate those remaining as we mature our understanding and approach to the model which allows us to speed our collaboration in the later scripts.

### Pre-processing Notebooks

The first is ‘filtering and formatting’ from the source tables of interest. This reduces the data bulk for our design phase. The second script performs ‘joins, folds and conversions’. It joins our tables of interest, folds the data (sequentially or in aggregate) into our final timestep of interest for our sequential models, and generates meaningful numeric values from non-numeric information. The third script performs feature engineering. In this script we engineered additional features and augmented the data in order to provide our models with more signal. We iterate on this script as we refine the model.
To illustrate we highlight just the time series pre-processing and not the text pre-pro cessing. This github repo describes the preprocessing in more detail with more extensive information.

a.)     **Filtering and Formatting**: The goal of this step is to reduce the size of the data passed along to subsequent steps and to do rudimentary formatting and cleaning (e.g. replace missing values and convert datatypes). For example, we selected columns of interest and filtered to eliminate account types that are not in our consideration set. We also limit the history for each account that we bring forward for sampling, reducing the size of the transaction table substantially. With the size of the data reduced, the time required to design the subsequent steps is much less. 

b.)     **Joins, Folds and Conversions**: After filtering the source data, the data are joined to form two single data frames. The goal of this step is to get close to having the data in the functional model-ready numerical form, but before much augmentation.  This simplifies the later augmentation work.

We chose the daily timestep to model on. Where the data were more frequent than daily, we ‘folded’ the data – that is, we generated aggregates, concatenations and other descriptive statistics of the information within that day.  In this iteration, we preserved detail of the last five events that day which captured the lion's share of the multiple events per day sample.  We chose aggregations that expressed the maximums and totals for within day events by type.  We also generated conversions of datetime variables, representing them as count-of-day differences (e.g., days since last activity). 

c.)     **Feature engineering**: Within the feature engineering step, we removed the predictive period – in our case 14 days – added derivative features, wrote out the final labels, and added new engineered or augmented features to the array or data frame.
