# Dengue Fever Prediction Analysis with Machine Learning

# Abstract
Summary: This report conducted an integrative analysis of gene expression data from samples across a spectrum of dengue infection states: dengue fever (DF), dengue haemorrhagic fever (DHF), convalescent individuals, and healthy controls.
Aims: The aim was to characterise gene expression profiles associated with different dengue infection states and evaluate the ability of machine learning models, particularly Support Vector Machines (SVMs), in classifying and distinguishing between DF and DHF.
Methods: The investigation used principal component analysis (PCA) and hierarchical clustering analysis (HCA) to explore the variability of gene expression. Volcano plots were used to identify significantly differentially expressed genes. An SVM classifier was developed and validated using bootstrap resampling to predict disease status.
Results: PCA and HCA revealed significant variability in gene expression between disease states. Volcano plots identified key genes with altered expression, implicating biological processes disrupted by dengue infection. The SVM classifier achieved an average accuracy of 67%, demonstrating the potential of using transcriptomic data in differentiating between DF and DHF.
Conclusion: The research highlighted the complexity of gene expression changes in dengue infection and highlighted the need for large datasets for effective application of machine learning. The significant genes identified could serve as biomarkers for disease status and severity, offering a basis for future diagnostic and therapeutic development. The study concludes that, although promising, the current approach requires further refinement and data enrichment to realize its full clinical potential.

# Introduction
This report conducts a comprehensive gene expression analysis of dengue fever, using data from the GEO GDS5093 dataset, which includes samples from four distinct patient groups: dengue fever (DF), dengue haemorrhagic fever (DHF), convalescent individuals and healthy controls. This study, enriched by insights such as monocyte population dynamics in DENV infection, seeks to explore the molecular responses to DENV in these groups and identify gene expression correlates via transcriptomic analysis from DNA microarrays (1).
Dengue fever, a globally widespread mosquito-borne disease, poses significant challenges in terms of treatment and prevention due to its varied clinical manifestations and the absence of targeted antiviral therapies (2, 3). Using bioinformatics and machine learning methods including PCA, HCA, and SVM, this investigation aims to analyse gene expression changes and evaluate the potential of transcriptomics in differentiating clinical states of dengue. These techniques are critical for deciphering the intricate gene expression patterns associated with dengue infection, offering prospects for the development of diagnostic and therapeutic approaches.

# Methods

Principal Component Analysis (PCA)

PCA is used as a dimensionality reduction and data visualisation technique. This method transforms a set of possibly correlated variables into a smaller number of uncorrelated variables, known as principal components (PCs). Gene expression data were transposed to position samples as rows and genes as columns. The transposed data was then merged with the metadata using the "sample" column of the metadata and the index of the transposed data. PCA was performed on the numerical gene expression data, selecting the top 10 principal components. The variance ratio of each component was calculated to evaluate the contribution of each principal component to the variance in the data set. A scatterplot was generated using the seaborn and Matplotlib libraries in Python to visualise the data in low- dimensional space, coloured by disease state.

Hierarchical Cluster Analysis (HCA)

Hierarchical clustering was used to divide the dataset into subsets based on the similarity of observations. Using Euclidean distance, the Ward method was applied to perform clustering. The data were merged before clustering and hierarchical clustering was calculated on the transposed gene expression data. The results were visualised as a dendrogram using Matplotlib, with branches coloured according to the disease state of each sample to facilitate easy interpretation of the clustering results.

Differential gene expression analysis

Differential gene expression analysis was conducted using univariate statistical tests. T-tests were performed between all pairs of disease states to identify genes with significant differences in expression. The p values obtained from these tests were adjusted for multiple testing using the false discovery rate (FDR) method. Volcano plots were created for each pairwise comparison, plotting the log2 fold change against the -log10 adjusted p values. This visualisation highlighted genes with significant differential expression.

Supports Vector Machine (SVM) classifier and bootstrap analysis
The methods employed in this study involved selecting dengue fever and dengue haemorrhagic fever patient samples from the GDS5093 dataset, coding their disease states for analysis, and preparing gene expression data. A Support Vector Machine classifier with a linear kernel was trained and tested on this data, with performance evaluated through accuracy scores and a confusion matrix, visualized via heat map. Bootstrap validation with 100 iterations provided a reliable measure of model reliability, producing an average precision to reflect the consistency of the classifier.

# Results

Principal component analysis of gene expression data

