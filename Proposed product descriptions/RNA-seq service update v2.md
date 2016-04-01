## RNA-seq service update

### Summary
In this campaign, we will update the RNA-seq service to include support for the new Genome data object via the Data API, new downloaders, additional interactive widgets and plots. As a result, this will also include refactoring of the current functionality and related modifications in apps and documentation.

### Story/Description
1. Enable/modularize the Tuxedo pipeline based on standalone methods.
  1. Create new method that runs TopHat immediately on a single sample
  2. Create a method to run CuffMerge and CuffDiff in a single step
  3. Note there are logical dependencies that make it impossible to run certain components out of sequence. It is not possible to run Cufflinks or later tools without first aligning the reads using Bowtie/Tophat/others. Also note that cufflinks is already generic in the sense that either Bowtie or TopHat can be used for aligning the reads.
2. Update the Tuxedo pipeline to use new version of Genome.
3. Provide UI elements to control mandatory and advanced/optional parameters
  1. Review mandatory and advanced options to make sure all the important ones are exposed and system parameters are autoset
4. Extend current functionality to get annotations for new genome objects. Also, precompute and load annotations for reference genomes
5. Precompute Bowtie indexes for all reference genomes in data store
6. Add downloaders for RNA-seq datatypes (reads, alignment, cuffdiff output, cummerbund plots).
7. Additional visualization support for output alignments, including [iobio](http://bam.iobio.io/). 


### Platform dependency:
1. Bulk Uploaders
  1. Make sure to capture metadata about the samples at upload
2. Ability to scale a compute-intensive job using multiple AWE workers or HPC
3. JBrowse browser for viewing BAM alignments

### Test plan
1. Test scalability for 50-100 samples for bulk upload
2. Test scalability for 50-100 samples for all compute-intensive methods, incl. alignment





