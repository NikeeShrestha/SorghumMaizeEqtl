
# Path of files for eQTL analsyis

To macth the order pf phenotype files and genotype file use the order from mvp based geno.ind data as a reference. 

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

- Number of genotypes used: 811
- Number of markers used: 180,520

## Genotype data

-  /work/schnablelab/nikees/vla_karla/input/mvp.geno.*

## Phenotype data

- /work/schnablelab/nikees/vla_karla/input/counts.NE2021.811.filtered_bcSP.orderSampler.ordered.txt

Genotype data was filtered to exclude markers with MAF < 0.05 considering only homozygous alleles and markers with heterozygosity > 0.05.

Only biallelic markers were included. The total number of PCs used in the GWAS was 3 for both sorghum and maize eQTL. 

Parameters for rMVP used:

imMVP <- MVP(
    phe=ph[, c(1, i)],
    geno=geno,
    map=map,
    K=Kinship,
    nPC.MLM=3,
    maxLoop=10,
    vc.method="EMMA",
    method=c("MLM"),
    file.output=c("pmap.signal"),
    p.threshold = 0.05 / nrow(map)
  )