The gene expression profiles of the samples from the four populations – those with dengue fever, dengue haemorrhagic fever, convalescent, and healthy controls – were subjected to principal component analysis (PCA) to ascertain the extent of their differences. PCA revealed that the first two principal components (PC1 and PC2) accounted for 21.23% and 8.59% of the variance, respectively, indicating substantial but incomplete separation between disease states based on gene expression patterns.
The resulting PCA scatterplot (Figure 1) illustrates the distribution of samples in the space defined by PC1 and PC2. Notably, there is a visible distinction between the groups, with some overlap, particularly between convalescent and dengue fever samples, suggesting similarities in their gene expression profiles. In contrast, healthy controls cluster distinctly from dengue fever and dengue haemorrhagic fever samples, reflecting significant differences in gene expression profiles associated with disease states.

<img width="940" alt="Screenshot 2024-05-17 at 11 20 51" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/3a2b13fd-61e8-441a-a3e8-8c1c3cf30e84">

The explained variance ratios for the first ten principal components were as follows: PC1 - 21.23%, PC2 - 8.59%, PC3 - 6.32%, PC4 - 4.32%, PC5 - 3.30%, PC6 - 2.80%, PC7 - 2.21%, PC8 -1.99%, PC9 - 1.90% and PC10 - 1.73%. These components cumulatively account for approximately 53.39% of the total variance in the dataset, indicating that while the first two components capture the most variance, additional components contribute to nuanced differences in gene expression between patient groups.

Hierarchical clustering analysis

Hierarchical clustering analysis (HCA) was performed to evaluate the extent of differences in gene expression profile between the four populations. The Ward method, which minimizes the total variance within the cluster, was used together with the Euclidean distance metric to measure the similarity between gene expression profiles.

The HCA-generated dendrogram (Figure 2) depicts a clear separation between disease states, with each branch representing a cluster of samples. Samples from healthy controls formed a distinct cluster, significantly differentiated from other populations, indicative of a unique gene expression profile in the absence of disease. Notably, there was a degree of separation between the DF and DHF groups, while convalescent individuals showed varying degrees of similarity to both active disease states.

<img width="935" alt="Screenshot 2024-05-17 at 11 20 32" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/26fe84c2-5c26-4a91-aea9-a3de862c5560">

The clusters corresponding to the DF and DHF populations suggest a relationship between gene expression profiles and disease severity. Convalescent samples interspersed with these clusters suggest a pattern of transient gene expression as patients recover from dengue infections.
Hierarchical clustering then reveals the distinct patterns of gene expression profiles associated with each disease state, providing a visual representation of the underlying molecular differences. This exploratory method of data analysis demonstrates the potential of gene expression profiling to distinguish between different clinical manifestations of dengue fever, which could be instrumental in improving diagnosis and understanding of disease progression.

Differential gene expression analysis

To ascertain the gene expression changes in the four disease states, differential gene expression analysis was conducted. T tests were performed to compare each pair of disease states, and p values were adjusted for multiple comparisons using the false discovery rate (FDR) approach.
Convalescent vs Dengue Haemorrhagic Fever samples
The analysis produced a series of volcano plots, one of which compares convalescent individuals with patients suffering from dengue haemorrhagic fever (Figure 3). Volcano plots serve as a powerful visualization tool to show the relationship between fold changes in gene expression and statistical significance. In the graph, the horizontal axis shows the log2 fold change, while the vertical axis represents the negative logarithm of the corrected p-value, which intensifies the visual impact of highly significant genes.

<img width="931" alt="Screenshot 2024-05-17 at 11 20 10" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/4d8f5155-7b7c-4317-b25f-301a14f58a59">

When comparing convalescent individuals and dengue haemorrhagic fever patients, several genes were identified as significantly differentially expressed (p-value threshold < 0.05 and absolute log2-fold change > 0.58) (Table 1). CDC6, TTK, PBK, KCTD14, and AI401105 genes demonstrated upregulation, while CNTNAP3B showed downregulation in dengue haemorrhagic fever compared to the convalescent state.

<img width="946" alt="Screenshot 2024-05-17 at 11 19 55" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/43412103-c3ff-4811-88d7-034ec1b9f184">

The findings indicate a marked difference in the expression of some genes when comparing convalescent states with active disease, which may contribute to understanding the pathophysiology of dengue haemorrhagic fever and the recovery process.

Convalescent vs Dengue Fever samples

A volcano plot was constructed to visualize differential gene expression between convalescent individuals and dengue fever patients. The graph highlights genes with statistically significant differences in expression levels, where the x- axis represents the log2 fold change and the y-axis shows the negative log10 of the adjusted p-value.
In Figure 4, significant genes are marked in red, in contrast to the majority, which is showed in grey. The vertical lines indicate the fold change thresholds, while the horizontal line represents the significance level. Moreover, genes located in the upper right and upper left corners of the graph show both high levels of fold change and statistical significance.

