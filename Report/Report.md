<!--StartFragment-->

# **Analysis of TCGA Sarcoma data for age associated biomarkers in AYA patients and ML model development for classification**

   Authors (@slack): Vidhyavathy Nagarajan (@Vidhya2205), Ahmed Hasan (@Hasan), Nusrat Afrin (@Nusrat), Shreya Karandikar (@Shreya), Dharshana Rajkumar (@Dharshana), Maram Nhaili (@Maram), Mary Dhevanayagam (@Shanu),
   
   Link to GitHub Repository and Github Code - [****Link to code****](https://github.com/vidhya2205/TCGA-analysis_SARC_DEA_ML_stage3_HackBio/blob/main/Code/Code_BM%2BML.Rmd) **,** [****Link to Repo****](https://github.com/vidhya2205/TCGA-analysis_SARC_DEA_ML_stage3_HackBio)**.

   ## 1. **Introduction**

Sarcoma is a rare and heterogeneous type of cancer of mesenchymal origin accounting for 1% and 15% of all adult and childhood malignancies, respectively (von Mehren M _et al.,_ 2022; Burningham Z _et al.,_ 2012). Due to the diversity of the subtypes and site of origin, its characterization and treatment are challenging (Holthuis EI et al., 2024; Burningham Z et al., 2012). Hence, identifying reliable biomarkers is crucial for improving early diagnosis, prognosis, and treatment response prediction in sarcoma patients.
Previous studies indicate that there is a significant difference in response to therapy, health-related quality index and prognosis between adolescent-younger patients (AYA - age of diagnosis(AOD) 18-40yrs) and older patients (OA - AOD >= 40) __(Stricker E  _et al._, 2023; Younger, E _et al., 2018_; Drabbe C _et al._, 2021; Liu H _et al._, 2022;  Xu Z _et al._, 2021). Regarding the prognosis there have been contradicting conclusions, some reporting that OA patients have a poorer prognosis (Stricker E  _et al._, 2023; Younger, E _et al._, 2018), while some others supporting otherwise (Li, J. _et al_., 2024; Andrew EC _et al_., 2024; Bleyer A _et al_., 2008; Tricoli JV _et al_., 2016; Wolfson JA _et al_., 2023).  Hence, this study focuses on comparing the RNA-seq data of these two age groups to identify age-specific biomarkers to enhance patient characterization, therapeutic strategies, and prognosis.

   ## 2.**Methodology**
<p align = center>
  <kbd>
<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdXD1aGgz_5bou6xMt1GPnacDs1x14Wk8v1LaDVdFV4gmQ0uWehrYpvs5SxkROBz0NTTMqWVDjBS2Dh7sE3IIDUCrOZmKlpCS7yRLuhR1z9Hco1fLEPl3WZ-RqGD2hB00cc8TApU7ceO59_hVPOiMSP1ir1?key=xvw3JB3jr1ZpthYtl54CPw" width="400" height = "400">
  </kbd>
  </p>
  <p align = center><sup>Figure 3.1. Flow chart summarizing the data collection and preprocessing methodology </sup></p>

   ### **2.1. Biomarker Discovery using differential gene expression analysis (DGEA) and functional enrichment analysis (FEA)**

<p align = center>
  <kbd>
<img src="https://drive.google.com/drive/recent" width="400" height = "400">
  </kbd>
  </p>
  <p align = center><sup>Figure 3.2: Flow chart summarizing Biomarker discovery methodology </sup></p>
  
The dataset was derived from The Cancer Genome Atlas (TCGA) project, particularly the "_TCGA-SARC_" cohort, which included sarcoma samples. The samples were separated into two age groups: 18-40 and ≥40 years. Supplementary figure 1, demonstrates the distribution of samples in the two age groups. The ones that lacked or had inaccurate age data were eliminated. Then, a random subset of 20 from each group was chosen for analysis. Unstranded gene expression data were normalized by gene length and read depth, further quantile filtered (cutoff: 0.25) to eliminate low-expression genes. Differential expression analysis was done between age groups, with genes identified as upregulated, downregulated, or non-significant based on a log fold change(logFC) threshold of ±1.5  and FDR < 0.005. Volcano plots and heat maps were created to show differentially expressed genes. The _Ensembl IDs_ were converted to _HGNC symbols_ for genes with significant upregulation or downregulation. Furthermore, functional enrichment analysis was conducted, and results of the top enriched pathways based on fold enrichment and FDR values were presented using bar plots in each category.

   ### **2.2. Machine Learning** 

<p align = center>
  <kbd>
<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeo0AXKHijBjIYyyDOp0R6IqxiGCB9dJD9Yq-TBsG-KtqVjE4kxn75wy1Fydf_w2Zj0PLkTwTJi9beN7beZETfqEy2rTQxRLBFoH3wqSmyZ5zBC50pzS-KxjAhlofbOlgOeYlVXdaxllOAvQIReAY2Z0ClV?key=xvw3JB3jr1ZpthYtl54CPw" width="400" height = "400">
  </kbd>
  </p>
 <p align = center><sup>Figure 3.3: Flow chart summarizing Machine learning methodology </sup></p>

Data was transposed and merged with the meta\_data to include the target variable ( age ) in a single file. Merged data was confirmed for any NAs or non-numeric values and was scaled. The top 1000 genes with variable expression levels were selected by applying standard deviation and organizing them in decreasing order. The data was again checked for missing values and then split into train( 70%) and test sets (30%). Data was classified based on age group by training Random Forest using the training set where we identified its accuracy based on precision, recall, and F1 scores. We ensured the model’s performance and precision using a confusion matrix and plotted this using an ROC curve. A 10-fold cross-validation was done using the k method. The top 20 biomarkers were plotted based on the Mean Decrease score given by the Random Forest model. A violin plot showed the significance of biomarkers in two different age groups.**

## **3. Results and Discussion**

### **3.1. Biomarker discovery**

####       **3.1.1. Differential gene expression analysis (DGEA)**

Based on the DGEA, 2376 significant differentially expressed genes (DEG) were identified from the \~31,000 genes, between the two groups, using a log fold change and p-value cutoff. Of these, 848 and 1877 genes were up-regulated and down-regulated respectively, in the AYA patient group. The volcano plot (figure 4.1) shows the distribution of DEGs (\~31,000), with highly significant genes displayed in the top right (blue) and left (red) quadrants. Heatmap (figure 4.2) of the significant DEG (2376 genes), shows a pattern of dysregulation specific to each group as clustered by column colors (red-OA and blue-AYA patients).

<p align = center float="left">
  <kbd>
<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXe_daCO5dEInyrn88GEDk04DNfX334MeHslBXyU4Q-QZ0FPX1Ffr9cGG-3v_h95-JaauvytnmiTSe-Oq3a9BcL7c4NwvHBKl0pbA0ZZL1iSahTCg8ll-Q6O77WF8ukFb0ZrG_grfGHXRnbkpEEPiUC7fNQs?key=xvw3JB3jr1ZpthYtl54CPw" width="390" height = "400">
  </kbd>
   <kbd>
<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXco4J90eU6x_p5rLabF80J43jSqiWJXQzyVgrPUGND3nnHbZUgV-S4wXqdqnN0KM6w_jJPftyStuyqHofw_2wbJ1Yqiu6FoXTxEkTOJsvSfsQXUBtMLlhOs8rSU4M6tYPOYCOUdq9IaSsRaaiyAh-wTGTU?key=xvw3JB3jr1ZpthYtl54CPw" width="390" height = "400">
  </kbd>
</p>
<p align = center>
  <sup>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Fig 3.1. Volcano Plot &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fig 3.2. Heatmap of significantly up and down regulated genes
  </sup>
</p>

Though there are contradicting studies, some prior studies have shown that AYA sarcoma patients are associated with a worse prognosis compared to OA patients (Li, J. et al., 2024; Andrew EC et al., 2024; Bleyer A. et al., 2008; Tricoli JV et al., 2016; Wolfson JA et al., 2023). Along similar lines, the identified protein-coding differentially regulated genetic biomarkers are closely related to cancer proliferation, advanced stages, and poor prognosis as explained in detail below.
Among the top 5 novel upregulated genes (based on logFC) in the AYA group, there were 2 lncRNAs (ENSG00000287397 and ENSG00000241168) and 3 protein-coding genes (_GABRA6_,  _NANOGNB_, _PPP4R3C_).  _GABRA6_ gene encodes for a subunit of the _GABA_ receptor and is involved in the GABAergic signaling pathway linked to tumor progression and is explored as a therapeutic target in multiple cancers (Bhattacharya D _et al_., 2021; Yang Y, _et al_., 2023; Huang W _et al_., 2022). Specifically, in the chondrosarcoma cell line, an inhibitor of the GABAergic signaling pathway has successfully attenuated proliferation (Yang Y, _et al_., 2023). _PPP4R3C,_ a regulatory subunit of _PPP4C_ (Hastie CJ _et al_., 2006), which __is associated with homologous recombination and Wnt signaling pathways, has a well-established role in cancer(Wang, Y. _et al_., 2023; Dong MZ _et al_., 2022). Further, this gene has been reported to be a potential diagnostic biomarker for its high expression in several tumors including sarcoma, and is associated with metastasis and poor prognosis in several other cancers (Wang, Y. _et al_., 2023; Li, X., _et al_., 2015; Wang K _et al_., 2024).

The top 5 downregulated genes included 1 lncRNA (ENSG00000286564), and 4 protein-coding genes (_SFTPA1, SFTPB, ADIPOQ, OTX2_). Among these, _SFTPA1, SFTPB, and ADIPOQ_ are found to be downregulated in cancers and their overexpression is associated with good prognosis in some cancers. While _SFTPA1_ and _SFTPB_ are mainly involved in immune response in lung cancer cells, and their downregulation is associated with cancer progression and associated with aggressive growth, _ADIPOQ_ is associated with inducing autophagic cell death in breast cancer (Luo, H _et al_., 2023; Yuan L _et al._ 2022; Chung SJ, _et al_., 2017). Though limited studies are available on the role of these genes in sarcoma and cancer in general, these serve as potential biomarkers.

   ####       **3.1.2. Functional enrichment analysis (FEA)**

FEA of the upregulated and downregulated genes resulted in a set of pathways that are enriched  with the gene sets respectively. A total of 4686 pathways were identified by the analysis (2423 in Biological Process (BP), 1157 in Molecular Function (MF), 517 in Cellular components(CC) and 589 KEGG Pathways (KP))  for each gene set. From these the top enriched pathways are identified and plotted based on enrichment and p-value (FDR) as illustrated in Fig 3.3 and Fig. 3.4.
<p align = center>
  <kbd>
<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfh2bYXUy07vUSYVIP51GsL0B_5eqrRhIUTG37WkmT3CBOOs80FPygdjR-5nx1dfymP7xkVzebXQy03NU_urtO_ieN7aKMGArea16zs7DFUhSWds_tL9jmh1a2S9Wd0bycvRdx549EsmHVc8e80-Efr3W6j?key=xvw3JB3jr1ZpthYtl54CPw" width="700" height = "300">
  </kbd>
  </p>
 <p align = center><sup>Fig. 3.3. FEA of downregulated genes</sup></p>
    
<p align = center>
  <kbd>
<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXe9ED8oDB2yYaQzGemw76B-Z_TpMnFYgY0GDgPww0OopTyxm8Cx4p8ArwRxZc-72Yi4afeEiDjHanebfrOZ1GnvJtrwaDoLgT61dQBn3ByG2eqB1E2YuaCIDy8m2UVbq232Ib7moycCaJ2q4DytuTD8qRDM?key=xvw3JB3jr1ZpthYtl54CPw" width="700" height = "300">
  </kbd>
  </p>
 <p align = center><sup>Fig. 3.4. FEA of upregulated  genes</sup></p>
 
Transcriptional Regulatory Network in Embryonic Stem Cells (TRNES), Calcium Signaling, Glutamate Receptor Signaling, Cellular Effects of Sildenafil, GABA Receptor Signaling are the the top 5 enriched KEGG pathways in downregulated genes FEAin AYA sarcoma patients . The TRNES pathway, Glutamate Receptor Signaling, Calcium Signaling and GABA Receptor Signaling are pathways that associated with therapy resistance in sarcoma (Zhang, Z. et al., 2024), TCA cycle (in osteosarcoma) (Koda S et al., 2023; A., B., Shin  et al., 2013), immune associated pathways in cancer (including osteosarcoma) (Wu L, et al., 2021), and proliferation of chondrosarcoma (Kanbara K et al., 2018) respectively. This suggests that dysregulation of genes in these pathways can in turn impact multiple mechanisms in cancer and have to be studied in detail.

The top 5 enriched KEGG pathways in upregulated genes FEA includes, Granulocyte Adhesion and Diapedesis, Agranulocyte Adhesion and Diapedesis, T Helper Cell Differentiation, Altered T Cell and B Cell Signaling in Rheumatoid Arthritis, Pathogenesis of Multiple Sclerosis. Of these, Granulocyte & Agranulocyte Adhesion and Diapedesis pathways are associated with innate immune response and cancer cell migration (Xing L, et al., 2017; Filippi MD et al., 2016), while T Helper Cell Differentiation pathway is associated with active immune response and control tumor necrosis process (Ahmed H et al., 2022). Additionally, most of the highlighted pathways in the BP term are also associated with immune response (Fig 4.4). These results suggest that the majority of upregulated genes in AYA sarcoma patients are associated with immune response pathways and studying them in detail could provide insights on effectiveness of immunotherapy. Additionally, multiple retrospective studies have shown that though immunotherapy is emerging in treatment of sarcoma, it's not very effective and requires more advancement (Wood GE et al 2024; Koumarianou A et al., 2021; Jeong S et al., 2023).

   ### **3.2. Machine Learning**

   ####       **3.2.1. Random Forest Classification**

A Random Forest classification model was developed based on gene expression data to distinguish between two age groups (18-40 and ≥40 years). After filtering the most variable genes using standard deviation, the model was trained with 100 decision trees and tuned via 10-fold cross-validation, yielding an Out-of-Bag (OOB) error rate of 30%. The confusion matrix showed class error rates of 35% for the 18-40 group and 25% for the ≥40 group.

   ####       **3.2.2. ROC Curve**

Upon validation, the model achieved 100% accuracy, with Sensitivity, Specificity, Precision, Recall, and F1 Scores all scoring 1.0, indicating excellent classification performance. The optimal number of variables per split (mtry = 1000) yielded an R-squared value of 0.737 and an RMSE of 0.445, demonstrating the model’s ability to explain a significant portion of the data's variance. The ROC curve, with an AUC of 1, further reinforced the model’s predictive power.
<p align = center>
  <kbd>
<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeU_UBiabBgpO57DU9JEZpfiM-1AEICXdESS2QKpsj387_ZPYAZaWFLAFalfey9i6lQ6xqInKRO5v5vwalxOLrjCvBbx-_Inlv7LRGtzHlkNKNVkB5PUtbvP5IcTPvvrUgyRrP2Zkyti4tsm6CnGrFVYqu1?key=xvw3JB3jr1ZpthYtl54CPw" width="700" height = "300">
  </kbd>
  </p>
 <p align = center><sup>Fig 4.2.3. Receiver operating characteristic (ROC) curve demonstrating the performance of Random Forest in Biomarker identification. The area under the curve (AUC) is 1.</sup></p>

 ####       **3.2.3. Top Variable Genes** 

**Age group:**

The top 20 variable genes between the two age groups were identified and visualized using violin plots, revealing distinct expression patterns. Several genes, such as ENSG00000173369 and ENSG00000124491, were more expressed in the ≥40 groups, while others, like ENSG00000173388 and ENSG00000119582, showed higher expression in the younger group. These differences suggest that these genes may serve as molecular markers for aging.

_C1QB_ (ENSG00000173369) is a component of C1Q. It activates the complement pathway and aggravates disease progression creating an immunosuppressive environment that allows cancer cells to proliferate and evade immune detection (Roumenina et.al.,2019). C1Q may have regulatory functions in tumors that enhance survival and cause apoptosis. Determining whether C1QB is largely tumor-promoting or tumor-suppressive in sarcomas is difficult due to the dual nature of the complement system in cancer (Chen et.al.,2021).

_CD74_ is an invariant chain of human lymphocyte antigen (HLA) class II chaperone that functions in antigen presentation.  It is a receptor on the cell surface that binds to the cytokine macrophage migration inhibitory factor (MIF). Improved CD74/MIF interactions were found to activate the PI3K/AKT pathway in melanoma and increase tumor survival. With a comparatively high expression in pediatric osteosarcoma patients without metastases, CD74 has been found associated with immune infiltrations and immune checkpoint inhibitors (Yuan et al., 2024). AYA patients should be examined as they have high expression of it in our study.

<p align = center>
  <kbd>
<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXe-BgLQNZLIm4ek_YMwALylMVcHcQNEZMZpJIQzDdd5kI9drJXT6uqCNrD0XoNiqrWV23clLExsgSkHCUIEkXhqga6YwOMGshUSWHS7dMy53dycGd1KbuIemz04rjcMJIwDWd9B5kDf037kjADM6dDj24Q?key=xvw3JB3jr1ZpthYtl54CPw" width="700" height = "500">
  </kbd>
  </p>
 <p align = center><sup>Fig 4.2.2. Violin overlay box plot for different expression levels wrt age groups ( 0= 18-40, 1 = >=40) </sup></p>

**Mean Decrease Score via Random Forest:**
   
<p align = center>
  <kbd>
<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdqVBSYmkJFOlShcecTmXiaJ-54i8aPsHOZ7HKZu7LO_SjLee4ErPIJk8jzQFXHFWmoMMoTAfuClDKJdTtsohxUGXX_PGilNKdGpzfenK8ucgEwiJXrYSdrzH_32ax4x64GcejwZCgLm9tcto-XZ8mqP6g?key=xvw3JB3jr1ZpthYtl54CPw" width="700" height = "500">
  </kbd>
  </p>
 <p align = center><sup>Fig 4.2.1. MeanDecreaseGini scores from the Random Forest model to measure feature relevance. Genes at the bottom are the most important and so on.</sup></p>
    
The study highlights the effectiveness of gene expression profiles in distinguishing between younger and older age groups, with identified genes potentially linked to aging-related processes such as cell cycle regulation and apoptosis. The top 20 genes present a focused list for further exploration as biomarkers for age-related diseases or therapeutic targets.

   ### **4. Conclusion and Future Prospects**

DGEA and functional enrichment analysis of the RNA-seq data of the AYA and OA sarcoma patients was performed to identify significant biomarkers. Many of the top 5 differentially regulated genes identified have been linked to play a role in sarcoma and other cancers. However, research is needed to elucidate and establish their roles in the AYA sub-group of sarcoma patients. Future studies can be directed to explore the role of these genes in this subgroup. Additionally, the differentially regulated protein-coding genes identified in silico must be validated by in vivo and in vitro assays for their role as age-based biomarkers in sarcoma. With increasing interest in the role of lncRNAs in sarcoma pathogenesis and progression (Wang K et al., 2020; Min L et al., 2017), the dysregulated lncRNAs can pave the way to new research. The dysregulation of immune response pathways, vital pathways associated with cancer progression, and cancer stem cell-like properties indicate a significant difference in the progression and therapy response between the two groups. The integration of multi-omics can contribute to a more comprehensive disease profile which will help understand sarcoma's underlying mechanism and develop suitable therapeutic targets and diagnostic biomarkers for each age group. The current study has some limitations due to the limited number of samples and uneven distribution of subtypes in the 2 groups, hence a larger study with even distribution could provide more accurate insights. 

The results of applying the Random Forest model on 40 samples of Sarcoma gave accuracy and Kappa of 1, indicating sensitivity and specificity values of 1. This suggests that the model is perfectly predicted for both classes of age groups. The 95% confidence interval for accuracy is (0.7354, 1), which shows the model could generalize well on new data. Positive and Negative Predictive Values (Pos Pred Value = 1, Neg Pred Value = 1) indicate that the model’s predictions for both classes are entirely accurate. Cross-validation via k-fold showed a mtry value of 1000 and an increase in the RMSE value as the mtry increases depicting an accuracy. The balanced accuracy is also 1, confirming equal performance across both classes. However, these perfect scores also indicate that there might be overfitting due to the small sample size of 40 and high dimensionality of 1000. The top 20 variable genes identified by the model can help classify sarcoma based on age. To enhance model performance, validate it on independent data to assess generalizability and increase the sample size to mitigate overfitting. Employ dimensionality reduction techniques, such as PCA or feature selection, and implement repeated stratified k-fold cross-validation for reliable performance evaluation. Additionally, explore simpler models like Logistic Regression or SVM for potentially better generalization, analyze feature importance for interpretability, and consider regularization methods to prevent overfitting. This could further enhance the predictive power and uncover non-linear relationships within gene expression data. Lastly, incorporating longitudinal data and exploring how gene expression patterns evolve as individuals age could offer valuable insights into aging's progressive nature, potentially leading to early detection markers for age-associated diseases.

   ### 5. References 

1. von Mehren M, Kane JM, Agulnik M, Bui MM, Carr-Ascher J, Choy E, Connelly M, Dry S, Ganjoo KN, Gonzalez RJ, Holder A, Homsi J, Keedy V, Kelly CM, Kim E, Liebner D, McCarter M, McGarry SV, Mesko NW, Meyer C, Pappo AS, Parkes AM, Petersen IA, Pollack SM, Poppe M, Riedel RF, Schuetze S, Shabason J, Sicklick JK, Spraker MB, Zimel M, Hang LE, Sundar H, Bergman MA. Soft Tissue Sarcoma, Version 2.2022, NCCN Clinical Practice Guidelines in Oncology. J Natl Compr Canc Netw. 2022 Jul;20(7):815-833. doi: 10.6004/jnccn.2022.0035. PMID: 35830886; PMCID: PMC10186762.

2. Burningham Z, Hashibe M, Spector L, Schiffman JD. The epidemiology of sarcoma. Clin Sarcoma Res. 2012 Oct 4;2(1):14. doi: 10.1186/2045-3329-2-14. PMID: 23036164; PMCID: PMC3564705.

3. Holthuis EI, Heins MJ, van Houdt WJ, et al. Improving Diagnosis and Care for Patients With Sarcoma: Do Real-World General Practitioners Data and Prospective Data Collections Have a Place Next to Clinical Trials?. JCO Clin Cancer Inform. 2024;8:e2400054. doi:10.1200/CCI.24.00054

4. Stricker E, Reed DR, Schabath MB, Sok P, Scheurer ME, Lupo PJ. Trends in Overall Survival among Patients Treated for Sarcoma at a Large Tertiary Cancer Center between 1986 and 2014. Cancers (Basel). 2023 Jan 14;15(2):514. doi: 10.3390/cancers15020514. PMID: 36672463; PMCID: PMC9856368.

5. Liu H, Zhang H, Zhang C, Liao Z, Li T, Yang T, Zhang G, Yang J. Pan-Soft Tissue Sarcoma Analysis of the Incidence, Survival, and Metastasis: A Population-Based Study Focusing on Distant Metastasis and Lymph Node Metastasis. Front Oncol. 2022 Jul 7;12:890040. doi: 10.3389/fonc.2022.890040. PMID: 35875111; PMCID: PMC9303001.

6. Xu Z, Wang L, Tu L, Liu Y, Xie X, Tang X, Luo F. Epidemiology of and prognostic factors for patients with sarcomatoid carcinoma: a large population-based study. Am J Cancer Res. 2020 Nov 1;10(11):3801-3814. Erratum in: Am J Cancer Res. 2021 Apr 15;11(4):1800-1802. PMID: 33294268; PMCID: PMC7716166.

7. Drabbe C, Van der Graaf WTA, De Rooij BH, Grünhagen DJ, Soomers VLMN, Van de Sande MAJ, Been LB, Keymeulen KBMI, van der Geest ICM, Van Houdt WJ, Husson O. The age-related impact of surviving sarcoma on health-related quality of life: data from the SURVSARC study. ESMO Open. 2021 Feb;6(1):100047. doi: 10.1016/j.esmoop.2021.100047. Epub 2021 Jan 27. PMID: 33516150; PMCID: PMC7844567.

8. Younger, E., Husson, O., Bennister, L. et al. Age-related sarcoma patient experience: results from a national survey in England. BMC Cancer 18, 991 (2018). <https://doi.org/10.1186/s12885-018-4866-8>

9. Andrew EC, Lewin J, Desai J, Orme L, Hamilton A, Bae S, Zhu W, Nicolson S, Varghese LN, Mitchell CB, et al. Clinical Impact of Comprehensive Molecular Profiling in Adolescents and Young Adults with Sarcoma. Journal of Personalized Medicine. 2024; 14(2):128. https\://doi.org/10.3390/jpm14020128

10. Li, J., Ji, Y. Clinicopathological characteristics and genetic features of young and senior Ewing sarcoma patients. Diagn Pathol 19, 124 (2024). https\://doi.org/10.1186/s13000-024-01548-4

11. Bleyer A, Barr R, Hayes-Lattin B, et al. The distinctive biology of cancer in adolescents and young adults. Nat Rev Cancer. 2008;8(4):288-298. doi:10.1038/nrc2349

12. Tricoli JV, Blair DG, Anders CK, Bleyer WA, Boardman LA, Khan J, Kummar S, Hayes-Lattin B, Hunger SP, Merchant M, Seibel NL, Thurin M, Willman CL. Biologic and clinical characteristics of adolescent and young adult cancers: Acute lymphoblastic leukemia, colorectal cancer, breast cancer, melanoma, and sarcoma. Cancer. 2016 Apr 1;122(7):1017-28. doi: 10.1002/cncr.29871. Epub 2016 Feb 5. PMID: 26849082; PMCID: PMC4803597.

13. Wolfson JA, Kenzik KM, Foxworthy B, et al. Understanding Causes of Inferior Outcomes in Adolescents and Young Adults With Cancer. J Natl Compr Canc Netw. 2023;21(8):881-888. doi:10.6004/jnccn.2023.7056.

14. Huang W, Cao L. Targeting GABA signaling for cancer treatment. Nat Cell Biol. 2022;24(2):131-132. doi:10.1038/s41556-021-00839-y

15. Bhattacharya D, Gawali VS, Kallay L, Toukam DK, Koehler A, Stambrook P, Krummel DP, Sengupta S. Therapeutically leveraging GABAA receptors in cancer. Exp Biol Med (Maywood). 2021 Oct;246(19):2128-2135. doi: 10.1177/15353702211032549. PMID: 34649481; PMCID: PMC8524771.

16. Wang K, Peng B, Xu R, et al. Comprehensive analysis of PPP4C's impact on prognosis, immune microenvironment, and immunotherapy response in lung adenocarcinoma using single-cell sequencing and multi-omics. Front Immunol. 2024;15:1416632. Published 2024 Jul 4. doi:10.3389/fimmu.2024.1416632

17. Li, X., Liang, L., Huang, L. et al. High expression of protein phosphatase 4 is associated with the aggressive malignant behavior of colorectal carcinoma. Mol Cancer 14, 95 (2015). https\://doi.org/10.1186/s12943-015-0356-7

18. Dong MZ, Ouyang YC, Gao SC, et al. PPP4C facilitates homologous recombination DNA repair by dephosphorylating PLK1 during early embryo development. Development. 2022;149(10):dev200351. doi:10.1242/dev.200351

19. Wang, Y., Han, W., Yun, S. et al. Identification of protein phosphatase 4 catalytic subunit as a Wnt promoting factor in pan-cancer and Xenopus early embryogenesis. Sci Rep 13, 10240 (2023). https\://doi.org/10.1038/s41598-023-35719-y.

20. Hastie CJ, Vázquez-Martin C, Philp A, Stark MJ, Cohen PT. The Saccharomyces cerevisiae orthologue of the human protein phosphatase 4 core regulatory subunit R2 confers resistance to the anticancer drug cisplatin. FEBS J. 2006;273(14):3322-3334. doi:10.1111/j.1742-4658.2006.05336.x

21. Grubelnik G, Boštjančič E, Pavlič A, Kos M, Zidar N. NANOG expression in human development and cancerogenesis. Exp Biol Med (Maywood). 2020;245(5):456-464. doi:10.1177/1535370220905560

22. Dunwell TL, Holland PWH. A sister of NANOG regulates genes expressed in pre-implantation human development. Open Biol. 2017;7(4):170027. doi:10.1098/rsob.170027

23. Yang Y, Ren L, Li W, et al. GABAergic signaling as a potential therapeutic target in cancers. Biomed Pharmacother. 2023;161:114410. doi:10.1016/j.biopha.2023.114410

24. Chung SJ, Nagaraju GP, Nagalingam A, et al. ADIPOQ/adiponectin induces cytotoxic autophagy in breast cancer cells through STK11/LKB1-mediated activation of the AMPK-ULK1 axis. Autophagy. 2017;13(8):1386-1403. doi:10.1080/15548627.2017.1332565

25. Yuan L, Wu X, Zhang L, et al. SFTPA1 is a potential prognostic biomarker correlated with immune cell infiltration and response to immunotherapy in lung adenocarcinoma. Cancer Immunol Immunother. 2022;71(2):399-415. doi:10.1007/s00262-021-02995-4

26. Luo, H., Li, Q., Wang, RT. et al. Downregulation of pro-surfactant protein B contributes to the recurrence of early-stage non-small cell lung cancer by activating PGK1-mediated Akt signaling. Exp Hematol Oncol 12, 94 (2023). <https://doi.org/10.1186/s40164-023-00455-6>.

27. Jiang MC, Ni JJ, Cui WY, Wang BY, Zhuo W. Emerging roles of lncRNA in cancer and therapeutic opportunities. Am J Cancer Res. 2019;9(7):1354-1366. Published 2019 Jul 1.

28. Xie, J., Wang, M., Xu, S., Huang, Z., & Grant, P. W. (2021). The Unsupervised Feature Selection Algorithms Based on Standard Deviation and Cosine Similarity for Genomic Data Analysis. _Frontiers in Genetics_, _12_, 684100. <https://doi.org/10.3389/fgene.2021.684100> 

29. Acharjee, A., Larkman, J., Xu, Y. _et al._ A random forest-based biomarker discovery and power analysis framework for diagnostics research. _BMC Med Genomics_ **13**, 178 (2020). <https://doi.org/10.1186/s12920-020-00826-6> 

30. Naji, M. A., Filali, S. E., Aarika, K., Benlahmar, E. H., Abdelouhahid, R. A., & Debauche, O. (2020). Machine Learning Algorithms For Breast Cancer Prediction And Diagnosis. _Procedia Computer Science_, _191_, 487-492. <https://doi.org/10.1016/j.procs.2021.07.062>.

31. Saritas, I., Ozkan, I. A., & Sert, I. U. (2010). Prognosis of prostate cancer by artificial neural networks. _Expert Systems With Applications_, _37_(9), 6646-6650. <https://doi.org/10.1016/j.eswa.2010.03.056> 

32. S. Sharma, A. Aggarwal and T. Choudhury, "Breast Cancer Detection Using Machine Learning Algorithms," _2018 International Conference on Computational Techniques, Electronics and Mechanical Systems (CTEMS)_, Belgaum, India, 2018, pp. 114-118, doi: 10.1109/CTEMS.2018.8769187.

33. Roumenina, Lubka T et al. “Tumor Cells Hijack Macrophage-Produced Complement C1q to Promote Tumor Growth.” _Cancer immunology research_ vol. 7,7 (2019): 1091-1105. doi:10.1158/2326-6066.CIR-18-089.

34. Chen LH, Liu JF, Lu Y, He XY, Zhang C, Zhou HH. Complement C1q (C1qA, C1qB, and C1qC) May Be a Potential Prognostic Factor and an Index of Tumor Microenvironment Remodeling in Osteosarcoma. Front Oncol. 2021 May 17;11:642144. doi: 10.3389/fonc.2021.642144. PMID: 34079754; PMCID: PMC8166322.

35. Yuan J, Yu S. Comprehensive Analysis Reveals Prognostic and Therapeutic Immunity-Related Biomarkers for Pediatric Metastatic Osteosarcoma. Medicina (Kaunas). 2024 Jan 4;60(1):95. doi: 10.3390/medicina60010095. PMID: 38256356; PMCID: PMC10820594.

36. Wang K, Ye X, Yang C, et al. Comprehensive Analysis of Novel lncRNA-TF Regulatory Cross Talks and Identification of Core lncRNA-TF Feedback Loops in Sarcoma. DNA Cell Biol. 2020;39(9):1558-1572. doi:10.1089/dna.2020.5385

37. Min L, Garbutt C, Tu C, Hornicek F, Duan Z. Potentials of Long Noncoding RNAs (LncRNAs) in Sarcoma: From Biomarkers to Therapeutic Targets. Int J Mol Sci. 2017;18(4):731. Published 2017 Mar 29. doi:10.3390/ijms18040731

38. Jeong S, Afroz S, Kang D, Noh J, Suh J, Kim JH, You HJ, Kang HG, Kim YJ, Kim JH. Sarcoma Immunotherapy: Confronting Present Hurdles and Unveiling Upcoming Opportunities. Mol Cells. 2023 Oct 31;46(10):579-588. doi: 10.14348/molcells.2023.0079. Epub 2023 Sep 22. PMID: 37853684; PMCID: PMC10590708.

39. Koumarianou A, Duran-Moreno J. The Sarcoma Immune Landscape: Emerging Challenges, Prognostic Significance and Prospective Impact for Immunotherapy Approaches. Cancers (Basel). 2021 Jan 20;13(3):363. doi: 10.3390/cancers13030363. PMID: 33498238; PMCID: PMC7863949.

40. Wood GE, Meyer C, Petitprez F, D'Angelo SP. Immunotherapy in Sarcoma: Current Data and Promising Strategies. Am Soc Clin Oncol Educ Book. 2024;44(3):e432234. doi:10.1200/EDBK\_432234

41. Ahmed H, Mahmud AR, Siddiquee MF, Shahriar A, Biswas P, Shimul MEK, Ahmed SZ, Ema TI, Rahman N, Khan MA, Mizan MFR, Emran TB. Role of T cells in cancer immunotherapy: Opportunities and challenges. Cancer Pathog Ther. 2022 Dec 20;1(2):116-126. doi: 10.1016/j.cpt.2022.12.002. PMID: 38328405; PMCID: PMC10846312.

42. Filippi MD. Mechanism of Diapedesis: Importance of the Transcellular Route. Adv Immunol. 2016;129:25-53. doi: 10.1016/bs.ai.2015.09.001. Epub 2015 Oct 14. PMID: 26791857; PMCID: PMC4889131.

43. Xing L, Cheng Q, Zha G, Yi S. Transcriptional Profiling at High Temporal Resolution Reveals Robust Immune/Inflammatory Responses during Rat Sciatic Nerve Recovery. Mediators Inflamm. 2017;2017:3827841. doi: 10.1155/2017/3827841. Epub 2017 Apr 12. PMID: 28490837; PMCID: PMC5405595.

44. Kanbara K, Otsuki Y, Watanabe M, et al. GABAB receptor regulates proliferation in the high-grade chondrosarcoma cell line OUMS-27 via apoptotic pathways. BMC Cancer. 2018;18(1):263. Published 2018 Mar 7. doi:10.1186/s12885-018-4149-4

45. Koda S, Hu J, Ju X, Sun G, Shao S, Tang RX, Zheng KY, Yan J. The role of glutamate receptors in the regulation of the tumor microenvironment. Front Immunol. 2023 Feb 1;14:1123841. doi: 10.3389/fimmu.2023.1123841. PMID: 36817470; PMCID: PMC9929049.

46. Zhang, Z., Zhang, Y. Transcriptional regulation of cancer stem cell: regulatory factors elucidation and cancer treatment strategies. J Exp Clin Cancer Res 43, 99 (2024). <https://doi.org/10.1186/s13046-024-03021-y>

47. A., B., Shin, S.-S., & Che, S. (2013). Glutamate Signaling in Human Cancers. InTech. doi: 10.5772/55174

48. Wu L, Lian W, Zhao L. Calcium signaling in cancer progression and therapy. FEBS J. 2021;288(21):6187-6205. doi:10.1111/febs.16133
<!--EndFragment-->
