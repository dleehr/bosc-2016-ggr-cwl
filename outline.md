#  CWL in Practice: Experiences, challenges, and results from adopting Common Workflow Language

 _Dan Leehr_, Alejandro Barrera, Tim Reddy, Hilmar Lapp

 ---

15 minutes scheduled, so 7 slides

"2 minutes per slide"

Goal: Illustrate why CWL is useful in supporting reproducible research
Sub-goal - provide some details on challenges and what we learned

## 1. Intro: (who I am)
- Who I am: Duke GCB. Center for genomic and computational biology at Duke
  - A few of us in attendance here this week
  - We have faculty that do research - often federally funded, like the GGR project that these methods support
  - we also have an informatics team to support the center, and this support includes systems and some custom development, which is where I typically fit in.

## 2. Groundwork: (why I'm here)
- Connecting faculty trying to do research with appropriate tools and support
- We (informatics) are empowered to identify, recommend, and implement ways to support computational research reproducibility.
- GGR - better understand first 12 hours of glucocortioid response
- gene editing to turn on and off genes, to elucidate (make clear) the network of gene regulation in GCR
- To do this, compare results of numerous genomic experiments in each condition
- moves fast, lots of data

-- Bunch of these next slides are saying the same thing

## 3. Goals of the pipelines

- Run on our HPC cluster
  - hardac:50 node slurm cluster, 128-256GB and 32 cores each
  - Scale with resources and be a good citizen
  - not a commodity cloud or a pool of VMs (but that's coming!)
- Distributable and reproducible
  - We can repeat our own results
  - Consistently run a dataset through the pipeline
  - Modular components (how did results change),
- Leverage existing work tractable and usable

Goals are all linked

## 4. Pipelines I

- 3 different genomic processing pipelines: ChIP, rna, dnase
- Many shared steps some distinct. e.g. both use bowtie


Take an example of two initial steps: QC and trimming

- show the original bash code for these
- show the cwl code and the modules

- FastQC
  -
- Trimmomatic (Illumina)

Repeating across compute environments

- scripts like `run_analysis.sh` is an easy entrypoint, but it depends on the state of the computing environment
  - on a shared system you immediately encounter things like file permissions
- Easy to interleave control flow with data flow
  - If I have a slurm cluster I want to optimize my analysis for it.
  - while (squeue -u dcl9) sleep 1
- Make code independent of data? (scripts should not have hard-coded paths, or should they?)
-



## HPC challenges (after CWL/Docker)

## Existing HPC cluster

- Shared across the center
- Users don't have root access
- Memory/CPU usage governed by the scheduler


## Why CWL?

- Structured language
- Declarative and not a script

Makes it really hard to leave things ambiguous
  -



Candidates:
- pipelines in development
-
- docker (good for building images and distributing, archiving them)
- Workflow language



## Existing HPC cluster



- HARDAC
  - SLURM HPC, 50+nodes, 128-256GB RAM and 32 cores each
  - 500TB scratch space (Infiniband)
  - shared linux system

## Try 1: In search of solution (what I did)
- Cite NESCent reproducibility paper?
    - Even with source code and a makefile, that's not enough
    http://bib.oxfordjournals.org/content/early/2016/03/23/bib.bbw020.abstract
- Docker. As a developer on several applications with complex dependencies, this seemed like the holy grail.
    - but it still might not be enough!
- Bake a container image and put it on a shelf. High-level view everything looks like a single script.
- Built a prototype thing: docker-pipeline around another collaborator's pipeline.
- make it easy to distribute and substitute containers

## Learned 1

- hard to use
- Lots of time spend writing wrapper scripts to conform to an interface. Obvious this was one of the most important pieces
- Docker-only, which didn't suit our cluster very well. Good for distribution.

## Try 2: CWL

-


Other Notes:

Nix: http://dl.acm.org/citation.cfm?id=2830172
- docker builds can fail!
- docker may be a stopgap - but a central hub is very powerful

Guix: http://arxiv.org/abs/1506.02822


## Repeatability, Reproducibility, Generalizability

- Tools are one axis - tracking and archiving software versions. Also data and workflow
- Recipe
  - Tools = Equipment
  - Steps and quantities = workflow (this is the hard part)
  - Data = ingredients
- Scripts and workflows
- Perl, Python, bash.
- Great to automate, but often very specific.
- Like programming a robot to break an egg
- "move arm 4 inches to the left, grip handle, actuate door, search for egg in egg tray 6" below door top
- What if refrigerator is different, or eggs aren't kept there?
- Little incentive to build these scripts as products because they're not our product. They're our junk drawer - the ugly details that let us connect tools to data.


## Background

- Processing pipelines that can be confidently repeated, reused, and customized
- Internally (today) and externally tomorrow

## Benefits

- Forces explicit design in workflow and identifying connections/dependencies.
  - what files are actually required at this step?
- Output files are always checksummed

## Challenges
- Control flow & scheduling
  - Primarily Alex
  - Identifying inputs and outputs - considering steps in the workflow as functions on data.
  - Can't just provide *.fa or encode metadata into filenames, you need to be explicit
  - No provisions for conditionals.
    - 3 workflows with many shared subworkflows (
  Having 3 workflows with some shared steps still requires a lot of boilerplate. Writing by hand is error prone, we're trying templating
  -
- File name replacement and other common expression operations
  - var, join, change_ext, base
- Practical aspects on a shared HPC cluster
  - Docker and shared environments
    -
    - Still building docker images for these tools, since that addresses the distributability question
    -
  - helmod
  -
  - slurm/toil (what is BD2K?)

Other notes

- wrapper scripts are a sign something is missing
- So how are we using CWL and how are we NOT using CWL
- Slow initially
-