<img width="931" alt="Screenshot 2024-05-17 at 11 19 39" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/a55a87e6-b473-4864-8961-135566c9a8eb">

The analysis identified three genes – CDC6, PBK and KCTD14 – significantly upregulated in dengue fever patients compared to convalescent individuals. The adjusted p-values for these genes were well below the significance threshold, suggesting a strong association with the disease state.

<img width="805" alt="Screenshot 2024-05-17 at 11 19 15" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/fa0b1730-c8de-46f3-80c6-1bb33efdce74">

The identified genes are associated with cell cycle regulation and signalling pathways that could play a critical role in the pathogenesis of dengue fever. CDC6 is involved in the initiation of DNA replication, PBK in cell cycle progression and mitosis, and KCTD14 may be associated with protein-protein interactions that influence various biological processes. The upregulation of these genes in dengue fever patients could reflect the host cell response to viral replication or indicate mechanisms of viral pathogenicity (4, 5, 6, 7).

Convalescent vs healthy control samples

Gene expression profiles of convalescent individuals were compared to those of healthy controls using volcano plot analysis to identify significant differences in gene expression. The plot positions genes based on expression fold changes and adjusted p-values, with the significance threshold typically set at a p-value of 0.05 and a log2 fold change greater than an absolute value of 0.58.
In Figure 5, the volcano plot shows a distribution of genes across the spectrum of fold changes and significance levels. However, the analysis did not produce any genes that passed the significance threshold.

<img width="894" alt="Screenshot 2024-05-17 at 11 18 48" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/a5f06716-d091-448b-8f6d-112827b6b0c5">

The lack of significantly differentially expressed genes between convalescent individuals and healthy controls suggests that, at the level of gene expression detectable in this analysis, convalescent individuals may not show marked differences compared to the healthy control population. This could indicate that convalescent patients have returned to a baseline gene expression profile similar to that of healthy individuals, or that changes in gene expression due to the dengue virus do not persist into the convalescent phase.

Dengue Haemorrhagic Fever vs Dengue Fever samples

Volcano plot analysis was used to investigate differential gene expression between dengue haemorrhagic fever (DHF) and dengue fever (DF) populations. This method plots the magnitude of expression change (log2 fold change) against statistical significance (adjusted p-value -log10), allowing simultaneous consideration of effect size and statistical evidence when identifying genes of interest.
Figure 6 presents the volcano plot for comparison between DHF and DF. Despite the analysis, no genes reached the threshold of statistical significance after adjustment for multiple comparisons.

<img width="913" alt="Screenshot 2024-05-17 at 11 18 17" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/34a995ee-0059-4a16-95eb-54ee23529456">

The absence of significant differentially expressed genes suggests that, at least within the sensitivity limits of this study, there may not be substantial differences in gene expression profiles between DHF and DF at the sampled time points. Moreover, it could imply that the distinction between DHF and DF may be driven by factors other than differential gene expression, such as post-transcriptional modifications, changes in protein activity, or host-pathogen interactions at the protein or metabolic level.

Dengue Haemorrhagic Fever vs healthy control samples

Differential expression of genes between dengue haemorrhagic fever (DHF) patients and healthy controls was assessed through volcano plot analysis. This graphical method shows the magnitude of gene expression changes versus their statistical significance.
Figure 7 shows the resulting volcano plot for DHF versus healthy controls. Genes that passed the significance threshold are highlighted in red, indicating substantial differences in expression levels that are statistically significant.

<img width="903" alt="Screenshot 2024-05-17 at 11 17 53" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/f644ca82-9ef5-485b-ab85-2f754d5ed59e">

The analysis identified several genes with downregulation in the DHF group compared to healthy controls, as well as one gene that was significantly upregulated. The results are summarized in Table 3 below.

<img width="826" alt="Screenshot 2024-05-17 at 11 17 35" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/6ea56afe-d027-4864-9c6c-856046995ee7">

Genes downregulated in the DHF group are involved in a variety of cellular processes, including cell cycle regulation, signal transduction, and immune response. For example, CDC6 is a key regulator of the initiation of DNA replication, and its downregulation may reflect disruption of normal cell cycle processes in DHF (4). In contrast, upregulation of CNTNAP3B, which may be involved in cell adhesion and signalling, could potentially indicate a compensatory or pathological response to infection (8).

