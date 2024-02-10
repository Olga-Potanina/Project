# Comparative analysis of the gut microbiota composition of healthy people and people with diarrhoea-predominant irritable bowel syndrome

*Authors:* O. Potanina, A. Sozontov, D. Syrkova, A. Soroka *Supervisors:* E. Shelly, E. Chukhrova <img src="\data\pictures\Bioinformatics_Institute.png" height="50"/>

**Introduction.** Irritable bowel syndrome (IBS) is a highly prevalent chronic disorder of gut-brain interaction, which is characterized by symptoms of recurrent abdominal pain and disordered defecation.
Patients are subgrouped according to their predominant stool pattern into IBS with diarrhea (diarrhea-predominant IBS), IBS with constipation, IBS with mixed bowel habits or IBS unclassified.
Therapies for IBS are only modestly effective, as the pathophysiology is not completely understood and is believed to be multifactorial.
In the last decades, the altered human gut microbiota has been proposed as one of the possible causes of IBS [1-2].

The objective of our project was the comparative analysis of the gut microbiota composition in patients with diarrhea-predominant IBS and healthy individuals.

**Materials and methods.** Raw sequencing data were taken from open sources (NCBI). All statistical analyses were performed using R (version 4.3.2) in RStudio (version 2023.06.1). ComBat algorithm (library “MBECS”) was used for batch-effect correction (the batch effect covariate = research_id). A p-value of <0.05 was considered statistically significant.

**Results and discussion.** Final analysis included 7 studies (total sample size was 381 participants) that evaluated gut microbiota from faeces. The general characteristics of the included studies are presented in *Table ​1.* Different variable regions of 16S rRNA genes were used for DNA amplification. In all cases, the Illumina MiSeq sequencer and the Amplicon sequencing approach were used. Taxa not found in more than 95% of the subjects have been deleted.

*Table 1.* General characteristics of the included studies
| Study | Country | Year | 16S rRNA gene region | Number of subjects (N=381) | Health state of the subjects |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | Belgium | 2018 | V5-V6 | 46 | healthy |
| 2 | Italy | 2018 | V3-V4 | 36 | healthy |
| 3 | Poland | 2023 | V3-V4 | 70 | healthy |
| 4 | Australia, Austria, Germany, Greece, Hungary, Ireland, Israel, Italy, Norway, UK, USA | 2018 - 2023 | V4 | 87 | healthy//IBS |
| 5 | Austria | 2017 | V4 | 25 | IBS |
| 6 | Israel | 2022 | V4 | 22 | IBS |
| 7 | Spain | 2015 | V4 | 95 | IBS |

As seen in *Table 2*, Welch Two Sample t-test found significantly higher levels of inflammatory, pathogenic and conditionally normal G-taxa, as well as lower levels of vitamin  B12 producing and increasing with coffee bacterial genera of patients with IBS compared to healthy controls.

*Table 2.* Results of IBS/healthy people comparison of total percentage means of G-taxa with special properties 
| G_taxa | Number of taxa |	Mean total percentage in IBS | Mean of total percentage in healthy | Difference in means | 95% CI*	| p.unadjusted* | p.adjusted** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Inflammatory | 48 |	5.34 | 3.00 | 2.34 | 1.65:3.03 | < 0.001 | **< 0.001** |
| Propionate producing | 18 | 22.95 | 20.66 | 2.29 | 0.11:4.48 | 0.04 | 0.800 |
| Acetate producing |	31 | 26.19 | 24.30 | 1.89	| -0.31:4.08 | 0.092 | **< 0.001** |
| Increase with alcohol |	3	| 15.25 |	13.38 |	1.87 | -0.14:3.87 | 0.068	| 1.000 |
| Increase with coffee | 5 | 7.71 | 9.49 | -1.78 | -2.66:-0.89 | < 0.001 | **< 0.001** |
| Vitamin B12 producing |	4 | 4.69 | 6.23	| -1.54	| -2.35:-0.74 | < 0.001	| **< 0.001** |
| Pathogens	| 7	| 1.31 | 0.07 | 1.24 | 0.91:1.57 | < 0.001	| **< 0.001** |
| Special_properties	| 34	| 11.12	| 12.28	| -1.16 |	-2.15:-0.17	| 0.022	| 0.484 |
| Conditionally normal	| 50	| 4.37	| 3.27	| 1.10	| 0.43:1.77 |	0.001 | **0.023** |
| Gases producing | 9 | 2.77 | 2.01 | 0.76 | 0.38:1.14 | < 0.001 | **< 0.001** |
| Serotonin destroying | 7 | 2.97 | 2.25 | 0.72 | 0.09:1.36 | 0.026 | 0.546 |
| Probiotics | 5 | 1.97 | 2.48 | -0.51 | -1.15:0.12 | 0.115 | 1.000 |
| Serotonin producing | 20 | 5.75 | 6.20 | -0.45 | -1.24:0.34 | 0.266 | 1.000 |

** Welch Two Sample t-test, **the Holm correction

The specificity of the data under study implies the presence of a large number of zeros, as not all taxa may be detected in all patients.
Our constructed model takes into account patient identification, stratification by study number (additional batch effect correction), and utilizes taxon-filtered data. We employed a Generalized Linear Model (GLM) for the Percentage variable, considering the complexities of the sample and the nested structure of patient data. The model uses the tweedie distribution family (commonly used for modeling positive continuous random variables with a heavy right tail and an excess of zeros).
The assessment is presented as the mean percentage difference between the Healthy subjects group and the IBS group with a two-sided confidence interval; negative values indicate a lower average level of a particular taxon in the IBS patient group. The data are sorted by the absolute difference in mean value change.

