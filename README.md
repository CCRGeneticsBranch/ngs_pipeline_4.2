

## Introduction
This is the implementation of [KhanLab](https://ccr.cancer.gov/Genetics-Branch/javed-khan) NGS Pipeline using Snakemake.
## Installation


This pipeline is available on NIH biowulf cluster. The data from this pipeline could directly be ported in [OncoGenomics-DB](https://clinomics.ncifcrf.gov/production/public/), an application created to visualize NGS data available to NIH users.
## Requirements
[mutt](http://www.mutt.org/)  
[gnu parallel](http://www.gnu.org/software/parallel/)  
SLURM or PBS for resource management  
Bioinformatics Tools Listed in [config files](config/config_common.json)  
### Following R Packages
- [OmicCircos](https://www.bioconductor.org/packages/release/bioc/html/OmicCircos.html)
- [RColorBrewer](https://cran.r-project.org/web/packages/RColorBrewer/index.html)
- [Rsubread](https://bioconductor.org/packages/release/bioc/html/Rsubread.html)
- [edgeR](http://bioconductor.org/packages/release/bioc/html/edgeR.html)
- [limma](http://bioconductor.org/packages/release/bioc/html/limma.html)
- [optparse](https://cran.r-project.org/web/packages/optparse/index.html)
- [pracma](https://cran.r-project.org/web/packages/pracma/index.html)
- [sequenza](https://cran.r-project.org/web/packages/sequenza/index.html)
- [stats](https://stat.ethz.ch/R-manual/R-devel/library/stats/html/00Index.html)
- [stringr](https://cran.r-project.org/web/packages/stringr/vignettes/stringr.html) 
- [deconstructSigs](https://github.com/raerose01/deconstructSigs)  

## Conventions

- Sample names cannot have "/" or "." in them
- Fastq files end in ".fastq.gz"
- Fastq files are stored in DATA_DIR (Set as Environment Variable) 

### DNASeq:
- QC
- BWA, Novoalign  
- Broad Standard Practices on bwa bam  
- Haplotype Caller, Platupys, Bam2MPG, MuTect, Strelka  
- snpEff, Annovar, SIFT, pph2, Custom Annotation  
- Coverage Plot, Circos Plot, Hotspot Coverage Box Plot  
- Create input format for oncogenomics database (Patient Level)  
- Make Actionable Classification for Germline and Somatic Mutations   
- Copy number based on the simple T/N LogRatio (N cov >=30), Corrected for Total # Reads  
- Copy number, tumor purity using sequenza   
- LRR adjusted to center  
- Contamination using [conpair](https://github.com/nygenome/Conpair)  
- HLA Typing  
	* [HLAminer](www.bcgsc.ca/platform/bioinfo/software/hlaminer) v1.3.1   
	* [seq2HLA](https://bitbucket.org/sebastian_boegel/seq2hla)  
- Neoantigen Prediction 
	* [pVAC-Seq](http://pvac-seq.readthedocs.io/en/latest/) 
		methods: NNalign,NetMHC,NetMHCIIpan,NetMHCcons,NetMHCpan,PickPocket,SMM,SMMPMBEC,SMMalign  
		epitope length: 8,9,10,11



### RNASeq:
- 
- Mapping - STAR
- Variant analysis - GATK
- Fusion calling - fusion-catcher, Arriba, STAR-fusion
- Gene expression - RSEM
- Haplotype Caller
- snpEff, Annovar, SIFT, pph2, Custom Annotation
- Actionable Fusion classification

### Patient:
- Genotyping On Patient. 
	1000g sites are evaluated for every library and then compared (all vs all)
	If two libraries come from a patient the match should be pretty good >80%
- Still to develop:
	If the match is below a certain threshold, break the pipeline for patient.

Rulegraph


![alt tag](Rulegraph.png)


DAG for example Sample
![alt tag](dag.png)
