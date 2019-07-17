# RNA-Seq_pipe

This repository stores all the R and bash files that are used to run a RNA-Seq analysis.

## Downloading tools 
Some tools need to be downloaded and compiled in order to run the pipeline available. Here is the list of the tools to be downloaded: 
* STAR: https://github.com/alexdobin/STAR
* Trimmomatic: http://www.usadellab.org/cms/?page=trimmomatic
* FastQC: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/
* featureCounts: http://bioinf.wehi.edu.au/featureCounts/

Tools must be downloaded following the instructions on the websites. The resulting folders and binary executable files must be saved in a _scripts_ folder. 
## RNA-Seq pipeline
On the _RNA-Seq_ folder, you will find the necessary tools to run a RNA-Seq pipeline on your terminal in a Unix environment. Several folder are located within it: 
* data: _fasta_, _gff_ and a subfolder _subdata_ must be added in this folder. 

   * subdata: _fastq_ files are included in this folder. 
   
* scripts: all the scripts and tools needed to run the _RNA-Seq_ analysis are found here. 

A folder _bin_ must be created where all the results will be stored. 
The user must follow the following steps before running the analysis 
```bash 
git clone https://github.com/jumagari14/RNA-Seq_pipe.git
cd RNA-Seq_pipe
mkdir -p -m 755 bin data
mkdir -p -m 755 data/subdata
## Include all the necessary data in data and subdata folder
cd scripts 
```
Once these steps are done, a _shell_ file can be executed 
```bash
./main_rna_seq.sh 
```

After running the pipeline, several folders are found in _bin_: 
* genome_ind: Genome indexes, necessary to run the STAR mapping. 
* STAR_Align: Sorted and unsorted _Bam_ files from STAR mapping.
* counts: _txt_ files with the counting results. 
* trimm_data: trimmed _fastq_ reads. A subfolder _quality_ where _html_ and _zip_ files as a result of _FASTQC_ analysis are stored is also generated. 

In the main directory, a file _.tabular_ where all the counting results are saved is created. This file will mainly be used in the latter normalisation step.  

The main script includes _parallel_ command. If this command is not available on the cluster where the analysis is run, the optional script (optional_rna-star.sh) must be run. 
In the current repository, R files to perform the normalisation analysis and to extract extra information about _gff_ files are included. 