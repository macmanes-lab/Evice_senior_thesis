================================================
Use BWA to look for bacteria using raw reads
================================================

**Download** Wolbachia genome (you maybe did this already). Once downloaded, index the file using ``bwa index`` to make it usable for mapping

::
  cd /home/evice/harmonia/genome/
  bwa index -p wolbachia /home/evice/harmonia/WOLBACHIA.FILE.FASTA

Once that command is completed, you can do the mapping. 

::

  interleave-reads.py \
  harm1.fq \
  harm2.fq \
  | skewer -Q 5 -t 2 -x $SCRATCH/adapters.fa - -1 \
  | extract-paired-reads.py -p - -s /dev/null - \
  | bwa mem -p -t 4 wolbachia - \
  | samtools view -T . -F4 -bu - \
  | samtools sort -l 0 -O bam -T tmp -@ 2 -o wolbachia.bam -
  
This command will take a long time (maybe 24 hours). When it is done, do the same thing, but with spiroplasma. Note that you have several places where the names have to be changed from wolbachia to spiroplasma. 
