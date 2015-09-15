=====================
BLAST instructions
=====================

1. Find a sequence from Wolbachia and/or Spiroplasma on genbank (http://www.ncbi.nlm.nih.gov/genbank/). I think a 
simple text search should suffice, at least in the beginning. You'll want the fasta sequence. It may be easier to copy and paste the 
sequence for short things, and download longer things.. 

2. If copy/paste, in the terminal type:

::

  nano query01.fasta

This command will open up a text editor --> paste in the sequence and type  ``control-x`` to exit, ``y`` to save, then ``enter``

3. Now you are ready to blast: 

::

  makeblastdb -in harmonia_genome.fasta -out harmonia -dbtype nucl

This makes the blast database from the harmonia genome, you only have to do this the 1st time.

::

  blastn -evalue 8e-8 -num_threads 8 -db harmonia -query query01.fa -max_target_seqs 3 -outfmt "6 qseqid pident evalue stitle" > query01.blastn
  
This should only take a few seconds (I hope). To look at the results, type:

::

  more query01.blastn
  
For each sequence you find on Genbank, you'll need to make a new query file.. So, instead of ``nano query01.fasta`` you'll type ``nano query02.fasta``. Also, in the blast search you typed ``-query query01.fa``, that will need to be changed as well to ``-query query02.fa``. **Lastly**, the output file for the blast needs to be changed as well, ``> query02.blastn``

