# A sigma-54 promoter predictor in prokaryotic genomes based on a machine learning method
## Abstract
Sigma factor, as a unit of RNA polymerase holoenzyme, is a critical factor in the process of gene transcriptional regulation. It recognizes the specific DNA sites and brings the core enzyme of RNA polymerase to the upstream regions of target genes. Therefore, the prediction of the promoters for a particular sigma factor is essential for interpreting functional genomic data and observation. This paper develops a new method to predict sigma-54 promoters in bacterial genomes. The new method organically integrates motif finding and machine learning strategies to capture the intrinsic features of sigma-54 promoters. The experiments on E. coli benchmark test set show that our method has good capability to distinguish sigma-54 promoters from surrounding or randomly selected DNA sequences. The applications of other three bacterial genomes indicate the potential robustness and applicative power of our method on a large number of bacterial genomes. 

**Citing Us:** Bingqiang L, Ling H, Xiangrong L, Jichang W, Qin M. Computational prediction of sigma-54 promoters in bacterial genomes by integrating motif finding and machine learning strategies. *IEEE/ACM Transactions on Computational Biology and Bioinformatics* 
2018;PP(99):1-1. doi: 10.1109/TCBB.2018.2816032
## Environment
Linux system is recommended. Ubuntu 18.04.2 LTS is used for testing. (5/10/2019)

# Usage
## Installation

Firstly, download MRMD to your working path from the website http://lab.malab.cn/soft/MRMD/index.html or use the code below in Unix:

```
cd /your/working/path/
wget http://lab.malab.cn/soft/MRMD/mrmd.jar
```
Then download the zip file manually from github, or use the code below in Unix:
```
wget https://github.com/OSU-BMBL/PromotePredictor/archive/master.zip
```
Unzip the file:
```
unzip master.zip && rm -rf master.zip
```
Move the MRMD to the master folder and enter the folder.
```
mv mrmd.jar ./PromotePredictor-master
cd ./PromotePredictor-master
```
[WEKA](https://www.cs.waikato.ac.nz/~ml/weka/ "WEKA") should be used to further process the final result.

## Obtain the characteristic matrix

This step can obtain the characteristic matrix of each sample in the 79-dimensional feature,which can convert fasta file to arff file.

An example usage is like this:
```
java -jar extractor.jar NC_000964_sigma54_81_non.fasta NC_000964_sigma54_81.fasta result_feature.arff
```

The general command of this step is following:
```
# This command won't actually execute.
# java -jar extractor.jar neg.fa pos.fa result_feature.arff
```



#### Inputs

The format of input file is fasta
The example of input file:


>\>96_55_2762890_-_TTGGCACGATCCTTGCA_16079761_levD_81
>TAAGTGTTTCAACAACAAATTGCTATTGGCTGAAATAACAATGAAAACGCTTAACACAACTGTGTTGGCACGATCCTTGCA

#### Outputs

The format of output file is arff
The example of output file:


>@RELATION 727
>@ATTRIBUTE 0 NUMERIC
>@ATTRIBUTE 1 NUMERIC
>@ATTRIBUTE 2 NUMERIC
>@ATTRIBUTE 3 NUMERIC
>@ATTRIBUTE 4 NUMERIC
>@ATTRIBUTE 5 NUMERIC
>...
>
>@ATTRIBUTE 203 NUMERIC
>@ATTRIBUTE class {0,1}
>@data
>0.5541,.......,0.5,0.5,1
>0.66621,........0.12332,0.342114,0


**Note: the number 1 or 0 in the end of each line indicates whether this sequences is a promoter or not.** 

## Dimension reduction

MRMD can reduce the dimension of the input file.

In our example, we could use this command to reduce the dimension of our result_feature.arff
```
java -jar mrmd.jar -i result_feature.arff -o output.txt
```


For more usage of MRMD, you can visit it's [website](http://lab.malab.cn/soft/MRMD/index.html "website").


#### Inputs

The format of the input file is arff.(as above)

#### Outputs

The result file will be in an arff file and "output.txt";

The data of the reduction is in the arff file;

The data in result file output.txt  have 4 columns with means:
  
(1) The number selected features

(2) The first column is the index

(3) The second column is the feature name

(4) The third column is the score

## Training model

Import the final arff file to WEKA and train the model.


## Contact

Any questions, problems, bugs are welcome and should be dumped to
Qin Ma <Qin.Ma@osumc.edu>
Creation: JAN. 6, 2018
