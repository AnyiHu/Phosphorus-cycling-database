# Phosphorus-cycling-database (PCyCDB)
This is a curated phosphorus cycling database (PCyCDB) with 117 gene families and 10 clusters. 
Homologous genes were added into the database to reduce the false positive rate. The criteria (i.e., identity, hit length) for filtering the alignment result generated by sequence similarity searching tools (e.g., BLAST, USEARCH, DIAMOND) were refined by identifying a known simulated gene dataset and mock bacteria community to obtain the best accuracy and further reduction of false positives and false negatives. The accuracy, PPV, sensitivity, specificity and NPV were 99.76%, 95.70%, 99.94%, 99.74% and 99.99%, respectively, at the 70% identity and 25 amino acid cutoffs. 
Importantly, the genes encode the intracellular phosphorus metabolic processes were added into PCyCDB, which should help researchers broaden the insights into not only the geochemical P cycling but also the microbial P metabolisms.

User guide:
1. Assuming you had a sample named $Sample.fa, and obtained a blast table named Sample.P.blast using BLAST+ or DIAMOND or other alignment tools, you can filter the result using filter_Generate_ORF2gene.py. 
Command: python filter_Generate_ORF2gene.py -s $identity -cov $alignment-coverage -hit $hitlength -b $Sample.P.blast
By doing this, you will obtain a ORF2gene file named $Sample.ORF2gene.txt, which descripts the P cycling gene for each ORF.
If you have a lot of sample for analysis, a bash for loop is recommend for quickly processing the data. For example:
for i in $Sample*.blast;do python filter_Generate_ORF2gene.py -s $identity -cov $alignment-coverage -hit $hitlength -b $i;done

2. Assuming you already have calculated the coverage (or TPM) using Bowtie2, CheckM, Salmon or other tools, and obtained a abuncance file named $Sample.quant for all ORFs, you can easily extracted the abuncance of PCGs using Coverage_get.py.
Command: python Coverage_get.py -i $Sample.ORF2gene.txt -t $Sample.quant -o $Sample.P.profile.txt