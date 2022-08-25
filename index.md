## A Helpful Guide to RNA Splicing Tools

*A beginner’s step-by-step guide to using current RNA Splicing prediction tools (Pangolin, MTSplice and SpliceAI).* 

This page includes: 
* Input and Output Formats 
* Different Types of Predictions 
* Pangolin Usage 
* MTSplice Usage 
* SpliceAI Usage 
* Glossary 

To learn more about RNA splicing and deep learning prediction in this field, visit this [page](https://snehabalaji.github.io/Technical/). I strongly recommended gathering foundational knowledge in both fields before proceeding to use the splicing tools. 

Credits: 
I would like to thank the authors of the following papers for making their tools free and easily accessible. The tools discussed in this webpage are credited to the following people: 
* Pangolin: Created by Zeng, T. and Li, Y.I. The github repository can be found [here](https://github.com/tkzeng/Pangolin).
* SpliceAI: Created by Kishore Jaganathan,Sofia Kyriazopoulou Panagiotopoulou,Jeremy F. McRae,Siavash Fazel Darbandi,David Knowles,Yang I. Li,Jack A. Kosmicki,Juan Arbelaez,Wenwu Cui,Grace B. Schwartz,Eric D. Chow,Efstathios Kanterakis,Hong Gao,Amirali Kia et al.. The github repository can be found [here](https://github.com/Illumina/SpliceAI).
* MTSplice: Created by Jun Cheng, Thi Yen Duong Nguyen, Kamil J Cygan, Muhammed Hasan Çelik, William G Fairbrother, Žiga Avsec, Julien Gagneur. The github repository can be found [here](https://github.com/snehabalaji/MMSplice_MTSplice).

## Introduction 
Hi everyone! My name is Sneha Balaji and I’m a second year [Engineering Science](https://engsci.utoronto.ca/program/what-is-engsci/)  student at the University of Toronto in Toronto, Canada! This summer I had the opportunity to intern at [King Mongkut’s University of Technology Thonburi](https://www.kmutt.ac.th/en/) (KMUTT) in Bangkok, Thailand. 

Over the course of my summer, my research mainly focused on RNA splicing, specifically about the various prediction tools in this ever-growing field. As someone who has freshly finished first year and with minimal technical expertise, I found it quite the challenge to understand and effectively use these tools. So, I decided to create this blog so that individuals with less technical backgrounds can have an easier time accessing and using these tools. Feel free to reference the **Glossary** at the bottom of this page for any unknown terminology!

This blog will focus on three current tools in particular: Pangolin, MTSplice and SpliceAI. A bit about these tools: 
* **Pangolin**: a deep learning technique that uses DNA sequences from four different species to predict both usage of a splice site and probability with reasonable accuracy in genetic variations. 
* **MTSplice and MMSplice**: both predict the effect of genetic variants using cassette exons using human tissues. MTSplice has been trained on tissue-specific variants, giving it tissue-specific prediction abilities as opposed to MMSplice.
* **SpliceAI**: a neural network that predicts splice sites from any given pre-mRNA sequence with a high degree of accuracy.

The tools above mainly focus on predicting the effects of a multitude of variants on RNA splicing, aiming to help scientists and researchers better understand the complex world of alternative splicing. 

## Input & Output Formats 
Pangolin, MTSplice and SpliceAI were created at different times by different people and as a result, operate using different input and output formats. 

Below is a helpful table of the input and output formats of each of the tools: 

<img width="440" alt="Screen Shot 2022-08-23 at 3 25 13 PM" src="https://user-images.githubusercontent.com/98296345/186252270-58dfdd63-d700-4538-84f3-5109f0ca39e8.png">

<img width="514" alt="Screen Shot 2022-08-23 at 3 25 18 PM" src="https://user-images.githubusercontent.com/98296345/186252413-091db449-26e5-44a6-a2e2-c2df333f0732.png">

With specific reference to the file formats: 
* **VCF**: Known as Variant Call Format files are a text used to store gene sequences. 
* **CSV**: Known as Comma Separated Value files are text files that can be easily arranged as a spreadsheet.  

Here is an example of the inputs for each of the tools: 
* **Pangolin**: The file is from gencode.v38 specifically the lift 37.annotation (which is the 37 version annotation of the human genome GRCh38):
<img width="1435" alt="Screen Shot 2022-08-25 at 11 22 54 AM" src="https://user-images.githubusercontent.com/98296345/186740518-4e363f60-0cc9-43e4-87b8-04a07d0cbcac.png">

* **MTSplice**: Here is an example of a possible MTSplice’s input from the ClinVar database: 
<img width="1440" alt="Screen Shot 2022-08-25 at 2 23 59 PM" src="https://user-images.githubusercontent.com/98296345/186740649-fab8783f-709e-4c0c-94be-9a418a9abd0d.png">

* **SpliceAI**: Here is an example input: 
<img width="538" alt="Screen Shot 2022-08-25 at 11 54 43 AM" src="https://user-images.githubusercontent.com/98296345/186740525-def328ae-2dc2-441b-b614-ada58848bf4a.png">

However, pre-processing is often required before feeding genetic information to these tools. Below is a table of the various preprocessing methods for each tool: 

<img width="646" alt="Screen Shot 2022-08-23 at 3 25 28 PM" src="https://user-images.githubusercontent.com/98296345/186252415-bdf29f99-a74a-4f6d-acab-4d18dff51df6.png">

Specifics on each preprocessing method will be discussed under each tool. 

In addition to feeding the model the gene file for prediction, each model also requires the input of an annotation file in the GTF format. These standard human genome files can be sourced from [ensembl](https://useast.ensembl.org/Homo_sapiens/Info/Index) or [gencode](https://www.gencodegenes.org/human/). 

## Different Types of Predictions 
The three different models can also predict different features with respect to RNA splicing, the table shown below helps to summarize some of these prediction capabilities.

<img width="664" alt="Screen Shot 2022-08-23 at 3 25 34 PM" src="https://user-images.githubusercontent.com/98296345/186252418-e4e3a25a-3c25-4b5d-aa01-18f7f4804f95.png">

These predictions refer to: 
* **Splice Site**: This refers to predicting where on the pre-mRNA a splice will occur; the possibilities consist of yes or no for a splice site.  
* **Probability**: 
* **Tissue-Specific**: Splicing can vary depending on the tissue it is performed in, meaning many alternative sequences from the same root DNA. Common tissues this occurs in are the brain, testis, heart and liver. More information about this feature can be found on this background information page. 
* **Splicing Efficiency**: 

## Setting up a Google Colab Notebook 

Some of these tools are offered for the public to use on GitHub, with the option of running the code on Google Colab, which will be the focus of this page. To copy any of the tools to your own Colab Notebook, go to:
```
file -> save a copy in drive 
```

Now that you have created your own copy of the notebook, you can freely make changes and save them. 

## Pangolin 
### Preprocessing

No specific preprocessing required. 

### Usage 

Pangolin can be executed using a single command from either the command line (if downloaded to computer) or in a Google Colab notebook. Here’s an example: 
```
pangolin examples/brca.vcf GRCh37.primary_assembly.genome.fa.gz gencode.v38lift37.annotation.Ensembl_canonical.db brca_pangolin
```
Other Usage options include: 
```
usage: pangolin [-h] [-c COLUMN_IDS] [-m {False,True}] [-s SCORE_CUTOFF] [-d DISTANCE] variant_file reference_file annotation_file output_file

positional arguments:
  variant_file          VCF or CSV file with a header (see COLUMN_IDS option).
  reference_file        FASTA file containing a reference genome sequence.
  annotation_file       gffutils database file. Can be generated using create_db.py.
  output_file           Prefix for output file. Will be a VCF/CSV if variant_file is VCF/CSV.

optional arguments:
  -h, --help            show this help message and exit
  -c COLUMN_IDS, --column_ids COLUMN_IDS
                        (If variant_file is a CSV) Column IDs for: chromosome, variant position, reference bases, and alternative bases. Separate IDs by commas. (Default: CHROM,POS,REF,ALT)
  -m {False,True}, --mask {False,True}
                        If True, splice gains (increases in score) at annotated splice sites and splice losses (decreases in score) at unannotated splice sites will be set to 0. (Default: True)
  -s SCORE_CUTOFF, --score_cutoff SCORE_CUTOFF
                        Output all sites with absolute predicted change in score >= cutoff, instead of only the maximum loss/gain sites.
  -d DISTANCE, --distance DISTANCE
                        Number of bases on either side of the variant for which splice scores should be calculated. (Default: 50)
```

### Accuracy 

Pangolin has been shown to have a higher AUPRC score than pre-existing models and while its its tissue-specific prediction abilities are low, they are higher than MTSplice [1](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-022-02664-4).

### Example Prediction 
Here is an image of Pangolin’s prediction run on the breast cancer variant gene. 

<img width="618" alt="Screen Shot 2022-08-23 at 3 25 47 PM" src="https://user-images.githubusercontent.com/98296345/186252419-01fce74e-5f7b-4fe9-9ee0-0d7e1edafeec.png">

### How to Interpret the Results 

The output file is formatted as `gene|pos:largest_increase|pos:largest_decrease|`.This means that the default predictions will report the max increase and decrease in score and positions for 50 bases around the variant. 

Currently, only reports substitutions and deletions and if the variants are not defined by the annotation file, they are skipped. 

## MTSplice 
### Preprocessing

Preprocessing for MTSplice requires three separate steps: 
Filtering the quality of the variants as low quality one can lead to unreliable predictions. One way this can be done is by using Bcftools through pre and post-call filtering. For example:
* `-A`: for keeping possible alternate alleles at the variant site 
* `-V TYPE`: to skip TYPE. 

Splitting multiple variants into separate lines. Example command using bcftools (set of commands that work in VCF files to manipulate variant information): 
`bcftools norm -m-both -o out.vcf in.vcf.gz`
Left-normalization which is shifting the position of a variant to the leftmost position possible. An example is GGCA-->GG which is not left-normalized while GCA-->G is. Example command using bcftools: 
`bcftools norm -f reference.fasta -o out.vcf in.vcf` 

### Usage 
MMSplice can be used in a Google Colab environment, which is offered on the project’s GitHub page. To use MMSplice (the non-tissue specific version), the model can be run with the various input files in a set of commands like this: 
```
dl = SplicingVCFDataloader(genome_version, fasta, vcf)
``` 
Note: where d1 is the reference gene annotation file.
``` 
model = MMSplice()
output_csv = 'preds.csv'
predict_save(model, dl, output_csv, pathogenicity=True, splicing_efficiency=True)
```
In addition, certain post-processing steps can also be made using pandas, as seen in the Google Colab notebook. 

Other usage parameters include: 
* To have tissue-specific predicting, set `tissue_specific=True` in `SplicingVCFDataloader`. For example:
```
dl = SplicingVCFDataloader(gtf, fasta, vcf, tissue_specific=True)
```

### Accuracy 

MTSplice is one of the more accurate current RNA splicing tools, however a cassette extron based model may prove to be ineffective when predicting complex mutations that affect multiple splice sites. 

In addition, since the model was trained using exonic variants, only exonic variant predictions are made. 

### Example Prediction 

<img width="641" alt="Screen Shot 2022-08-23 at 3 25 55 PM" src="https://user-images.githubusercontent.com/98296345/186252422-0047210a-ef22-4c84-a79d-d27dcc05b9f1.png">

### How to Interpret the Results 

As seen in the example above, the output consists of many columns, each with their own meaning: 
* `ID`: id string of the variant
* `delta_logit_psi`: The main score is predicted by MMSplice, which shows the effect of the variant on the inclusion level (PSI percent spliced in) of the exon. The score is on a logit scale. If the score is positive, it shows that the variant leads to a higher inclusion rate for the exon. If the score is negative, it shows that the variant leads to a higher exclusion rate for the exon. If delta_logit_psi is bigger than 2 or smaller than -2, the effect of the variant can be considered strong.
* `exons`: Genetics location of exon whose inclusion rate is affected by variant
* `exon_id`: Genetic id of exon whose inclusion rate is affected by variant
* `gene_id`: Genetic id of the gene which the exon belongs to.
* `gene_name`: Name of the gene which the exon belongs to.
* `transcript_id`: Genetic id of the transcript which the exon belongs to.
* `ref_acceptorIntron`: acceptor intron score of the reference sequence
* `ref_acceptor`: acceptor score of the reference sequence
* `ref_exon`: exon score of the reference sequence
* `ref_donor`: donor score of the reference sequence
* `ref_donorIntron`: donor intron score of the reference sequence
* `alt_acceptorIntron`: acceptor intron score of variant sequence
* `alt_acceptor`: acceptor score of the sequence with variant
* `alt_exon`: exon score of the sequence with variant
* `alt_donor`: donor score of the sequence with variant
* `alt_donorIntron`: donor intron score of the sequence with variant
* `pathogenicity`: Potential pathogenic effect of the variant.
* `efficiency`: The effect of the variant on the splicing efficiency of the exon.
*Note: this list is directly from the MMSplice GitHub.* 

## SpliceAI

### Preprocessing

No specific preprocessing required. 

### Usage 
The easiest way to install SpliceAI is using pip or conda with this command: 
```
pip install spliceai
# or
conda install -c bioconda spliceai
```
However, it can also be installed from the github repository. In terms of running SpliceAI, it can be done so form the command line using: 
```
spliceai -I input.vcf -O output.vcf -R genome.fa -A grch37
# or you can pipe the input and output VCFs
cat input.vcf | spliceai -R genome.fa -A grch37 > output.vcf
```
Here are the required parameters, directly from the project’s github page:
* `-I`: Input VCF with variants of interest.
* `-O`: Output VCF with SpliceAI predictions `ALLELE|SYMBOL|DS_AG|DS_AL|DS_DG|DS_DL|DP_AG|DP_AL|DP_DG|DP_DL` included in the INFO column (see table below for details). Only SNVs and simple INDELs (REF or ALT is a single base) within genes are annotated. Variants in multiple genes have separate predictions for each gene.
* `-R`: Reference genome fasta file. Can be downloaded from [GRCh37/hg19](http://hgdownload.cse.ucsc.edu/goldenPath/hg19/bigZips/hg19.fa.gz) or [GRCh38/hg38](http://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz).
* `-A`: Gene annotation file. Can instead provide `grch37` or `grch38` to use GENCODE V24 canonical annotation files included with the package. To create custom gene annotation files, use `spliceai/annotations/grch37.txt` in the repository as a template.

### Accuracy 

A major advantage of SpliceAI is its accuracy and its ability to predict if a particular site on a m-RNA is a splice donor, splice acceptor or neither using any genomic sequence input. In addition, its large prediction distance along the gene greatly increases its accuracy and ability. For example, the neural network can predict with up to 95% top-k accuracy for pre-mRNA transcripts in the training dataset and has an 85% top-k accuracy for long noncoding RNAs

### Example Prediction 

<img width="642" alt="Screen Shot 2022-08-23 at 3 26 02 PM" src="https://user-images.githubusercontent.com/98296345/186252423-e05f4656-5acc-453e-a26e-9dd48377267b.png">

### How to Interpret the Results 

As shown above, each variant has an associated “INFO” column with a series of numbers. The first number is the increase in the probability that the position, which can be found from the “POS” column, is used as a splice site acceptor. The second value is the decreased probability that the site is used as an acceptor. 

For example, take the first row of the “INFO” column: 
```
SpliceAI=A|NEB|0.01|0.00|0.00|0.74|43|3|-26|3,C|NEB|0.04|0.00|0.00|0.71|43|3|-26|3,G|NEB|0.03|0.00|0.00|0.75|43|3|-26|3
```
Here, 0.01 is the increase and 0.00 is the decrease in the probability that the site is used as an acceptor. 

## Another Current Tool
Apart from the three tools listed above, there are other tools in the field at this moment that are also efficient and accurate at predicting RNA splicing. For example, a tool developed by Thanyathorn Thanapattheerakul, Worrawat Engchuan and Jonathan H. Chan​ uses convolutional neural networks to predict splicing. The github repository for this tool can be found [here](https://github.com/smiile8888/rna-splice-sites-recognition). 

In addition, the study associated with this tool found that CNN based models performed much better than the non-CNN models. Also that this specific CNN model was found to have room for improvement in predicting negative splicing sequences. Although the model is able to distinguish pathogenic and benign variants to a certain extent. 


## Glossary 
* Gene Transfer File (GTF): a type of file formatting that is used for storing information about genetic structure. 
* Neural Networks: computing algorithms modelled after human neural connections in the brain. 
* Deep Learning: a field of computing concerned with developing algorithms and programs that learn the way humans do
* Area Under the Precision Recall Curve (AUPRC): Known as AUPRC is a metric for binary responses used to measure the prediction accuracy of a technology.
* Cassette Exons: intervening exons that can be excluded or skipped and generate distinct protein results. 
* Pre-mRNA: Precursor messenger RNAs (or Pre-mRNA) communicate information from DNA to protein synthesizing units abou how to build the target protein. 
* Alternative Splicing: different splice sites that allow for a single parent gene to code for many different proteins. 
* Weights: In the context of deep learning weights are numerical values that represent the strength of the connection between two neurons. 
* Nodes: a computational unit made of an input, transfer connection and output. 
* Convolutional Neural Networks: is a type of neural network that processes data in a grid-like format like an image by assigning importance scores and then learning. 

## References 
* Zeng, T., Li, Y.I. Predicting RNA splicing from DNA sequence using Pangolin. Genome Biol 23, 103 (2022). https://doi.org/10.1186/s13059-022-02664-4 
* Kishore Jaganathan, Sofia Kyriazopoulou Panagiotopoulou, Jeremy F. McRae, ..., Serafim Batzoglou, Stephan J. Sanders, Kyle Kai-How Farh. “Predicting splicing from primary sequence with deep learning”. Cell. (n.d.). Retrieved June 20, 2022, from https://www.cell.com/cell/fulltext/S0092-8674(18)31629-5 
* Cheng, J., Çelik, M.H., Kundaje, A. et al. MTSplice predicts effects of genetic variants on tissue-specific splicing. Genome Biol 22, 94 (2021). https://doi.org/10.1186/s13059-021-02273-7 
* Thanapattheerakul T, Engchuan W, Chan JH. 2020. Predicting the effect of variants on splicing using Convolutional Neural Networks. PeerJ 8:e9470 https://doi.org/10.7717/peerj.9470 
