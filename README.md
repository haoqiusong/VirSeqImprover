# VirSeqImprover

An integrated pipeline for error-correction, extension, and annotation of viral scaffolds to recover error-free full genomes of viruses and phages by polishing and extending draft viral assemblies.

# Installation

Use conda install to install VirSeqImprover.

```bash
conda install virseqimprover --channel haoqiusong
```

# Run VirSeqImprover

## Input

A viral scaffold/contig (.fasta) and the read sample (.fastq) from which the input scaffold is assembled.

The reads can be paired-end reads or single-end reads. For paired-end reads, two separate read files are needed.

## Usage

Command line example:
```bash
-1 /home/VirSeqImprover/input/read1.fastq -2 /home/VirSeqImprover/input/read2.fastq -scaffold /home/VirSeqImprover/input/scaffold.fasta -o /home/VirSeqImprover/output
```
For all the files and directory, full paths are recommended in the input.

## Output

The ouput folders and files will be generated in the output directory folder you specify. (If not specified, it will be the same directory of your input files by default.)

The final output file -- ```pilon_out.fasta``` is the final improved scaffold of the original scaffold.

# Annotation example

1. After applying VirSeqImprover to the viral scaffold, use an online tool eggNOG-mapper (http://eggnog-mapper.embl.de/) to annotate viral genes. On the website, choose "Metagenomic" as the data kind, Prodigal as the gene prediction method, then upload the improved scaffold file, and choose "Viruses - 10239" as the taxonomic scope.

2. When the job is done, download the ```out.emapper.decorated.gff``` and ```out.emapper.annotations``` files, use them to generate two separated annotation tables (.csv), including the annotated and unannotated genes by running ```ann.py```.

Command line example:
```bash
python ann.py
./out.emapper.annotations
./out.emapper.decorated.gff
```

3. Upload ```pilon_out.fasta``` (as the sequence) and the two .csv files (as the features) generated by ```ann.py``` to an online visualization tool Proksee (https://proksee.ca/) to visualize the annotation of the improved viral scaffold.
