---
tags:
  - Non-commercial
catalog:
  name: MOLPRO
  description: Package for accurate ab initio quantum chemistry calculations
  license_type: Non-commercial
  disciplines:
    - Chemistry
  available_on:
    - Puhti
    - Mahti
---

# MOLPRO

MOLPRO is a software package geared towards accurate ab initio quantum chemistry calculations. The emphasis in the program is on highly accurate computations, with extensive treatment of the electron correlation problem through the multireference configuration interaction, coupled cluster and associated methods.

## Available

-   Puhti: 2024.3
-   Mahti: 2024.3

## License

-  The use of the software is restricted to non-commercial research. 

## Usage

Initialise MOLPRO on Puhti or Mahti:

```bash
module load molpro/2024.3
```


Molpro has been built with the Global Arrays toolkit (`--with-mpi-pr`) that allocates one helper process per node for parallel MPI runs.

!!! info "Note"
    Although some parts of the code support shared memory parallelism (OpenMP), its use is not generally recommended.

### Example batch scripts

!!! info "Note"
    Wave function-based correlations methods, both single and multireference, often create a
    substantial amount of disk I/O. In order to achieve maximal performance for the job and to
    avoid excess load on the Lustre parallel file system it is advisable to use the local disk.

=== "Puhti"

    ```bash
    #!/bin/bash
    #SBATCH --partition=test
    #SBATCH --nodes=2
    #SBATCH --ntasks-per-node=40      # MPI tasks per node
    #SBATCH --account=yourproject     # insert here the project to be billed 
    #SBATCH --time=00:15:00           # time as `hh:mm:ss`
    module purge
    module load molpro/2024.3

    export MOLPRO_TMP=$PWD/MOLPRO_TMP_$SLURM_JOB_ID
    mkdir -p $MOLPRO_TMP

    $MOLPROP -d$MOLPRO_TMP -I$MOLPRO_TMP -W$PWD test.com
    rm -rf $MOLPRO_TMP
    ```

=== "Puhti, local disk"

    ```bash
    #!/bin/bash
    #SBATCH --partition=large
    #SBATCH --nodes=2
    #SBATCH --ntasks-per-node=40
    #SBATCH --account=yourproject     # insert here the project to be billed
    #SBATCH --time=00:15:00           # time as `hh:mm:ss`
    #SBATCH --gres=nvme:100           # requested local disk space in GB
    module purge
    module load molpro/2024.3
    export MOLPRO_TMP=$LOCAL_SCRATCH/MOLPRO_TMP_$SLURM_JOB_ID
    mkdir -p $MOLPRO_TMP

    $MOLPROP -d$MOLPRO_TMP -I$MOLPRO_TMP -W$PWD test.com
    rm -rf $MOLPRO_TMP
    ```

