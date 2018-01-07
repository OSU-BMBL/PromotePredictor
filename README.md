
Usage

Note: The computer you use should have WEKA and MRMD installed. The WEKA's
installation site is http://lab.malab.cn/soft/MRMD/index.html

CMD line


$ java -jar extractor.jar neg.fa pos.fa feature.arff

extractor.jar can obtain the characteristic matrix of each sample in the 79-dimensional feature,which can convert fasta file to arff file


==================
Inputs and outputs
==================

The format of input file is fasta
The example of input file:

-----

>96_55_2762890_-_TTGGCACGATCCTTGCA_16079761_levD_81
TAAGTGTTTCAACAACAAATTGCTATTGGCTGAAATAACAATGAAAACGCTTAACACAACTGTGTTGGCACGATCCTTGCA

-----

The format of output file is arff
The example of output file:

-----
@RELATION 727
@ATTRIBUTE 0 NUMERIC
@ATTRIBUTE 1 NUMERIC
@ATTRIBUTE 2 NUMERIC
@ATTRIBUTE 3 NUMERIC
@ATTRIBUTE 4 NUMERIC
@ATTRIBUTE 5 NUMERIC
...

@ATTRIBUTE 203 NUMERIC
@ATTRIBUTE class {0,1}
@data
0.5541,.......,0.5,0.5,1
0.66621,........0.12332,0.342114,0
....

Note: the number 1 or 0 in the end of each line indicates whether this sequences is a promoter or not. 
==================
Result
==================

Import the file to WEKA and Using the trained model(specific training steps are as follows) judege the imported file(the format of the imported file must be arff,the conversion of the format are as above)



========================================
Supplement
========================================
1)Dimensional-reduction

$ java -jar mrmd.jar -i input -o output

mrmd.jar can reduce the dimension of the input file and save the result to the
file of output.txt 

==================
Inputs and outputs
==================

The format of the input file is arff.(as above)

==================
Results
==================
The result file will be in file "feature_MRMD_79.arff" and "output.txt";

The data of the reduction is in "feature_MRMD_79.arff";

The data in result file output.txt  have 4 columns with means:
(1) The number selected features
(2) The first column is the index
(3) The second column is the feature name
(4) The third column is the score

2)Taining model

Import the file "feature_MRMD_79.arff" to WEKA and train the model.

==================
Contact
==================
Any questions, problems, bugs are welcome and should be dumped to
Qin Ma <Qin.Ma@sdstate.edu>
Creation: JAN. 6, 2018

#---------------------------------------------------------------------------#
