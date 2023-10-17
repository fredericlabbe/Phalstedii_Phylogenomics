# Phalstedii_Phylogenomics
Collection of scripts for a range of genomic data processing and analysis.
Not everything is documented yet, but most scripts have some helpful information if you type `python script.py -h`.

## Contents

* [Converting SNP coordinates](#Converting-SNP-coordinates)
* [Converting genomic window coordinates](#Converting-genomic-window-coordinates)

## Converting SNP coordinates
This script `VCFCoordConv.py` converts SNP coordinates in a [VCF](https://gatk.broadinstitute.org/hc/en-us/articles/360035531692-VCF-Variant-Call-Format) file (i.e. chromosome, starting position, and ending position) from one coordinate system to another. This script can also export the dictionary of coordinates between the two coordinates systems. It uses a syntenic path file generated by `SynMap` [(Haug-Baltzell *et al.* 2017)](https://pubmed.ncbi.nlm.nih.gov/28334338/) which provide the order and orientation of contigs between genome assemblies. This csv syntenic path file should at least contains the five columns:
* `Dest_Chromosome`: Name of the chromosome/scaffold in the destination coordinate system.
* `Src_Scaffold`: Name of the chromosome/scaffold in the source coordinate system.
* `Start`: Starting position of the chromosome/scaffold in the source coordinate system.
*  `End`: Ending position of the chromosome/scaffold in the source coordinate system.
* `Reverse`: Reversed (1) or non-reversed (0) chromosome/scaffold in the source coordinate system in comparison to the chromosome/scaffold in the destination coordinate system.

#### Example command
`python VCFCoordConv.py --vcf /path/to/file.vcf.gz' --table /path/to/table.csv'`

`python VCFCoordConv.py -h` Will print a full list of command arguments.

#### Command arguments
| Name | Description |
| :--: | ----------- | 
| `vcf` | Path to the vcf file or gzipped vcf file (required) |
| `table`  | Path to the csv table of the syntenic path generated by SynMap (required) |
| `export`  | Whether the dictionary of coordinates should be exported as a csv table (optional) |

#### Notes
The VCF file should not contain the INFO field (as it can contains "," and thus impacts the script outputs) and should have the following extensions: `vcf` or `vcf.gz`. To run it, ensure that you are using Python v.3.7, and have installed the following dependencies: [os](https://docs.python.org/3/library/os.html), [gzip](https://docs.python.org/3/library/gzip.html), [re](https://docs.python.org/3/library/re.html), [pandas](https://pandas.pydata.org/), [argparse](https://docs.python.org/3/library/argparse.html), and [sys](https://docs.python.org/3/library/sys.html).

## Converting genomic window coordinates
This script `WindCoordConv.py` converts the genomic window coordinates in a csv file (i.e. chromosome, starting position, and ending position) from one coordinate system to another. It uses a dictionary of coordinates as a csv table generated by `VCFCoordConv.py`.

#### Example command
`python WindCoordConv.py --table /path/to/table.csv' --dictionary /path/to/dictionary.csv' --size 100000'`

`python WindCoordConv.py -h` Will print a full list of command arguments.

#### Command arguments
| Name | Description |
| :--: | ----------- | 
| `dictionary` | Path to the dictionary of coordinates as a csv table (generated by `VCFCoordConv.py`) (required) |
| `table`  | Path to the csv table with genomic window coordinates to convert (required) |
| `size`  | Window size in bp (required) |

#### Notes
To run it, ensure that you are using Python v.3.7, and have installed the following dependencies: [os](https://docs.python.org/3/library/os.html), [re](https://docs.python.org/3/library/re.html), [pandas](https://pandas.pydata.org/), [argparse](https://docs.python.org/3/library/argparse.html), and [sys](https://docs.python.org/3/library/sys.html).

___
## Citation

Please cite this when using these scripts:
Pecrix Y., Dvorak E., Labbé F., Besnard G., Delmotte F., Godiard L., 2024. Phylogenomics reveals evolutionary history of admixed *Plasmopara halstedii* strains and genomic regions associated to the breakdown of sunflower resistance genes. XXX. https://doi.org/XXX
