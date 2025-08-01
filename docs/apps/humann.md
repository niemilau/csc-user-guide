---
tags:
  - Free
catalog:
  name: HUMAnN
  description: Profiling microbial pathways with metagenomic data
  license_type: Free
  disciplines:
    - Biosciences
  available_on:
    - Puhti
---

# HUMAnN



HUMAnN is a pipeline for efficiently and accurately profiling the presence/absence and abundance of 
microbial pathways in a community from metagenomic or metatranscriptomic sequencing data. 
This process (functional profiling) aims to describe the metabolic potential of a microbial community and its members. 

[TOC]

## License

Free to use and open source under [MIT License](https://raw.githubusercontent.com/biobakery/humann/master/LICENSE).

## Available

Versions available in Puhti: 3.0.1, 3.6, 3.8, 3.9

## Usage

In Puhti, HUMAnN is installed as containerized application. To activate it, run command:

```text
module load humann
humann
```

By default HUMaN tries to check and update the MetaPhlAn database every
time it's run. This will fail with containerized installation, so you
will need to add command line option:

```text
--metaphlan-options "--offline --bowtie2db /path/to/db"
```

To use CSC provided database use:

```text
--metaphlan-options "--offline --bowtie2db $MPA"
```

CSC provides default versions of the HUMaN databases. You can use them by
specifying:

```text
--nucleotide-database $HUMANN_NUC
--protein-database $HUMANN_PROT
```

HUMAnN can utilize several CPU cores. To do this set `--cpus-per-task` to desired number.
In Puhti you can use up to 40 cores. Also remember to add option `--threads` to your HUMAnN
command. You can use variable `$SLURM_CPUS_PER_TASK` to automatically match the requested
number.


Example batch job script (use your actual project neame for `--account`)

```text
#!/bin/bash -l
#SBATCH --job-name=humann
#SBATCH --account=project_123456
#SBATCH --partition=small
#SBATCH --time=01:00:00
#SBATCH --ntasks=1  
#SBATCH --cpus-per-task=10
#SBATCH --mem=20000

# Load HUMaN module
module load humann

# Dowload a test file
wget https://github.com/biobakery/humann/raw/master/examples/demo.fastq.gz

# Run HUMaN
humann --threads=$SLURM_CPUS_PER_TASK --input demo.fastq.gz --nucleotide-database $HUMANN_NUC --protein-database $HUMANN_PROT --metaphlan-options "--offline --bowtie2db $MPA" --output demo_out
```

## More information

*   [HUMAnN home page](https://huttenhower.sph.harvard.edu/humann)
*   [HUMAnN user guide](https://github.com/biobakery/humann)
*   [HUMAnN tutorial](https://github.com/biobakery/biobakery/wiki/humann3)
