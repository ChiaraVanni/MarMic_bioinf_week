## Dynamic programming

"What is dynamic programming?" ([PDF](https://github.com/ChiaraVanni/MarMic_bioinf_week/blob/master/Dynamic_progr/dynamicprogramming_primer.pdf))

1. Why do we need to do sequence comparisons?
2. What do you need for an assessment of how similar 2 sequences are to
each other?
3. “Align” the following symbol sequences by hand, i.e. position
identical letters vertically to each other and connect them by a vertical line. Represent gaps (insertions, deletions) by “-“

```
D A R L I N G

A I R L I N E
```

4. Which edit-operations do you know?
a. What is the unit cost model
b. Calculate identity and edit-distance of the sequences in exercise 3.
c. Now, calculate the identity score of your alignment in 3

5. Calculate the similarity score according to the BLOSUM62
substitution matrix ([here](https://github.com/ChiaraVanni/MarMic_bioinf_week/blob/master/Dynamic_progr/BLOSUM62.jpg)) for the following alignment.

```
SKLQETMKCV
|| ||| | |
SKGQETIKMV
```

7. Construct a “dotplot” for the following 2 sequences, i.e. for identical symbols, mark the respective square by a diagonal: What does the alignment look like? (is more than one alignment possible?)

![da_matrix1](https://github.com/ChiaraVanni/MarMic_bioinf_week/blob/master/Dynamic_progr/assets/da_matrix1.png)

8. What is “Dynamic Programming” (DP)?

9. Calculate the Dynamic Programming-Matrix for a global alignment
(Needleman-Wunsch algorithm) and infer the optimal global alignment(s) for the given sequences.

  Scoring: s(a,a) = 1; s(a,b) = -1; s(a,-) = s(-,a) = -1

![da_matrix2](https://github.com/ChiaraVanni/MarMic_bioinf_week/blob/master/Dynamic_progr/assets/da_matrix2.png)

a. How is the matrix initialized for a global alignment?

b. Why?

c. Which three cases have to be checked for each cell of the
matrix?

d. Where in the matrix is the trivial solution of the DP approach stored?

e. With respect to the comparison of the two sequences: what does each cell of the 2D-matrix stand for?

10. Calculate the Dynamic Programming-Matrix for a local alignment (Smith-Waterman algorithm) and infer the optimal local alignment for the given sequences.

  Scoring: s(a,a) = 1; s(a,b) = -1; s(a,-) = s(-,a) = -1

![da_matrix3](https://github.com/ChiaraVanni/MarMic_bioinf_week/blob/master/Dynamic_progr/assets/da_matrix3.png)

  a. How is the matrix initialized for a local alignment?

  b. Why?

  c. Which additional criterion (compared to the global DP matrix)
     has to be added in the evaluation of each cell of the matrix?

  11. Two sequences (S1 and S2) encode proteins of different domain architecture. S1 and S2 are to be compared by means of a dotplot. Consider the following cases and draw the corresponding dotplots:

     a. S1 and S2 are identical

     b. S1 and S2 have only one similar domain at their 5’-ends

     c.  S1 and S2 each consist of 2 domains that are similar in the two
      sequences but their order is switched

     d. S1 and S2 each consist of 2 domains that are similar in the two sequences but the 5’¬terminal domain of S1 is inverted in S2

     e. S2 lacks the middle domain of 3 S1 domains

     f. S2 consists of a repeat of 3 domains that are similar to the 5'-terminal domain of 3 S2 domains
