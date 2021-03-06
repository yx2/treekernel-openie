%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%                                                                                                 %
%                                       Code                                                      %
% Open Information Extraction with Tree Kernels                                                   %
% Ying Xu, Mi-Young Kim, Kevin Quinn, Randy Goebel and Denilson Barbosa      					  %
% NAACL2013                                                                          		      %
%                                                                                                 %
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

To extract relation candidates: in application/ExRECandidate.java. 
Input: files with raw sentences, one sentence per line.
output: the NE pairs and candidate relations. (I only keep PER, ORG, LOC, if you want all NEs from Stanford NE extraction, you can change the code: comment out" mentionList = this.filterMention(mentionList);")

You can also use your own NE and relation candidates extraction, and use the tree extraction code for SVM Tree Kernels I provided.
Just make sure the input is the same as the ExRECandidate.java
 
To use the SVM Tree Kernel and vector feature (step 1, 2, 3)
To use the SVM Tree Kernel only (step 1)

1. get the tree kernel representation:
    parseFilter/DataTransformSVMwithR.java
    
    input:
    path: path of the files
    file: the tagged data file
    outF: the tree representation file
    outFMap: the tree representation with corresponding triple.
    
    You can change the code for input file names. 
    or use the command
    DataTransformSVMwithR path file outF outFMap

2. get the vector features:
    parseFilter/DataTransformSVMFlat.java
    input: 
    path
    file: the tagged 
    outF: the result feature file (not the vector yet, features are still strings)
    FMapF: the feature to int id map file.
    outSVM: the final vector file
    outSVMMap: the vector with the triple.
      
    Note that here the training and testing are a little bit different.
    For training: you need functions: extractF() getFeatureMap(), transform()
    for testing: you need comment out the getFeatureMap()
    
    Or you can use the command:
    DataTransformSVMFlat train path file outF FMapF outSVM outSVMMap
    
    DataTransformSVMFlat test path file outF FMapF outSVM outSVMMap

3. DataTransformSVMTandV
    Now you can combine the two results file into training and testing files for SVM.
    input:
    path:
    file: the tree kernel file
    inSVMMap: the vector kernel file with the triple (outSVMMap in the previous process.)
    outF: final output, which can be the input to the SVM.
