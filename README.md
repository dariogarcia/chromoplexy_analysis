# Chromoplexy analyisis

In this repository we analyze data from 2800 patients with cancer. 
The main objective is to use genetic data to classify the cancer type of the patients. 
In order to do so we divide the process in several steps. 


Note: All the code shall run from src. 

### Step 1: Data processing

**input** 

- *allfiles*:A folder with one file per patient with the starting chromosome, the start of the break, 
the second chromosome and the end of the break. 
- *cancer_classification*: a file with the patient identifiers, the number of breaks per patient, 
if it has chromoplexy or not the number of chromoplexy events, the **cancer type** and the country. 


**output**

In this step we generate a graph per patient, in order to simplify the study. 

**files**
- loader
- graph_builder
- graphnx
- main_graph_printer

### Step 2: Graph analysis

**input**

**output**

**files**
- *main_gspan_subgraph_generator*: This file has the code to generate the gspan subgraphs. 
- *main_clique_analysis*: This code generates a graphs from the breaks data. Given a clique size, computes and stores the number of cliques, their chromosomic location, and their range within the chromosome, per patient.
- *main_freq_subgraph*:

### Step 3: Classification

**input**

**output**


#### TODO: 
- New structure to the code
- Add the weight to the vertex (done)
- Make the classification part 
- Find a chronotripsis criteria. 

#### Notas:
. Take care of overfitting. 