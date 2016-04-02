--------------   -------------------------------------------
**Title**        CWL in Practice: Adopting Common Workflow Language for
                 existing research projects and academic computing 
                 clusters
**Authors**       _Dan Leehr_, Alejandro Barrera, Hilmar Lapp
**Affiliation**  https://www.genome.duke.edu
**Contact**      dan.leehr@duke.edu
**URL**          https://github.com/Duke-GCB/GGR-cwl
**License**      MIT
--------------   -------------------------------------------

Assembling individual bioinformatics software packages to run together as a pipeline is often done by  scripting them together in a language like Bash, Python, or Perl. This approach, while simple to build and understand, often yields pipelines that are not generalizable across data sets or computing environments. Further, tracking or archiving versions of packages requires nontrivial effort, as does engineering for modularly. These properties hinder reproducibility of the process, as reconstructing the pipeline can be cumbersome or impossible without knowledge of softare versions or access to the original enivornment.

In contrast to the above, the [Common Workflow Language][1] provides a blueprint for architecting workflows. With [open source implementations][2] and a [comprehensive specification][3], it lowers the barrier to building reusable components and reproducible pipelines for bioinformatics. These pipelines can be run on any implementation supporting the language, and thus are a desirable product for reproducible research. Additionally, CWL encourages [Docker][5] images, bundling tools and their dependencies completely. The images thus allow compute environments to be perfectly archived and published.

At Duke Center for Genomic and Computational Biology (GCB), we're using CWL in support of the [Genomics of Gene Regulation][4] project. This project aims to comprehensively characterize and better understand the first 12 hours of the glucocorticoid response (GCR). Using gene editing techniques to turn on and off genes, researchers in the Reddy lab plan to elucidate the network of gene regulation involved in the GCR by comparing the results of a number of genomic experiments in each condition. Our task at hand is to develop pipelines for processing experimental data that can be confidently reused and customized. 

By building workflows that conform to the CWL standard, not only do we have flexibility to easily modify or replace parts of the GGR workflows, but we'll be able to distribute reproducible pipelines along with publications and data sets. Additionally we benefit from the ability to reuse components shared in the analysis of ChIP-seq, RNA-seq, and DNase-seq experiments.

During the research and development of these CWL pipelines, we've met two discrete challenges: translating existing logic to CWL and integrating this workflows with our high-performance computing resources. In this presentation, we will discuss our approaches to addressing these challenges. We'll cover the details of translating existing control flow and imperative scheduling logic to CWL's declarative language. This includes pragmatic approaches to reusing components for manageable workflows.

We'll also discuss the practical aspects of adopting CWL in an academic HPC environment. Our center operates a [40-node HPC cluster](https://www.genome.duke.edu/cores-and-services/computational-solutions/compute-environments-genomics) running [Slurm][6] for computational genomic workloads. As it is a shared compute environment, it is not suitable to run [Docker][5] or virtual machines favored by CWL. However, publishing [Docker][5] images makes it easier for consumers to use our workflows. We build Docker images and load modules with [helmod][7], both providing the necessary environment for CWL tools to run. Finally, we'll address how we're extending [toil][8], a workflow engine that supports CWL with [Slurm][6] integration, allowing us to scale up CWL workflows to our available compute resources.

[1]: http://www.commonwl.org
[2]: http://www.commonwl.org/#Implementations
[3]: http://www.commonwl.org/draft-3/
[4]: http://reddylab.org/projects/
[5]: http://docker.com
[6]: http://slurm.schedmd.com
[7]: http://rc.fas.harvard.edu/helmod/
[8]: http://toil.readthedocs.org/en/releases-3.1.x/essentials.html
