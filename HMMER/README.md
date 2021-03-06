## Command line hmmsearch

"What is an Hidden Markov Model?" ([PDF](https://github.com/ChiaraVanni/MarMic_bioinf_week/blob/master/HMMER/hmm_primer.pdf))

1. Go to the folder `MarMic_bioinf_week/HMMER`, in `data/` you can find the file `marmic_mcrA.fa`

The file contains 15 aligned mcrA sequences, which represent the alpha subunit of methyl coenzyme M reductase, also called coenzyme-B sulfoethylthiotransferase. This enzyme, with alpha, beta, and gamma subunits, catalyzes the last step in methanogenesis.

2. Now you will build your own HMM profile with hmmbuild. The process is simple:

  • collect sequences from members of a protein family (already done)

  • create a multiple sequence alignment (already done)

  • construct an HMM profile that expresses the characteristics of protein family.

First have a look at the usage and options of hmmbuild program by typing:

`export PATH=/bioinf/software/hmmer/hmmer-3.1b2/bin:$PATH`

`hmmbuild -h`

To build the HMM profile type:

`hmmbuild --informat afa --amino mcrA.hmm data/marmic_mcrA.fa`

Take a look at the profile file (`mcrA.hmm`), does it look similar to those you have in PFAM (have a look at one Pfam domain HMM [here](http://pfam.xfam.org/family/ABC_tran)?

3. Now we want to use this profile to search for mcrA in other organisms. For the sake of results, we will perform an HMM search on the genome of *Methanopyrus kandleri* AV19, but you can use this profile to search for mcrAs in any other genome or metagenome sequence.

Go to the NCBI Genomes page; find, and download the genome sequence of *Methanopyrus kandleri* AV19 in fasta format, make sure you download the amino acid sequences (or open reading frames), not the nucleotides!

`wget [link to genome_protein_file_name]`

<!---
`wget "ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/007/185/GCA_000007185.1_ASM718v1/GCA_000007185.1_ASM718v1_protein.faa.gz"`
--->

Unzip the file:

`gunzip [genome_protein_file_name]`

Again, have a look at the usage and options of hmmsearch program by typing:

`hmmsearch -h`

Now time for the HMM search:

`hmmsearch mcrA.hmm [genome_protein_file_name] > mcrA_methanpy.out`

In the output file:

- The first section is the header that tells you what program you ran, on what, and with what options.

- The second section is the sequence top hits list. It is a list of ranked top hits (sorted by E-value, most significant hit first), formatted in a BLAST-like style. The last two columns, obviously, are the name of each target sequence and optional description. The most important number here is the first one, the sequence E-value. This is the statistical significance of the match to this sequence.

  - How many hits to the mcrA.hmm profile are there with an E-value better than E-10?
  - Is *Methanopyrus* a methanogen?
