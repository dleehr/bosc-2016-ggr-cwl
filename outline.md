#  CWL in Practice: Experiences, challenges, and results from adopting Common Workflow Language

 _Dan Leehr_, Alejandro Barrera, Tim Reddy, Hilmar Lapp

 ---

 - Repeatability, Reproducibility, Generalizability
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

Background
- GGR - better understand first 12 hours of glucocortioid response
- gene editing to turn on and off genes, to elucidate (make clear) the network of gene regulation in GCR
- To do this, compare results of numerous genmoic experiments in each condition
- Processing pipelines that can be confidently repeated, reused, and customized
- Internally (today) and externally tomorrow

So how are we using CWL and how are we NOT using CWL

Benefits:
- Forces explicit design in workflow and identifying connections/dependencies.
  - what files are actually required at this step?
- Output files are always checksummed

Challenges
- Control flow & scheduling
  - Primarily Alex
  - Identifying inputs and outputs - considering steps in the workflow as functions on data.
  - Can't just provide *.fa or encode metadata into filenames, you need to be explicit
- File name replacement and other common expression operations
  - var, join, change_ext, base
- Practical aspects on a shared HPC cluster
  - Docker and shared environments
    -
    - Still building docker images for these tools, since that addresses the distributability question
    -
  - helmod
  - slurm/toil (what is BD2K?)

Other notes

- wrapper scripts are a sign something is missing


Results
- Slow initially
-
