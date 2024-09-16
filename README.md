# Remind me of some useful commands

Tools might be used:
- [Samtools](https://www.htslib.org/doc/samtools-depth.html)


## :hamster: Calculate sequencing depth of bam file

Sequencing depth of whole genome
```shell
samtools depth file.bam | awk '{sum+=$3} END { print "Average = ",sum/NR}'
```

Sequencing depth of covered regions
```shell
samtools depth -a file.bam | awk '{sum+=$3} END { print "Average = ",sum/NR}'
```

## :cow: Edit header of bam file

Change `old` string to `new` 
```shell
samtools view -H file.bam | sed "s/old/new/" | samtools reheader - file.bam
```

Or achieve this step by step
```shell
samtools view -H file.bam > header.sam
sed "s/old/new/" header.sam > header_new.sam
samtools reheader header_new.sam file.bam
```

## :tiger: Reheader files with no prefix 'chr'
If you want to rename header without prefix 'chr'
```shell
cat ref.fa | sed 's/>chr/>/g' > ref_noPrefix.fa
cat name.bed sed 's/^chr//' > name_noPrefix.bed
samtools view -h name.bam | sed 's/chr//g' | samtools view -Shb - -o name_noPrefix.bam
```
Reference or more details: [biostars](https://www.biostars.org/p/119295/#119462).

## :rabbit: 


## Trivia

Emojis before each sub-section are planned to be arranged in the following order:

:hamster: -> :cow: -> :tiger: -> :rabbit: -> :dragon_face: -> :snake:	-> :horse: -> :sheep: -> :monkey_face: -> :baby_chick: -> :dog: -> :pig: ->

which represents [Chinese zodiac](https://en.wikipedia.org/wiki/Chinese_zodiac) in a repeating twelve-year cycle. It can also be fun to use [Chinese Zodiac Calculator](https://www.travelchinaguide.com/intro/social_customs/zodiac/) to find your lucky animal!
