Doppelganger effect (DE) is when independently-derived data are highly similar due to chance, and these samples are separated across training and validation dataset, leading to consequences of inflated machine learning (ML) performance. The resulted classifier is overfitted to the FD and less generalized to other dataset.  

One of the reasons that DE is abundant in biological data is because of data integration. To address the limited availability of biological samples, it is a common practice of reanalysis of tissue samples between research groups or combining available datasets by bioinformaticians from multiple studies to increase statistical power and generalizability of the trained model. Since those specimens are deposited to the database using identifiers, which it’s not possible for the researchers to trace back to the source, causing these duplicated data to be undiscovered.  

Moreover, detection of DE is even more challenging due to batch effect, which comes from technical variations or different data preprocessing methods from independent experimenters or across studies. Hence, when multiple datasets are integrated for ML, batch correction is necessary prior to data doppelganger identification.  

One possible way to detect such duplicated data has been demonstrated by Sheng et. al. (2014). MD5 hash for each gene expression raw data file is generated to detect the potential of duplications despite the different accession number entries in the public database.  

Other than that, Waldron et. al. (2016) has developed R package doppelgangR that performs Pairwise Pearson comparison analysis. Using batch-corrected Pairwise Pearson correlation coefficient, transcriptome sample pairs with unusually high correlation are identified as duplicated samples due to sharing of specimens between collaborating research groups. Nevertheless, this could only deal with technical replicates or samples from data leakage but not doppelgangers that are simply similar by chance.  

A recent paper by Wang et. al. (2022) has demonstrated DE identification on single renal cell carcinoma (RCC) proteomics data set, using various correlation metrics including Pairwise Kendall Rank Correlation Coefficient (PKRCC), pairwise Pearson’s correlation coefficient (PPCC) , Pairwise Spearman Rank Correlation Coefficient (PSRCC). Their performance on identifying DD are evaluated, however selecting the best metrics is dependent on the nature of dataset, required stringency and sensitivity.

As mentioned by Wang et. al. (2022b), DE is present in protein sequences and structure studies, as proteins sharing similarity in primary sequences often share the same functionality. Hence, a threshold of protein sequence identity is set to exclude homologous proteins, for instance in hidden Markov model to remove distantly related proteins. However, this alone is insufficient, as there are proteins with rather weak similarity in sequences but share the same function, or the other way, homologous proteins could exhibit different functions. 

Other than transcriptomics, DE could also be present in other types of biomedical data, such as bio-imaging analysis, when images with the same artefact such as deformation originated from experimental procedure are distributed across training and testing dataset.	The pattern of artefact was learned by the model, leading to misclassification of features.

In my opinion, doppelganger effect is not unique to biomedical data. One example would be targeted advertisements based on users’ browsing history and other internet activities. A particular set of activities, such as A followed by B action that is detected in users by chance but has no actual association, yet the pattern is learned by the ML model and hence the next user who performed the first action will be predicted to be interested in the second action B.  


**Reference**
 Sheng, Q., Shyr, Y. & Chen, X. DupChecker: a bioconductor package for checking high-throughput genomic data redundancy in meta-analysis. *BMC Bioinformatics* 15, 323 (2014).
 
Waldron, L., Riester, M., Ramos, M., Parmigiani, G., & Birrer, M. (2016). The doppelgänger effect: hidden duplicates in databases of transcriptome profiles. *JNCI: Journal of the National Cancer Institute*, 108(11).

Wang, L. R., Choy, X. Y., & Goh, W. W. B. (2022). Doppelgänger spotting in biomedical gene expression data. *Iscience*, 25(8), 104788.

Wang, L. R., Wong, L., & Goh, W. W. B. (2022b). How doppelgänger effects in biomedical data confound machine learning. *Drug Discovery Today*, 27(3), 678-685.


