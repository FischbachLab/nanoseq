Hello world script
====================

A simple test script showing the nanoseq pipeline for the Nextflow framework on aws.


# Test
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

# Using MITI profile
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

# Real datasets
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
