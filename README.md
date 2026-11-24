# Towards Efficient *k*-Mer Set Operations via Function-Assigned Masked Superstrings - supplementary materials

Here we provide supplementary materials for the paper *Towards Efficient k-Mer Set Operations via Function-Assigned Masked Superstrings*, including the data sets used and experimental pipelines.

See the [supplementary material pdf](supplementary-material.pdf).

### Citation

> Ondřej Sladký, Pavel Veselý, and Karel Břinda: Towards Efficient *k*-Mer Set Operations via Function-Assigned Masked Superstrings.
> *Proceedings of the Prague Stringology Conference (PSC)*, pp. 26–40, 2025. [Paper](https://www.stringology.org/event/2025/p04.html); preprint: *bioRxiv* 2024.03.06.583483, [https://doi.org/10.1101/2024.03.06.583483](https://doi.org/10.1101/2024.03.06.583483)

```
@inproceedings{Sladky2025fms,
  title = {Towards efficient $k$-mer set operations via function-assigned masked superstrings},
  author = {Ond{\v{r}}ej Sladk{\'{y}} and Pavel Vesel{\'{y}} and Karel B{\v{r}}inda},
  booktitle = {Proceedings of the Prague Stringology Conference 2025},
  editor = {Jan Holub and Jan {\v{Z}}{\v{d}}{\'{a}}rek},
  pages = {26--40},
  address = {Czech Technical University in Prague, Czech Republic},
  isbn = {978-80-01-07461-9},
  year = {2025}
}
```

## Methods

### Indexing $f$-masked superstrings - FMSI

Indexing, membership queries, and set operations on $k$-mer sets represented via $f$-masked superstrings
was performed and benchmarked on [FMSI](https://github.com/OndrejSladky/fmsi),
which experimentaly implements membership queries as well as several basic operations on indexed
masked superstrings such as normalization, export and merging, which can be used to perform set operations.

### Used $f$-masked superstrings computed by KmerCamel🐫
To compute the $f$-masked superstrings used for representing the $k$-mer sets, we used [KmerCamel🐫](https://github.com/OndrejSladky/kmercamel)  (see also the [masked superstrings paper](https://doi.org/10.1101/2023.02.01.526717)).
Specifically we have used the (default) global greedy algorithm .

## Experimental evaluation

### Benchmark datasets

* *C. elegans* (`NC_003279.8`) - downloaded from [NCBI](https://www.ncbi.nlm.nih.gov)
  - [data/C.elegans.fna.xz](data/C.elegans.fna.xz)
* *C. briggsae* (`NC_013489.2`) - downloaded from [NCBI](https://www.ncbi.nlm.nih.gov)
  - [data/C.briggsae.fna.xz](data/C.briggsae.fna.xz)



### Reproducing experimental results

After cloning this repository, run the following to download all the dependencies.

```bash 
git submodule update --init
```
After that, CBL, FMSI, and KmerCamel (the submodules) need to be compiled, as described in each of these repositories. We note that CBL need to be compiled for each value of *k* separately, and we provide Bash script `compileCBL.sh` that compiles it for $k=21$.

#### Experimental evaluation of set operations

To reproduce the experimental evaluation of set operations, 
decompress [data/C.elegans.fna.xz](data/C.elegans.fna.xz) and [data/C.briggsae.fna.xz](data/C.briggsae.fna.xz) into directory `experiments/set_operations/`
and run the following (it requires to have Jellyfish 2 (v2.2.10) installed)

```bash
cd experiments/set_operations
python3 run_experiments.py
```

The input files can possibly be changed in `run_experiments.py` (variables `file1` and `file2` on lines 9 and 10, resp.). The values of *k* tested can be changed in line 123.

To evaluate the performance of CBL on the roundworm datasets, go to directory `experiments/set_operations` and run `./run_cbl.sh C.briggsae.fna C.elegans.fna <k>`, which generates log files into director CBL-logs/ from `/usr/bin/time` on Linux (or `gtime` on the darwin platform). The results for $k=21$ are in `experiments/set_operations/CBL-logs-kamenac/`.

## Figures

### Fig. 2 - Experiment on set operations

The data for the figure were taken from [experiments/set_operations/results-roundworms.csv](experiments/set_operations/results-roundworms.csv), computed on *C. elegans* and *C. briggsae* genomes.

## Contact

* Ondřej Sladký (ondra.sladky@gmail.com)
* Pavel Veselý (vesely@iuuk.mff.cuni.cz)
* Karel Břinda (karel.brinda@inria.fr)
