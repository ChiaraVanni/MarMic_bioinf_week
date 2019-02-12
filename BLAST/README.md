## Command line BLAST

"Database searching for similar sequences" ([PDF](https://github.com/ChiaraVanni/MarMic_bioinf_week/blob/master/BLAST/Database_Searching_for_Similar_Sequences.pdf))

Normally (but not today because everything is installed) you need a local BLAST installation, as well as locally stored databases to search against (download weekly updates from NCBI: nr, nt, or your own personal sequence databases)

Sequence database: specially formatted multifasta file of sequences. Remember multifasta format: (in this example: nucleotide sequences; can be also protein sequences!):

1. You want to format a 16S rRNA database

  • Find the files `marmic_aquificae_db.fasta.tar.gz` (database) and `marmic_16Sseq.fasta.tar.gz` (query) [here](https://github.com/ChiaraVanni/MarMic_bioinf_week/tree/master/BLAST/data)

  • Download the files to your directory and extract the archives using the following command in your terminal:

  ```
  wget (link to the file, better if in double quotes)
  tar -zxvf [filename_here]
  ```

2. Have a look at your files and see if everything seems right (you’re supposed to have a multifasta files with nucleotide sequences); use the command:

  `more [filename_here]`

  How many sequences are in the files? To find out, count the “>” of the header lines by typing:

  `grep -c "^>" [filename_here]`

3. Now you can start using the command line blast. Firstly you need to have the blast programs in your default path. To do this, type the command below:

  `export PATH=$PATH: /bioinf/software/blast+/blast+-2.2/bin`

  - Check the usage and options for the ‘makeblastdb’ program:

    `makeblastdb -help`

  - Now do the formatting of the 16S rRNA database (marmic_aquificae_db). Check with the help to see if the command given below is correct.

    `makeblastdb –in [filename_here] –dbtype nucl –parse_seqids -out [databasename_here] -title “[title_here]”`

4. Now you want to compare the query sequences against all the sequences in the database

    - Type `blastn -help` to see the syntax and options of blastn program

    - Now time for the blast search:

    `blastn -task blastn -db [databasename_here] -query [queryfilename_here] – evalue 0.00001 –perc_identity 97 -out [outputfilename_here] –outfmt “6 sacc qacc qstart qend sstart send qseq evalue pident bitscore”`

  When the process is finished you are notified and can look at the output file to check the results.

5. In order to make more sense of the output and results, you will need to retrieve additional information from the blast database.

  - First type in the following command to retrieve the subject accession numbers as a list from the output file.

  `cut –f 1 [outputfilename_here] > sbj_acc.txt`

  - Now you will use the blastdbcmd, which is a program used to examine contents of a blast database. In our case, we will try to retrieve the corresponding taxonomic classifications of the subject sequences.

  `blastdbcmd –db [databasename_here] –entry_batch [sbj_acc.txt] –outfmt “%a %t ” > tax.txt`

  - Now we want to join the output file, and the taxonomic classification.

  `join [outputfilename_here] tax.txt > classified_out.txt`

If you look into the new output file, you will see that each of your query sequences now has a taxonomic classification.
