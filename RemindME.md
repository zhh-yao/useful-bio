# Remind me of some useful commands

## Calculate sequencing depth of bam file with samtools


### Sequencing depth of whole genome
```shell
samtools depth file.bam | awk '{sum+=$3} END { print "Average = ",sum/NR}'
```

### Sequencing depth of covered regions
```shell
samtools depth -a file.bam | awk '{sum+=$3} END { print "Average = ",sum/NR}'
```

Full instruction of `samtools depth` can be found [HERE](https://www.htslib.org/doc/samtools-depth.html)