=== "Mahti"
 
     On Mahti, it is often necessary to undersubscribe cores per node to ensure sufficient memory per core. See the [Mahti job script guidelines](../computing/running/creating-job-scripts-mahti.md#undersubscribing-nodes) for more details.

    ```bash
    #!/bin/bash
    #SBATCH --partition=test
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=16
    #SBATCH --cpus-per-task=8
    #SBATCH --account=yourproject     # insert here the project to be billed
    #SBATCH --time=0:10:00 # time as hh:mm:ss
    # set --ntasks-per-node=X and --cpus-per-task=Y so that X * Y = 128
    module purge
    module load molpro/2024.3

    export MOLPRO_TMP=$PWD/MOLPRO_TMP_$SLURM_JOB_ID
    mkdir -p $MOLPRO_TMP

    $MOLPROP -d$MOLPRO_TMP -I$MOLPRO_TMP -W$PWD test.com
    rm -rf $MOLPRO_TMP
    ```

### Example of scalability

The performance of Molpro depends a lot on the system size and which computational model is used. The following table shows the wall time used (in seconds) for a single-point energy calculation on benzene (C<sub>6</sub>H<sub>6</sub>) at CCSD(T)/aug-cc-pVTZ level, as function of the number of cores. The table shows also the corresponding timings when the local disk (NVMe) is used. Note that the parallel runs allocate one core per node for a helper process, hence there is one core less per node used for the actual calculation. 


| Cores               |Wall time/Lustre (s) | Wall time/NVMe (s) |
| ------------------: | ------------------: | -----------------: |
|  1                  | 11749               |   10962            |
|  5                  |  3254               |    3228            |
| 10                  |  1730               |    1561            |
| 20                  |  1394               |    1239            |
| 40                  |  1112               |     814            |
| 2x20                |   786               |     729            |
| 2x40                |   716               |     701            |    


## References

All publications resulting from use of MOLPRO must acknowledge the following three references.

1. H.-J. Werner, P. J. Knowles, G. Knizia, F. R. Manby and M. Schütz, WIREs Comput Mol Sci 2, 242–253 (2012), [doi: 10.1002/wcms.82](https://onlinelibrary.wiley.com/doi/abs/10.1002/wcms.82)
2. Hans-Joachim Werner, Peter J. Knowles, Frederick R. Manby, Joshua A. Black, Klaus Doll, Andreas Heßelmann, Daniel Kats, Andreas Köhn, Tatiana Korona, David A. Kreplin, Qianli Ma, Thomas F. Miller, III, Alexander Mitrushchenkov, Kirk A. Peterson, Iakov Polyak, Guntram Rauhut, and Marat Sibaev J. Chem. Phys. 152, 144107 (2020). [doi:10.1063/5.0005081](https://doi.org/10.1063/5.0005081)
3. MOLPRO, version , a package of ab initio programs, H.-J. Werner, P. J. Knowles, P. Celani, W. Györffy, A. Hesselmann, D. Kats, G. Knizia, A. Köhn, T. Korona, D. Kreplin, R. Lindh, Q. Ma, F. R. Manby, A. Mitrushenkov, G. Rauhut, M. Schütz, K. R. Shamasundar, T. B. Adler, R. D. Amos, J. Baker, S. J. Bennie, A. Bernhardsson, A. Berning, J. A. Black, P. J. Bygrave, R. Cimiraglia, D. L. Cooper, D. Coughtrie, M. J. O. Deegan, A. J. Dobbyn, K. Doll and M. Dornbach, F. Eckert, S. Erfort, E. Goll, C. Hampel, G. Hetzer, J. G. Hill, M. Hodges and T. Hrenar, G. Jansen, C. Köppl, C. Kollmar, S. J. R. Lee, Y. Liu, A. W. Lloyd, R. A. Mata, A. J. May, B. Mussard, S. J. McNicholas, W. Meyer, T. F. Miller III, M. E. Mura, A. Nicklass, D. P. O'Neill, P. Palmieri, D. Peng, K. A. Peterson, K. Pflüger, R. Pitzer, I. Polyak, P. Pulay, M. Reiher, J. O. Richardson, J. B. Robinson, B. Schröder, M. Schwilk and T. Shiozaki, M. Sibaev, H. Stoll, A. J. Stone, R. Tarroni, T. Thorsteinsson, J. Toulouse, M. Wang, M. Welborn and B. Ziegler, see [https://www.molpro.net](https://www.molpro.net).

Some journals insist on a shorter list of authors; in such a case, the following should be used instead.

1. MOLPRO, version , a package of ab initio programs, H.-J. Werner, P. J. Knowles, and others, see [https://www.molpro.net](https://www.molpro.net).

Depending on which programs are used, additional references should also be cited. For instructions see the [manual](https://www.molpro.net/manual/doku.php?id=references).

## More information

-  [Molpro home page](https://www.molpro.net/)  
-  [Manual](https://www.molpro.net/manual/doku.php)
-  [Quick start](https://www.molpro.net/manual/doku.php?id=quickstart)
-  [User forum](https://groups.google.com/g/molpro-user)

  
