## RNA-seq pipeline v2

### Summary
Update the RNA-seq pipeline in KBase to make it more modular and scalable (requires additional platform support - details below). Also offer additional tools that reduce compute and improve usability.

### Story/Description
#### List of updates to the existing pipeline (2-3 sprints)
1. Enable/modularize the Tuxedo pipeline based on standalone methods.
  1. Create new method that runs TopHat immediately on a single sample
  2. Create a method to run CuffMerge and CuffDiff in a single step
  3. Note there are logical dependencies that make it impossible to run certain components out of sequence. It is not possible to run Cufflinks or later tools without first aligning the reads using Bowtie/Tophat/ or others. Also note that cufflinks is already generic in the sense that either Bowtie or TopHat can be used for aligning the reads.
  4. Create new method to run Cufflinks on multiple pre-aligned reads (will have to confirm the same reference genome and annotation file was used). **This has Q2/3 scaling dependencies on the SDK currently.**
  5. Create a method to run entire Tuxedo pipeline end-to-end after setting the parameters. **This has Q2/3 scaling dependencies on the SDK currently.**
2. Update the Tuxedo pipeline to use new version of Genome.
3. Provide UI elements to control advanced parameters
  1. Review these advanced options to make sure all the important ones are exposed and system parameters are autoset
3. Precompute Bowtie indexes for all reference genomes in data store
4. Add quality check tools for RNA-seq reads such as FastQC and enable existing ones such as Trimmomatic.
4. Build downloaders for RNA-seq datatypes.
5. Additional visualization support for output alignments, etc. **Bam alignments could be visualized by JBrowse however that is Q3/4 dependency.** 

#### Review and prototype additional tools that reduce compute and improve usability (1-2 sprints per tool)
1. Every tool also requires added efforts for supporting upload, download, visualization, documentation. 
2. Here is the initial list that is subject to change after the final review, as more information comes to forth regarding their performance and accuracy, particularly Kallisto. 
  1. STAR
  2. HISAT2
  3. EdgePro
  4. StringTie
  5. DESeq
  6. Kallisto-Sleuth


### Platform dependency:
1. Bulk Uploaders
  1. Make sure to capture metadata about the samples at upload
2. Ability to scale a compute-intensive job using multiple AWE workers or HPC
3. JBrowse browser for viewing BAM alignments

### Test plan
1. Test scalability for 50-100 samples for bulk upload
2. Test scalability for 50-100 samples for all compute-intensive methods, incl. alignment

### Citations
1. STAR: http://bioinformatics.oxfordjournals.org/content/early/2012/10/25/bioinformatics.bts635
2. EdgePro: http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3603529/
3. StringTie: http://www.nature.com/nbt/journal/v33/n3/full/nbt.3122.html
4. DESeq: http://genomebiology.biomedcentral.com/articles/10.1186/gb-2010-11-10-r106
5. Kallisto: https://pachterlab.github.io/kallisto/about.html
6. HiSat: http://www.nature.com/nmeth/journal/v12/n4/full/nmeth.3317.html



