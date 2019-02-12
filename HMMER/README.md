## Command line hmmsearch

"What is an Hidden Markov Model?" ([PDF](https://github.com/hseifert/MarMic_BioInf_Teaching/blob/master/HMMER/hmm_primer.pdf))

1. Download the file `marmic_mcrA.fa` from [here](https://github.com/hseifert/MarMic_BioInf_Teaching/blob/master/HMMER/marmic_mcrA.fa).

`add wget [link to the file (better if included in double quotes)]`

  The file contains 15 aligned mcrA sequences, which represent the alpha subunit of methyl coenzyme M reductase, also called coenzyme-B sulfoethylthiotransferase. This enzyme, with alpha, beta, and gamma subunits, catalyzes the last step in methanogenesis.

2. Now you will build your own HMM profile with hmmbuild. The process is simple:

  • collect sequences from members of a protein family (already done)

  • create a multiple sequence alignment (already done)

  • construct an HMM profile that expresses the characteristics of protein family.

First have a look at the usage and options of hmmbuild program by typing:

`/bioinf/software/hmmer/hmmer-3.1b2/bin/hmmbuild -h`

To build the HMM profile type:

`/bioinf/software/hmmer/hmmer-3.1b2/bin/hmmbuild --informat afa --amino mcrA.hmm marmic_mcrA.fa`

Take a look at the profile file (`mcrA.hmm`), does it look similar to those you have seen in PFAM?

3. Now we want to use this profile to search for mcrA in other organisms. For the sake of results, we will perform an HMM search on the genome of *Methanopyrus kandleri* AV19, but you can use this profile to search for mcrAs in any other genome or metagenome sequence.

Go to the NCBI Genomes page; find, and download the genome sequence of *Methanopyrus kandleri* AV19 in fasta format, make sure you download the amino acid sequences (or open reading frames), not the nucleotides!

`wget [link to protein_file_name]`

Again, have a look at the usage and options of hmmsearch program by typing:

`/bioinf/software/hmmer/hmmer-3.1b2/bin/hmmsearch -h`

Now time for the HMM search:

`/bioinf/software/hmmer/hmmer-3.1b2/bin/hmmsearch mcrA.hmm [genome_fasta_name_here] > mcrA_methanpy.out`

In the output file:

- The first section is the header that tells you what program you ran, on what, and with what options.

- The second section is the sequence top hits list. It is a list of ranked top hits (sorted by E-value, most significant hit first), formatted in a BLAST-like style. The last two columns, obviously, are the name of each target sequence and optional description. The most important number here is the first one, the sequence E-value. This is the statistical significance of the match to this sequence.

  - How many hits to the mcrA.hmm profile are there with an E-value better than E-10?
  - Is *Methanopyrus* a methanogen?