Dengue Fever vs healthy control samples

Differential gene expression analysis was performed to compare the gene expression profiles of dengue fever (DF) patients with those of healthy controls. The analysis used a volcano plot to visually identify genes with statistically significant differences in expression.

Figure 8 shows the volcano plot for comparison between DF and healthy controls. The graph captures the magnitude of change in gene expression and the significance of this change, with red dots indicating significantly differentially expressed genes.

<img width="925" alt="Screenshot 2024-05-17 at 11 16 58" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/34de3c97-9992-4806-9e7f-7ab5e8222904">

The analysis identified several genes that were significantly downregulated in dengue fever patients compared to healthy controls. The genes and their log2-fold changes and adjusted p values are presented in Table 4.

<img width="764" alt="Screenshot 2024-05-17 at 11 15 59" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/7b41806a-7b6b-4df5-8c6f-9a9abf02dd5b">

Downregulation of these genes in DF patients may reflect cellular responses to infection, such as alterations in cell cycle control, signalling pathways, and other cellular functions critical for host defence mechanisms. For example, the CDC6 gene is essential for the initiation of DNA replication and its reduced expression could indicate an interruption of normal cell cycle progression, a potential strategy of the virus to promote its replication (4).

Machine learning-based classification of dengue fever states

Machine learning techniques were applied to transcriptomic data to evaluate their effectiveness in distinguishing between dengue fever (DF) and dengue hemorrhagic fever (DHF). A Support Vector Machine (SVM) classifier with a linear kernel was trained on a subset of the data, with disease states encoded into numerical labels for analysis.
The SVM classifier achieved an accuracy of 67% in distinguishing between DF and DHF when applied to the test data. As a result, the classification report provides a detailed breakdown of classifier accuracy, recall, and F1 score for each disease state (Figure 9).

<img width="897" alt="Screenshot 2024-05-17 at 11 11 51" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/95eee18b-c31e-41fd-ae8a-85cd1e8d5b06">

The obtained classifier demonstrated higher precision and recall for DF (precision: 0.71, recall: 0.83) than DHF (precision: 0.50, recall: 0.33), as indicated by F1 scores of 0.77 and 0.40, respectively. This suggests that the model was better at identifying DF cases than DHF, which may be due to fewer DHF samples or less distinct gene expression profiles associated with DHF.
Additionally, bootstrap validation was used to estimate the robustness of model performance, which yielded an average accuracy of 0.6189 over 100 iterations. This consistent accuracy across multiple subsets of data indicates that the classifier has a reasonable level of robustness.

<img width="800" alt="Screenshot 2024-05-17 at 11 10 12" src="https://github.com/francarocci/Predicting-Diabetes-from-EHR/assets/141650033/c02fdb03-b80a-4cee-a639-a6f920e808ff">

The findings might suggest that transcriptomics data, together with machine learning, have the potential to distinguish between DF and DHF, which could inform clinical treatment decisions. However, the precision and recall of DHF highlight the need for further model refinement, potentially through the inclusion of more data, feature selection, or exploration of more complex models, to improve classifier performance for clinical applicability.

# Discussion

Gene expression profiles in dengue populations

Analysis of gene expression profiles in four populations – dengue fever (DF), dengue haemorrhagic fever (DHF), convalescent individuals, and healthy controls – provided a nuanced view of the host response to dengue infection. PCA, despite capturing a significant portion of the variance, highlighted the complexity and multidimensional nature of gene expression changes, suggesting that myriad biological processes are disrupted or modified during different phases of the disease. The overlap observed in PCA space between convalescent individuals and those with active dengue fever may indicate a gradual return to baseline expression levels, or perhaps the persistence of some infection- induced expression signatures that delay the return to a healthy state.
HCA results confirm those of PCA, offering a visual representation of the similarity and divergence in gene expression between patient groups. The distinct clusters formed by healthy controls versus those with dengue fever or haemorrhagic fever highlight the potential for using gene expression profiles as biomarkers of disease presence. However, the clusters also raise questions about individual variability in response to the virus and the potential influence of other factors such as genetic predisposition, viral strain differences, or previous exposure to dengue or related viruses.

Biological relevance of differentially expressed genes

