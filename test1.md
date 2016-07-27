## 1. RNA isolation and quality control

RNA were isolated from floral tissue using Trizol.

A BioAnalyzer picoRNA chip was performed on samples to determine quality.

## 2. Library construction

Performed using 1 ug of total RNA, was not DNase treated.

## 3. Sequencing of libraries

Spiked in 1% of a HiSeq 4000 SR50 lane.

Obtained ~2 million reads per sample.

## 4. Analysis

To first obtain transcript files for the Arabidopsis TAIR10 genome. Downloaded the GFF3 gene annotations, and made a GFF3 file that does not contain the chromosomes. 

      
      bedtools getfasta -fi TAIR10_all.fas -bed TAIR10_GFF3_genes_nochrom.gff -fo TAIR10_transcripts.fa
      

Index the transcripts from using salmon.

      
      salmon index --index TAIR10_index --transcripts TAIR10_transcripts.fa --type quasi
      

Make quant files from all the reads using salmon.

      
      for i in *.fq
      do
        salmon quant -i ~ekhtan/genomes/salmon/TAIR10_index/ --l SF -r $i -o $i'_quant'
      done
      

