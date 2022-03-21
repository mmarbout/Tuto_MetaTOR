# Tuto_MetaTOR

Practical course to learn how to use MetaTOR piepline and Hi-C data for binning of metagenomic assemblies.


## Table of contents

* [MetaTOR](#MetaTOR)
* [Dataset](#Dataset)
* [Usage](#Usage)
* [End-to-End pipeline](#End-to-End-pipeline)
* [Output files](#Output-files)
* [References](#References)
* [Contact](#Contact)

## MetaTOR

Metagenomic Tridimensional Organisation-based Reassembly

<p align="center">
  <img src="docs/example/images/metator_logo.png" width="200">
</p>

A tutorial is available [here](docs/example/metator_tutorial.md) to explain how to use metaTOR. More advanced tutorials to analyze the output files are also available:

* [Anvio](https://merenlab.org/software/anvio/) manual curation of the contaminated bins. Available [here](docs/example/manual_curation_of_metator_MAGs.md).
* Visualization and scaffolding of the MAGs with the contactmap modules of MetaTOR. Available [here](docs/example/MAG_visualization_and_scaffolding.md).

Principle of MetaTOR pipeline:

![metator_pipeline](docs/example/images/metator_figure.png)

## Dataset

The different data needed to perform the practical course can be found at the following path:

```sh
   ls -l /opt/metagenomics/tp3/
```

The folder contain the FastQ files and the assembly of the studied Metagenome. This is a simple metagenomic dataset ranging from a mice fecal sample with a defined community.

## Usage

MetaTOR is a modular piepline allowing to perform each step separetly or in end to end pipeline

```sh
    metator {network|partition|validation|pipeline} [parameters]
```

A metaTOR command takes the form `metator action --param1 arg1 --param2
arg2 #etc.`

There are three actions/steps in the metaTOR pipeline, which must be run in the
following order:

* `network` : Generate metaHiC contigs network from fastq reads or bam files and normalize it.
* `partition` : Perform the Louvain or Leiden community detection algorithm many times to bin contigs according to the metaHiC signal between contigs.

* `validation` : Use CheckM to validate the bins, then do a recursive decontamination step to remove contamination.

There are a number of other, optional, miscellaneous actions:

* `pipeline` : Run all three of the above actions sequentially or only some of them depending on the arguments given. This can take a while.
* `contactmap` : Generates a contact map from one bin from the final ouptut of metaTOR.

* `version` : display current version number.

* `help` : display help message.

## End-to-End pipeline

using the provided dataset, you can launch the whole pipeline. You will skeep the validation step as checkM is a very consuming software (40 Go RAM) unable to run on your VM.

```sh
    metator pipeline -v -F -i 10 -a /opt/metagenomics/tp3/ass_tuto.fa -1 /opt/metagenomics/tp3/Tuto_for.fastq.gz -2 /opt/metagenomics/tp3/Tuto_rev.fastq.gz -o Meta3C
```

MetaTOR will provide you with various metrics about the whole pipeline. It will also generate different files necessary for downstream analysis.

you can restart the pipeline by varying the number of iterations of the louvain algorithm.

## Output files

As we have launch the pileine without the checkM validation, the output files are not complete.

You will find the complete output files at the following path:

```sh
   ls -l /opt/metagenomics/tp3/output_Tuto/
```


## References

* [Metagenomic chromosome conformation capture (meta3C) unveils the diversity of chromosome organization in microorganisms](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4381813/), Martial Marbouty, Axel Cournac, Jean-François Flot, Hervé Marie-Nelly, Julien Mozziconacci, and Romain Koszul, eLife, 2014
* [Meta3C analysis of a mouse gut microbiome](https://www.biorxiv.org/content/early/2015/12/17/034793), Martial Marbouty, Lyam Baudry, Axel Cournac, Romain Koszul, 2015
* [Scaffolding bacterial genomes and probing host-virus interactions in gut microbiome by proximity ligation (chromosome capture) assay](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5315449/), Martial Marbouty, Lyam Baudry, Axel Cournac, and Romain Koszul, Science Advances, 2017

## Contact

### Authors

* amaury.bignaud@pasteur.fr
* martial.marbouty@pasteur.fr
* romain.koszul@pasteur.fr

### Research lab

[Spatial Regulation of Genomes](https://research.pasteur.fr/en/team/spatial-regulation-of-genomes/) (Institut Pasteur, Paris)
