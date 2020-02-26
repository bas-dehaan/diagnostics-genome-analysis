---
title: "Project Logbook"
author: "Geke Teitsma"
date: "2/14/2020"
output:
  html_document:
    df_print: paged
---

Date: 14 February 2020

## 1. ASCII codes

What: 
  To determine the quality of the given data, ASCII code can be used. Every base is assigned a code that matches a specific value. Each of these values lead to a differet accuracy level. This is done for the first 10 known bases in a data set. 
A data point is said to have a proper quality if the base call accuracy is equal or higher than 99.9, meaning th numerical score has to be at least 30.
Why: 
  The ASCII codes are used to be able to determine whether or not the data is reliable. Using the ASCII values an accuracy percentage can be calculated. 
Outcome: 
  The results of the analysis can be seen in the table below.


| Base | N | T | C | A | T | G | T | A | C | G |
|---|---|---|---|---|---|---|---|---|---|---|
| Quality char| # | > | > | 1 | A | 1 | B | 3 | B | 1 |
| Numerical score (ASCII value - 33) (Q) | 2 | 29 | 29 | 16 | 32 | 16 | 32 | 16 | 33 | 18 | 33 | 16 | 
|Base call accuracy (1-P) (P = 10^(-Q/10)) | 36.9 | 99.87 | 99.87 | 97.49 | 99.94 | 97.49 | 99.95 | 98.42 | 99.95 | 97.49 |
|Acceptable accuracy | No | No | No | No | Yes | No | Yes | No | Yes | No | Yes | No | 

Conclusions: 
  From the table one can draw some conclusions. The quality ofseveral bases do not have the requirements to be said accurate. Moreover, only 4 values have the right conditions. Therefore this data set should not be used to continue with, since the quality of the set is not as accurate as supposed to. 


## 2. Fastqc files of the raw data

The raw data is put in a fastqc file to determine the quality per base pair. 

![Fastqc for patient 2, R1](/homes/gjteitsma/Desktop/images/raw_data_R1.png)

![Fastqc for patient 2, R2](/homes/gjteitsma/Desktop/images/raw_data_R2.png)

Both the R1 and the R2 strand show areas with fluctiation. R1 shows less accurate results at the end of the reads. Although this is as expected with Illumina sequecing, the value drops below the acceptance point. 
R2 however shows very low accuracies over the entire sequence. 

To be able to work with the data the data will be tweaked. Using various options of the Trimmomatic tool from Galaxy an attempt has been made to make the data workable. 
Two aspects were used to tweak the data: The minimum quality and the minimum read length. 
The reason these two aspects are tweaked with is the following:

* Minimum quality: The quality needs to be altered to obtain results. Quality values below a certain range are not accurate enough, since a large part of the sequenced data will be assigned wrong base. 
* Minimum read length: One does not want to many short reads, since they can interfere with the longer reads and cause various misinterpretations of the data. 

## 3. Read trimming




|Attempt | Number of sequences | Minimum quality | Minimum read length | Sequences lost from initial value|Coverage| Conclusion |  
| --- | ---| --- | --- | --- | --- | --- |
|1 | 1,298,979 | N/A | N/A | N/A | 1218 | Initial data set |
|2 | 910,105 | 20 | 70 | 388,874 | 853 | First trimming step. First bp shows very low quality (18) | 
|3 | 644,445 | 26 | 70 | 654,534 | 604 | All positions above 30 quality score  | 
|4 | 899692 | 20 | 75 | 399287 | 843 | No variation from the second attempt  | 
|5 | 852698 | 20 | 100  | 446281 | 799 | Hardly any variation of the fastQC plot in comparison to the second attempt  | 
|6 | 1072839 | 20 | 20 |  226140 | 1006  | The overall mean quality is lower than the mean value at attempt 2 | 
|7 | 448598 | 30  | 70 |  | 421 |  All qualities at least 32 | 




![Tweaking for patient 2, R1. Mininum quality = 20, minimal read length = 70](/homes/gjteitsma/Desktop/images/Tweaking_R1_Mini_quality_=_20,minimal_read_length=70.png)

![Tweaking for patient 2, R2. Minimal quality = 20, minimal read length = 70](/homes/gjteitsma/Desktop/images/Tweaking_R2_Mini_quality_=_20,minimal_read_length=70.png)

![Tweaking for patient 2, R1. Mininum quality = 26, minimal read length = 70](/homes/gjteitsma/Desktop/images/Tweaking_R1_Mini_quality_=_26,minimal_read_length=70.png)

![Tweaking for patient 2, R2. Minimal quality = 26, minimal read length = 70](/homes/gjteitsma/Desktop/images/Tweaking_R2_Mini_quality_=_26,minimal_read_length=70.png)


Date: 26 February 2020

splice variant - choose what exon combination you want. 
the info for this skipping is in the 20 bp regions on both sides. 


To continue the project the settings of minimum quality = 26 and minimum read length = 70 are used. 
This is so all the positions show proper quality scores, since all are in the green range. 

## CHAPTER 4


Assignment 4: 
    Using the settings 644,445 reads were left. 
    
Using the Lander/Waterman equation the coverage can be determined. 

$C=\frac{LN}{G}$

Where:

* C = Coverage
* L = Read Length
* N = Number of Reads
* G = Captured Region

If: C= 20, N = 25 million and L = 300, G can be calculated as follows:

$G=\frac{LN}{C}=\frac{300*25,000,000}{20}=3.75*e^{6}$

By creating the read duplicates can arise, which do not origin from the sample, but are technical. These duplicates can possibly generate false positive variants. This is the case since one sample will technically be used twice. If this original read 


Assignment 5: Visualizing the Mapping Data






p


To do: DONT FORGET TO DO THE FORMULA
