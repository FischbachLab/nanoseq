Hello world script
====================

A simple test script showing the nanoseq pipeline for the Nextflow framework on aws.


# Default test job with GPU
```{bash}
aws batch submit-job \
    --job-name nf-nanoseq-gpu-test \
    --job-queue priority-maf-pipelines \
    --job-definition nextflow-production \
    --container-overrides command="s3://nextflow-pipelines/nf-nanoseq, \
"-profile", "test,docker", \
"--guppy_gpu", "true",\
"--guppy_cpu_threads", "1", \
"--guppy_gpu_runners","6", \
"--gpu_device","auto", \
"--outdir","s3://genomics-workflow-core/Results/Nanoseq/test-gpu" "
```

# Using MITI profile with GPU
```{bash}
aws batch submit-job \
    --job-name nf-nanoseq-gpu-MITI \
    --job-queue priority-maf-pipelines \
    --job-definition nextflow-production \
    --container-overrides command="s3://nextflow-pipelines/nf-nanoseq, \
"-profile", "MITI,docker", \
"--input", "s3://genomics-workflow-core/Results/Nanoseq/run1/SampleSheet_20220722_2139_MN19452_FAQ74537_830f0db9.csv", \
"--input_path", "s3://czb-seqbot/nanopore/220722_MN19452_0090_FAQ74537/BC-GF_ICLV-etOH_ICLV-bead_IDLV-bead/20220722_2139_MN19452_FAQ74537_830f0db9/fast5/", \
"--outdir","s3://genomics-workflow-core/Results/Nanoseq/run1-gpu" "
```

# Full options with GPU
```{bash}
aws batch submit-job \
    --job-name nf-nanoseq-gpu \
    --job-queue priority-maf-pipelines \
    --job-definition nextflow-production \
    --container-overrides command="s3://nextflow-pipelines/nf-nanoseq, \
"-profile", "docker", \
"--guppy_gpu", "true",\
"--guppy_cpu_threads", "1", \
"--guppy_gpu_runners","4", \
"--gpu_device","auto", \
"--protocol", "DNA", \
"--flowcell", "FLO-MIN106", \
"--kit", "SQK-LSK109", \
"--barcode_kit", "EXP-NBD114", \
"--trim_barcodes", "true", \
"--output_demultiplex_fast5", "true", \
"--run_nanolyse", "true", \
"--skip_alignment", "true", \
"--skip_quantification", "true", \
"--skip_fusion_analysis", "true", \
"--skip_modification_analysis", "true", \
"--input", "s3://genomics-workflow-core/Results/Nanoseq/run1/SampleSheet_20220722_2139_MN19452_FAQ74537_830f0db9.csv", \
"--input_path", "s3://czb-seqbot/nanopore/220722_MN19452_0090_FAQ74537/BC-GF_ICLV-etOH_ICLV-bead_IDLV-bead/20220722_2139_MN19452_FAQ74537_830f0db9/fast5/", \
"--outdir","s3://genomics-workflow-core/Results/Nanoseq/run1" "
```

# options with basecalling but no demultiplexing on 16S samples with GPU and sup (super-accurate basecalling) model
# output one fastq file only
#"--flowcell", "FLO-FLG001", \
#"--kit", "SQK-LSK109", \
```{bash}
aws batch submit-job \
    --job-name nf-nanoseq-16S \
    --job-queue priority-maf-pipelines \
    --job-definition nextflow-production \
    --container-overrides command="s3://nextflow-pipelines/nf-nanoseq, \
"-profile", "docker", \
"--guppy_gpu", "true", \
"--protocol", "DNA", \
"--guppy_config", "dna_r9.4.1_450bps_sup.cfg", \
"--guppy_model","template_r9.4.1_450bps_sup.jsn", \
"--skip_demultiplexing", "true", \
"--trim_barcodes", "false", \
"--output_demultiplex_fast5", "false", \
"--skip_alignment", "true", \
"--skip_quantification", "true", \
"--skip_fusion_analysis", "true", \
"--skip_modification_analysis", "true", \
"--input", "s3://maf-sequencing/nanopore/220914_Flongle16S_ALB873/no_sample/220914_2335_MC-114227_ALB873_558bf20f/samplesheet_220914_Flongle16S_ALB873.csv", \
"--input_path", "s3://maf-sequencing/nanopore/220914_Flongle16S_ALB873/no_sample/220914_2335_MC-114227_ALB873_558bf20f/fast5/", \
"--outdir","s3://genomics-workflow-core/Results/Nanoseq/220914_Flongle16S_ALB873" "
```

# Guppy v6.4.2 with the new flowcell and kit
```{bash}
aws batch submit-job \
    --job-name nf-nanoseq-16Spilot \
    --job-queue priority-maf-pipelines \
    --job-definition nextflow-production \
    --container-overrides command="s3://nextflow-pipelines/nf-nanoseq, \
"-profile", "docker", \
"--guppy_gpu", "true", \
"--protocol", "DNA", \
"--flowcell", "FLO-FLG114", \
"--kit", "SQK-LSK114", \
"--guppy_config", "dna_r10.4.1_e8.2_400bps_sup.cfg", \
"--guppy_model","template_r10.4.1_e8.2_400bps_sup.jsn", \
"--skip_demultiplexing", "true", \
"--trim_barcodes", "false", \
"--output_demultiplex_fast5", "false", \
"--skip_alignment", "true", \
"--skip_quantification", "true", \
"--skip_fusion_analysis", "true", \
"--skip_modification_analysis", "true", \
"--input", "s3://genomics-workflow-core/Results/Nanoseq/20221211_Flongle10_4_1_pilot/20221214_16Spilot.csv", \
"--input_path", "s3://maf-sequencing/nanopore/Nathan_Johns/20221211_FlongleTest/20221211_Flongle10_4_1_pilot/no_sample/20221212_0008_MN37738_ANV909_5a4e9ab8/fast5/", \
"--outdir","s3://genomics-workflow-core/Results/Nanoseq/20221211_Flongle10_4_1_pilot_400bps_sup" "
```
