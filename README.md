
# Path of files for eQTL analsyis

To match the order pf phenotype files and genotype file use the order from mvp based geno.ind data as a reference. 

You can use the command in R as :

genoList <- read.table("mvp_maize.geno.geno.ind", header = F)
colnames(genoList) <- "taxa"

pheno <- read.csv("counts.NE2020.693.filtered_bcSP.orderSampler.ordered_coeff.txt", header = T, sep='\t')

ph <- plyr::join(genoList, pheno, by="taxa")

# Maize

- Number of genotypes used: 693
- Number of markers used: 9,673,152

## Genotype data

- /work/schnablelab/nikees/vla_karla/input/mvp_maize.geno.*

##  Phenotype data

- /work/schnablelab/nikees/vla_karla/input/counts.NE2020.693.filtered_bcSP.orderSampler.ordered_coeff.txt

# Sorghum

- Number of genotypes used: 648
- Number of markers used: 4,692,581 (4,167,091 SNPs and 525,490 indels)

## Genotype data

- `/work/schnablelab/nikees/sorghumeqtl/data/mvp_sorghum_648.geno.*`

## Phenotype data

- `/work/schnablelab/nikees/sorghumeqtl/data/counts.NE2021.648.filtered_bcSP.orderSampler.ordered.txt`

Genotype data was filetered to exclude markers with MAF < 0.05 considering only homozygous alleles and heterozgotes > 0.05 from this file: `/work/schnablelab/nikees/sorghumeqtl/data/SAP_BQSR_imputed_allchr_snps_renamed.vcf.gz`

Only biallelic markers were included. The total number of PCs used in the GWAS were 3 for both sorghum and maize eQTL. 

Parameters for rMVP used:

 imMVP <- MVP(
    phe=ph[, c(1, i)],
    geno=geno,
    map=map,
    K=Kinship,
    nPC.MLM=3,
    #ncpus=16,
    maxLoop=10,
    vc.method="EMMA",
    method=c("MLM"),
    file.output=c("pmap.signal"
    )
    
    
## How did I generate the markers for sorghum?

## Filtering markers

Filtered with missing rate<0.5, multiallelic marker, InbreedingCoeff>0, MAF>0.01 using two files `SAP_BQSR_filtered_snps.vcf.gz` and `SAP_BQSR_filtered_indels.vcf.gz`

Imputed biallelic genetic markers: 8,864,198 SNPs and 2,207,670 indels --> Total markers: 11,071,868

The imputed vcf file is located in this path: `/mnt/nrdstor/schnablelab/nikees/sorghum_new_WGS/SAP_BQSR_imputed_allchr_sns_indels_renamed.vcf.gz`

Filtered for 648 individuals present in RNAseq dataset

Filtered for MAF 0.05 and heterozygousity 0.05: 4,167,091 SNPs and 525,490 indels --> final total markers used for GWAS analysis: 4,692,581
