# Chromoplexy analyisis

In this repository we analyze data from 2800 patients with cancer. 
The main objective is to use genetic data to classify the cancer histology of the patients. 
In order to do so we divide the process in several steps. 

### Step 1: Data processing

**input:** 

- *data/raw_original_data/allfiles*:A folder with one file per patient with the starting chromosome, the start of the break, 
the second chromosome and the end of the break. 
- *data/raw\_original\_data/cancer\_classification.txt*: a file with the patient identifiers, the number of breaks per patient, 
if it has chromoplexy or not, the number of chromoplexy events, the **cancer type** and the country. 
- *data/raw_original_data/metadatos_v2.0.2.txt*: a file with the patient identifiers, the number of breaks per patient, 
if it has chromoplexy or not, the number of chromoplexy events, the **cancer type** and the country. 


**output:**

In this step we generate a graph per patient, in order to simplify the study. 

**files**
- loader
- graph_builder
- graphnx
- main\_graph_printer
### Matadata study (Previous to step 2)

In this step we clean the given metadata in order to work more eficiently in the next step. 


**output:**
- *data/raw_original_data/clean_metadata.csv*: a file with the patient identifiers,the patient sex, the patient age, and the two histologies of the cancer. 


### Step 2: Graph analysis

In this step we use the gspan implementation from [https://github.com/Jokeren/DataMining-gSpan]

**Input**
- *data/raw_original_data/allfiles*:A folder with one file per patient with the starting chromosome, the start of the break, 
the second chromosome and the end of the break. 
- *data/raw_original_data/clean_metadata.csv*: a file with the patient identifiers,the patient sex, the patient age, and the two histologies of the cancer. 

**Output**
- *data/datasets/classification_dataset_[number of patients]_[support of the graphs]_[max distance].csv*
- some auxiliar files. 

**Process**

The main code for generate the csv is on _src/step2/dataset\_generation.py_. 

```
python2 dataset_generation.py
```

In this file we process all the raw files of the patients as follows:
1. Fill in the Data class:
For every patient: 
	1. We generate a gspan compatible graph with *generate_one_patient_graph* of *src/step2/main_gspan_subgraph_generator.py*
 		This file is saved on _data/all_files_gspan_[max distance]_
	2. We generate the patient subgraphs using gspan, called from _generate\_subgraphs_ of  _src/step2/dataset\_generation.py_. 
	3. We save this subgraphs on the Data class.
2. When de Data class is filled with all the patients we save ir as a pkl. This processs is SLOW, VERY SLOW. This way we avoid doing it every time. 

3. We generate the csv ussing the data generated on previous step and some features extracted from the original patient break files. 


**Optional**.

 Run *main_freq_subgraph* over the file generated by gspan code. 
This code will generate a pdf with all the subgraphs found by gspan. 

```
python step2/main_freq_subgraph_plotter.py '../data/results/gspan_output.txt'
```

**Files**
- *main_gspan_subgraph_generator*: This file has the code to generate the gspan subgraphs. 
- *main_freq_subgraph*: Generates a pdf with all the subgraphs found by gspan. 
- *main_clique_analysis*: This code generates a graphs from the breaks data. Given a clique size, computes and stores the number of cliques, their chromosomic location, and their range within the chromosome, per patient.
- *dataset_generation*: This code generates a csv for classification from the original data.

### Step 3: Classification

**input**

**output**


### TODO: 
- New structure to the code (done)
- Add the weight to the vertex (done)
- Make the classification part (in process)
- New code for subgraph feature extraction: 
    For every patient: 
        1. Gets the patient graph and plots it.  
        2. Gets the all the subgraph patterns of this graph. 
        3. Generates the sample in terms of subgraphs of this patient. 
            (dict\[sub_graph\] = number of sub_graphs of this type)
        4. Add to the general list the new subgraphs. 
    Generates a list of the most common patterns for all the patients. (done)

- Find a way to codify the patterns in order to use them as features.(done)
- Add to the graphs the edge weight as the number of repeated edges over the selected two vertex.(done)
- Find a chronotripsis criteria. 
- Make some histograms of the weights of the vertex depending on the max_distance given. (done)
- Study the concept of chromotripsis and find a way to relate it with the max distance. 

#### Notas:
- Take care of overfitting. 
- All the code shall run from src. 