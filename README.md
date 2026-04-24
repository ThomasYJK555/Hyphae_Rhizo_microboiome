# Hyphae_Rhizo_microboiome
Microbiome analysis for fungal hyphaea and rhizosphere of different vegetables
The fungal hyphae samples and rhizosphere samples from bitter melons, peppers, eggplants, and cucumbers were collected from Yuanmou and Huanian. Shotgun metagenome sequencing was performed to analyze the fungal hypae microbiome and rhizosphere microbiome from nematode-infected and healthy plants.
# Workflow for metagenomic data
1. Quality control
   Paired-end raw reads were processed by fastp (v0.23.4) and bowtie2 (v2.5.4) to remove low-quality and host genome contaminations.
2. Contig Assembly
   Megahit (v1.1.3) was used to assemble the clean reads into contigs.
3. Taxonomy analysis based on reads
   Paired-end clean reads were taxonomy classified using Metaphlan4 (v4.0.6, database version 202503).
4. Metagenomic binning
   Assembled contigs with lengths over 1000 bp were binned into draft genomes using metabat2, concoct in metaWRAP (v1.3.2)，and bin_refinement module was applied to refine the bins from metabat2 and concoct.
5. Reference microbial genome catalog construction
   Refined MAGs from this study were integrated with the SMAG dataset, which contains over 40,000 MAGs. The reference microbial genomes catalog of species-level genome bins (SGBs) was built by clustering all the MAGs into species-level bins (SGBs) according to 95% ANI using dRep.
6. Reference microbial genome abundance calculation
   All the clean data of samples were mapped to reference genomes directory to calculate the TPM abundance of each sample using CoverM (v0.7.0)
7. MAGs-based taxonomy and function analyses
   Reference genomes were taxonomy classified with GTDBTk, and the ORFs of each genome were annotated using kofam_scan (v1.3.0) to obtain the KO (KEGG Orthology) profiles.
   Each SGB was subjected to run_dbcan (v4.1.4) to annotate the CAZy modules profile as well as CGCs and PULs, and their substrates.
   Each SGB was subjected to AntiSMASH (v8.0) to annotate the Biosynthesis gene clusters (BGCs), and BiG-SCAPE (v2.0) was implemented to cluster the GCFs for each BGC.
