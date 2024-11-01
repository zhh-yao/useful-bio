# Remind me of some useful commands


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


## :tiger: Edit files about prefix 'chr'
If you want to rename header without prefix 'chr'
```shell
cat ref.fa | sed 's/>chr/>/g' > ref_noPrefix.fa
cat name.bed sed 's/^chr//' > name_noPrefix.bed
samtools view -h name.bam | sed 's/chr//g' | samtools view -Shb - -o name_noPrefix.bam
```
or vice versa, rename bam files into files with the prefix 'chr'
```
for file in *.bam
do
    filename=`echo $file | cut -d "." -f 1`
    samtools view -H $file | sed -e 's/SN:\([0-9XY]\)/SN:chr\1/' -e 's/SN:MT/SN:chrM/' | samtools reheader - $file > ${filename}_chr.bam
done
```
Reference or more details: [Here](https://www.biostars.org/p/119295/) and [Here](https://www.biostars.org/p/13462/) from Biostars.


## :rabbit: Downsampling bam file
```shell
samtools view -bs 99.2 input.bam > output.bam
```
where 99.2 represent sampling 20% of input bam file with seed 99.


## :dragon_face:



## Trivia

Tools might be used:
- [Samtools](https://www.htslib.org/doc/samtools-depth.html)


Emojis before each sub-section are planned to be arranged in the following order:

:hamster: -> :cow: -> :tiger: -> :rabbit: -> :dragon_face: -> :snake:	-> :horse: -> :sheep: -> :monkey_face: -> :baby_chick: -> :dog: -> :pig: ->

which represents [Chinese zodiac](https://en.wikipedia.org/wiki/Chinese_zodiac) in a repeating twelve-year cycle. It can also be fun to use [Chinese Zodiac Calculator](https://www.travelchinaguide.com/intro/social_customs/zodiac/) to find your lucky animal!
