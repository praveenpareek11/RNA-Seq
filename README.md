# RNA-Seq
Analysis of RNA-Seq data using PCA and GSVA

**This was given as an assignment to me from Elucidata (India)**

## Introduction
Pancreatic Adenocarcinoma (PAAD) is the third most common cause of death from cancer, with an overall 5-year survival rate of less than 5%, and is predicted to become the second leading cause of cancer mortality in the United States by 2030.

Ribonucleic acid (​ RNA​ ) is a polymeric molecule essential in various biological roles in coding, decoding, regulation and expression of genes.

RNA-Seq (RNA sequencing), is a sequencing technique to detect the quantity of RNA in a biological sample at a given moment. Here we have a dataset of normalized RNA Sequencing reads for pancreatic cancer tumors​ . The measurement consists of ~20,000 genes for 185 pancreatic cancer tumors. The file format is ​ GCT , a tab-delimited file used for sharing gene expression data and metadata (details for each sample) for samples.

The GCT file is like multi-dimensional DataFrame, which consists of 3 DataFrames combined in 2-D.

These are:

- **data_df:** It has 18465 rows (Gene ID) abd 183 columns (Sample Name/ID)
- **row_metadata_df:** It has row metadata and When we see the type, It is empty dataframe. This means in our data, the row metadata is not present.
- **col_metadata_df:** It has 183 columns (Sample Names/ID) and 124 rows (Column metadata like histological_type, Patient_ID, status(is he alive or not)) for each sample.

### **Data cleaning and check the distribution of gene expression across samples**
Out of 18465 rows, 4367 rows had NULL values at some of the columns. So I removed them in data cleaning process.
So after data cleaning 14098 rows are there and 183 columns.
These 14098 rows represent Gene ID, and 183 columns represent 183 different samples.

### **Generation of gene expression distribution for all samples:**
Here we plot the expression (numerical value which ranges from 0 to 15, e.g. 7.5 or 11.2 etc.) Points for understanding graph:

- x-axis of heatmap graph has sample names
- y-axis of heatmap graph has the gene id
- The colour signifies the value of gene expression corresponding to each sample. So the colour bar on the right, helps us to get the insight into the distribution of gene expression as the values are encoded via colour.

### Visualization of all the data using Phantasus tool online.

![data_gene](https://user-images.githubusercontent.com/36000962/75327868-17c63280-58a3-11ea-87b1-2d9e1b5ddfcf.png)

### Image of the all sample gene distribution

![gene_distribution](https://user-images.githubusercontent.com/36000962/75326736-2875a900-58a1-11ea-9354-4d566826fdda.png)


### Identify only the ​ Exocrine​ (adenocarcinoma) tumors and remove ​ Neuroendocrine​ tumors.

#### Preparing the data for PCA:
Using PCA result for plotting the data.

We already know that the data is for two broad categories of Pancreatic Cancer:
- Exocrine
- Neuroendocrine
So based on that, there will be 2 different clusters of data points.

Here I used the 'histological_type_other' data to seperate the two type of cancers.

### Image of PCA plot:
![pca_plot](https://user-images.githubusercontent.com/36000962/75601309-d1114c00-5adf-11ea-90bc-9e5019b39346.png)


We can see that most of the points are concentrated in the particular range of PC1 and PC2 values. So we can separate the samples from Neuroendocrine and Exocrine. The outliers are -100 > PC1 and PC1 > 100 . I choose this range as it is PC1 and more prominant feature. and other constraint is PC2 < 50. It will provide us to clearly seperate the outliers. So in next step, We'll remove the outlier samples from the dataframe.


### Understand the effect of Interferons in Pancreatic Adenocarcinoma:

Interferons (IFNs) are a group of signaling proteins made and released by host cells in response to
the presence of several pathogens, such as viruses, bacteria, parasites, and also tumor cells. Type I
interferons (IFNs) are a large subgroup of interferon proteins that help regulate the activity of the
immune system. The genes responsible for type 1 Interferons is called ​ Type 1 IFN signature and
consists of a set of 25 genes in homo sapiens.


Now, we know the samples, which fall in category of Pancreatic Adenocarcinoma, and we also know the genes responsible for type1 interferons (Type 1 IFN Signature).
These genes are a set of 25 genes in homosapians.
So To plot the gene expression, for pancreatic adenocarcinoma, We'll create a dataframe with these 25 genes as rows and the Sample name (Which is the index of the pp dataframe.) as columns.


### Image of the Type 1 IFN genes (25 genes) --> it's distribution across samples of Exocrine.

![gene_25](https://user-images.githubusercontent.com/36000962/75326741-2b709980-58a1-11ea-9891-5ef9725f59dc.png)