*Table 3.*  Zero inflation method for G taxa
| Estimate | 2.5 % | 97.5 % | p.value | Taxon name | p.adjusted* |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 0.114 | 0.053 | 0.174 | <0.001 | Methanobrevibacter_G | **0.031** |
| -0.107 | -0.127 | -0.087 | <0.001 | Flavobacterium_G | **<0.001** |
| 0.086 | 0.056 | 0.115 | <0.001 | Senegalimassilia_G | **<0.001** |
| 0.065 | 0.038 | 0.093 | <0.001 | Solobacterium_G | **0.001** |
| 0.058 | 0.044 | 0.071 | <0.001 | Acidaminobacter_G | **<0.001** |
| -0.050 | -0.066 | -0.033 | <0.001 | Alkaliflexus_G | **<0.001** |

*the Holm correction

Methanobrevibacter (+0.1 (0.05, 0.17) pp in the IBS group) is a genus of archaea from the group of methanogenic archaea capable of producing methane as a byproduct of their anaerobic lifestyle. These microbes typically inhabit low-oxygen environments such as animal stomachs and other sites where organic matter decomposition occurs. Flavobacterium (-0.1 (-0.12, -0.08) pp in the IBS group) is not a typical member of the human flora and is usually not found in the normal microbiota of the human body. However, some species of Flavobacterium can cause infections in humans, especially in individuals with weakened immune systems. Senegalimassilia (+0.08 (0.05, 0.11) pp in the IBS group) - is a bacterial genus, research on which in human microbiota is limited and poorly represented in the scientific literature.

Further, the analysis on correlation between the presence of serotonin-producing bacteria in the microbiota of patients and their health condition was conducted. Serotonin as a neurotransmitter promotes intestinal movement and secretion, and its excess may lead to chronic diarrhea [5]. Its high levels may cause anxiety, while its low levels are associated with depression [6-7]. It is known that 95% of total serotonin in the body is produced in the gastrointestinal tract, while only 5% of the remaining serotonin is found in the brain [8]. However, the data on the correlation of serotonin-producing bacteria and IBS is contradictory. We employed a generalized linear mixed model (glmer from the lme4 package) to explore their relationship. The model considered random effects to correct for batch effects at the research level (research_id covariate). The analysis was conducted for G taxa. As a result, no statistically significant association was found between the presence of serotonin-producing bacteria and the diarrheal type of IBS (p-value of 0.823), which indicates the existence of other mechanisms of IBS development and the necessity for further research.

In order to perform classification of diagnosis (Healthy or IBS) machine learning algorithm Random Forest was used. Data corrected for batch effect (research ID) was analyzed by Boruta to select variables on taxon G level with confirmed significance. Random Forest was educated on this selected data, and tested on data of research 4, this is the only research in which both healthy subjects and subjects with IBS were enrolled. Our model has specificity 0,78 and sensitivity 0,61, which indicates that it has a lower type I error rate and the model can reject healthy patients without a condition at acceptable level.  

**References** 

1. Shaikh, S. D., Sun, N., Canakis, A., Park, W. Y., & Weber, H. C. (2023). Irritable Bowel Syndrome and the Gut Microbiome: A Comprehensive Review.
Journal of clinical medicine, 12(7), 2558. <https://doi.org/10.3390/jcm12072558>;

2. Pittayanon, R., Lau, J.T., Yuan, Y., et al. (2019). Gut Microbiota in Patients With Irritable Bowel Syndrome-A Systematic Review. Gastroenterology, 157(1),
97-108. <https://doi.org/10.1053/j.gastro.2019.03.049>;

3. Shaikh, S. D., Sun, N., Canakis, A., Park, W. Y., & Weber, H. C. (2023). Irritable Bowel Syndrome and the Gut Microbiome: A Comprehensive Review. Journal of clinical medicine, 12(7), 2558. https://doi.org/10.3390/jcm12072558;

4. Pittayanon, R., Lau, J.T., Yuan, Y., et al. (2019). Gut Microbiota in Patients With Irritable Bowel Syndrome-A Systematic Review. Gastroenterology, 157(1), 97-108. https://doi.org/10.1053/j.gastro.2019.03.049;

5. Gros, M., Gros, B., Mesonero, J. E., & Latorre, E. (2021). Neurotransmitter Dysfunction in Irritable Bowel Syndrome: Emerging Approaches for Management. Journal of clinical medicine, 10(15), 3429. https://doi.org/10.3390/jcm10153429;

6. Jenkins, T. A., Nguyen, J. C., Polglaze, K. E., & Bertrand, P. P. (2016). Influence of Tryptophan and Serotonin on Mood and Cognition with a Possible Role of the Gut-Brain Axis. Nutrients, 8(1), 56. https://doi.org/10.3390/nu8010056;

7. Colle, R., Masson, P., Verstuyft, C., Fève, B., Werner, E., Boursier-Neyret, C., Walther, B., David, D. J., Boniface, B., Falissard, B., Chanson, P., Corruble, E., & Becquemont, L. (2020). Peripheral tryptophan, serotonin, kynurenine, and their metabolites in major depression: A case-control study. Psychiatry and clinical neurosciences, 74(2), 112–117. https://doi.org/10.1111/pcn.12944;

8. Khan, W. I., & Ghia, J. E. (2010). Gut hormones: emerging role in immune activation and inflammation. Clinical and experimental immunology, 161(1), 19–27. https://doi.org/10.1111/j.1365-2249.2010.04150.x.