The significant genes identified from the volcano tracings not only suggest potential biomarkers for dengue infection, but also provide information on biological pathways that may be perturbed by the virus. For example, downregulation of CDC6, a key regulator of the DNA replication process, could suggest a mechanism by which the dengue virus alters host cell cycle progression to its advantage (4). Similarly, downregulation of PBK and KCTD14 in both dengue fever and haemorrhagic fever compared to healthy controls could reflect a common host response to viral infection, potentially to limit cellular activities that facilitate replication or spread viral (6, 7).
The biological functions of these genes could also shed light on the clinical manifestations of dengue. In fact, modulation of cell cycle genes could relate to the cytopathic effects observed in dengue virus-infected cells, such as apoptosis or autophagy (5). As a result, understanding the interplay between these differentially expressed genes and the life cycle of the dengue virus could open new avenues for therapeutic intervention, potentially targeting the virus's ability to manipulate host cellular machinery.

Machine learning in the clinical differentiation of dengue states

The moderate success of SVM in distinguishing between DF and DHF highlights the potential and limitations of applying machine learning to clinical dengue diagnostics. The size of the dataset is a critical factor; with more extensive data, the model could potentially learn a more accurate and nuanced distinction between disease states. Furthermore, the pre-processed nature of the dataset raises concerns about the loss of critical information. Raw, unprocessed gene expression data often contains noise but also preserves subtle patterns that could be crucial for differentiating related conditions such as DF and DHF. Moreover, pre-processing steps, while necessary to facilitate analysis, could standardize these vital nuances, leading to a model that, while capable of identifying broad differences, lacks the finesse needed to spot greater distinctions. Furthermore, generalized datasets often fail to account for interindividual variability, which is particularly pertinent in diseases such as dengue that have a wide range of clinical presentations. The genetic background of the host, immune history, and even the serotype of the infecting dengue virus can profoundly influence the clinical course and gene expression response of the host.
For the machine learning approach to be truly effective in a clinical context, models must be trained on large, diverse, and possibly multi-omics datasets that capture the full breadth of the host response. Such models could be more effective in identifying biomarkers indicative of the transition from dengue fever to more severe haemorrhagic fever, thus improving patient management and treatment strategies.

# Conclusion

This comprehensive study delved into the intricate gene expression patterns associated with dengue infection. Using advanced data analysis and machine learning techniques, it differentiated between dengue fever, dengue haemorrhagic fever, convalescent individuals, and healthy controls. Moreover, this research used principal component analysis and hierarchical clustering to classify these variations effectively to detect similarities between each disease state. As a result, key genes involved in cell cycle regulation and DNA replication were significantly altered, suggesting the dengue virus's strategy of hijacking the host's cellular machinery for its replication. Despite the obtained findings, the study faced challenges due to the complexity of the disease and limitations of the dataset, such as size and pre-processing. Applying a Support Vector Machine classifier highlighted the potential and challenges of using machine learning in a clinical context. Finally, the findings highlight the importance of developing larger and more complete datasets, incorporating multi-omics approaches and refining machine learning algorithms to improve the understanding and management of dengue virus infection.

# References

1. Kwissa M, Nakaya HI, Onlamoon N, et al. Dengue virus infection induces expansion of a CD14(+) CD16(+)
monocyte population that stimulates plasmablast differentiation. Cell Host Microbe 16(1):115-27 (2014).
2. Bhatt S., Gething P., Brady O., et al. The global distribution and burden of dengue. Nature 496, 504–507 (2013).
3. Lei HY., Yeh TM., Liu HS., et al. Immunopathogenesis of dengue virus infection. J Biomed Sci 8, 377–388 (2001).
4. Bicknell, L., Bongers, E., Leitch, A. et al. Mutations in the pre-replication complex cause Meier-Gorlin syndrome. Nat Genet 43, 356–359 (2011).
5. Mills GB, Schmandt R, McGill M, Amendola A, Hill M, Jacobs K, May C, Rodricks AM, Campbell S, Hogg D. Expression of TTK, a novel human protein kinase, is associated with cell proliferation. J Biol Chem 267(22):16000-6 (1992).
6. Ayllón, V., O'Connor, R. PBK/TOPK promotes tumour cell proliferation through p38 MAPK activity and regulation of the DNA damage response. Oncogene 26, 3451–3461 (2007).
7. Esposito L, Balasco N, Vitagliano L. Alphafold Predictions Provide Insights into the Structural Features of the Functional Oligomers of All Members of the KCTD Family. Int J Mol Sci 23(21):13346 (2022).
8. Boyadjiev SA, South ST, Radford CL, et al. A reciprocal translocation 46,XY,t(8;9)(p11.2;q13) in a bladder exstrophy patient disrupts CNTNAP3 and presents evidence of a pericentromeric duplication on chromosome 9. Genomics 85(5):622-9 (2005).
