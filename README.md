# DRD2-gene-RAG
### Eli Hiton

## Introduction
Through the work of the Human Genome Project and research since then, there is a bounty of genetics knowledge. Unfortunately, this research is spread across numerous databases and research papers. For a doctor wanting a quick question answered to a pharmaceutical researcher looking for a broad survey of a topic, sifting through this research might not be feasible. This project demonstrates the use of the RAG technique to answer questions about the DRD2 gene.

## Data Pipeline
Using Entrez all abstracts matching the query DRD2 AND ("pharmacogenetics" OR "therapeutic use" OR "adverse effects" OR "drug response" OR "clinical trials") were retrieved from Pubmed. The title, abstract, authors, and dates were retrieved from the abstract and cleaned. Any abstracts lacking any of these items were discarded leaving 617 abstracts. These abstracts were separated into chunks along sentence boundaries ranging in length from ___ to ___ maybe a graphic about chunk size. 

<div align="center">
  <img src="https://github.com/elihiton/DRD2-gene-RAG/blob/main/chunk-length-histogram.png" alt="Chunk Length Histogram">
</div>



These chunks were embedded with all-MiniLM-L6-v2 and stored in a Chroma databases. User queries are passed to the database and relevant chunks are passed to gemini-2.0-flash-lite to generate responses using the retrieved content. Gemini was initialized with one of the following prompts depending on use case:

"You are a RAG system designed to provide useful genetic and genomic information for clinicians to aid their work on
diagnosis, etiology, treatment and anything else they need.
A clinician has entered the query below and the context contains relevant chunks retrieved from a database of research on the DRD2 gene. 
Use as many or as few of the sources as you need to answer the question accurately and concisely. You may also use existing knowledge from your training base.
Please cite studies if applicable.

Context: {context}

Question: {query}"

or

"You are a RAG system designed to provide useful genetic and genomic information for pharmaceutical industry workers to aid their work on
research, development, pharmacovigilance and anything else they need.
A pharmaceutical industry worker has entered the query below and the context contains relevant chunks retrieved from a database of research on the DRD2 gene. 
Use as many or as few of the sources as you need to answer the question accurately and concisely. You may also use existing knowledge from your training base.
Please cite studies if applicable.

Context: {context}

Question: {query}"

## Sample Responses
My patient carries the DRD2/ANKK1 TaqIA A1 allele. How should this influence my prescribing decisions for treating their bipolar disorder?

Patients with the DRD2/ANKK1 Taq1A A1 allele may experience the following:
Treatment with Dextromethorphan (DM): In a study by Lee et al. (2012), patients with the A1A1 genotype showed greater decreases in manic symptoms when treated with add-on DM compared to the A2A2 genotype. This suggests the DRD2/ANKK1 Taq1A polymorphism influences responses to DM in bipolar patients.
Risk of Side Effects: Patients with one or two DRD2 Taq1 A1 alleles are at a greater risk of significant side effects, particularly if they are male, Caucasian, have a schizophrenic or delusional disorder, or are taking strong dopamine D2-receptor antagonistic drugs (Alenius et al., 2008). If this is the case, it may be beneficial to use drugs without strong dopamine D2 receptor antagonistic properties.

My patient experienced severe tardive dyskinesia on risperidone. Is there a DRD2-related genetic test I should order before trying another antipsychotic?

Yes, DRD2 genotyping may be useful. The -141C Del allele of the DRD2 gene has been associated with tardive dyskinesia (TD) (Koning, 2012; Nakazono, 2005). Also, the DRD2 TaqI_D polymorphism has been associated with akathisia (Koning, 2012). The utility of DRD2 information and what to do with genotyping results has not been previously addressed, despite availability on clinical test panels (Eum, 2017). These results suggest that the contribution of these DRD2 gene variants in the vulnerability of antipsychotic-induced MD takes place in a more general or pleiotropic way (Koning, 2012).

Which studies demonstrate the most robust association between DRD2 expression levels and antipsychotic-induced weight gain? I need citations for our pharmacovigilance protocol.

Several studies suggest an association between DRD2 gene variants and antipsychotic-induced weight gain (AIWG). Here are the key findings and citations for your pharmacovigilance protocol:
Muller et al. (2012) found significant associations between three DRD2 SNPs (rs6277, rs1079598, and rs1800497) and AIWG, particularly when stratifying by ethnicity and antipsychotics with the highest weight gain risk.
Hong et al. (2010) identified an association between the DRD2 rs4436578-C homozygous genotype and an increased risk of AIWG in schizophrenic patients treated with clozapine, olanzapine, or risperidone.
Lencz et al. (2010) demonstrated that carriers of the deletion allele of the DRD2 -141C Ins/Del (rs1799732) promoter region polymorphism exhibited significantly more weight gain after 6 weeks of treatment with either risperidone or olanzapine.
Houston et al. (2012) found that the A allele of DRD2 rs2440390(A/G) was associated with greater weight gain.
It is important to note that some studies have not found a significant association between DRD2 and AIWG. For example, Zhang et al. (2003) did not find a significant association between the TaqI A polymorphism of the DRD2 gene and AIWG.


Does genetic testing for DRD2 variants have clinical utility when personalizing addiction treatment approaches?

Yes, genetic testing for DRD2 variants shows clinical utility in personalizing addiction treatment approaches. Several studies support this:
Predicting Treatment Outcomes: DRD2 variants can predict outcomes in addiction treatment. For example, one study found a significant association between the A1 allele of the DRD2 gene and poor outcomes in methadone treatment for opioid dependence. Individuals with the A1 allele also reported higher heroin use prior to the study Lawford, B R et al., 2000).
Identifying Risk: DRD2 polymorphisms, specifically the TaqIA polymorphism, have been linked to an increased vulnerability to addiction. Screening for this marker may help identify individuals at risk (Teh, Lay K et al., 2012).
Pharmacogenetic Approach: DRD2 gene variants have been studied to identify responsiveness to treatment for nicotine addiction (Herman, Aryeh I et al., 2014). Research suggests that integrating genetic information with clinical data can inform health professionals of the most efficacious pharmacotherapeutic intervention for substance use disorders (Patriquin, Michelle A et al., 2015).
Association with Impulsive-Addictive-Compulsive Behavior: Variants of the DRD2 gene have been associated with impulsive-addictive-compulsive behavior (Blum, K et al., 1995).
