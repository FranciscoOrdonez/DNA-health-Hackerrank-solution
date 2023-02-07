# DNA-health-Hackerrank-solution
DNA health Hackerrank solution
DNA is a nucleic acid present in the bodies of living things. Each piece of DNA contains a number of genes, some of which are beneficial and increase the DNA‘s total health. Each gene has a health value, and the total health of a DNA is the sum of the health values of all the beneficial genes that occur as a substring in the DNA. We represent genes and DNA as non-empty strings of lowercase English alphabetic letters, and the same gene may appear multiple times as a susbtring of a DNA.

Given the following:

An array of beneficial gene strings, genes = [g0, g1, . . . , gn-1]. Note that these gene sequences are not guaranteed to be distinct. An array of gene health values, health = [h0, h1, . . . , hn-1], where each hi is the health value for gene gi. A set of s DNA strands where the definition of each strand has three components, start, end, and d, where string d is a DNA for which genes gstart, . . . , gend are healthy. Find and print the respective total healths of the unhealthiest (minimum total health) and healthiest (maximum total health) strands of DNA as two space-separated values on a single line.

Input Format

The first line contains an integer, n, denoting the total number of genes. The second line contains n space–separated strings describing the respective values of g0, g1, . . . , gn-1 (i.e., the elements of genes). The third line contains n space-separated integers describing the respective values of h0, h1, . . . , hn-1 (i.e., the elements of health). The fourth line contains an integer, s, denoting the number of strands of DNA to process. Each of the s subsequent lines describes a DNA strand in the form start end d, denoting that the healthy genes for DNA strand d are gstart, . . . , gend and their respective correlated health values are hstart, . . . , hend.

Constraints

1 <= n, s <= 105 0 <= hi <= 107 0 <= first <= last < n 1 <= the sum of the lengths of all genes and DNA strands <= 2 x 106 It is guaranteed that each gi consists of lowercase English alphabetic letters only (i.e., a to z). Output Format

Print two space–separated integers describing the respective total health of the unhealthiest and the healthiest strands of DNA.

Sample Input 0

6 a b c aa d b 1 2 3 4 5 6 3 1 5 caaab 0 4 xyz 2 4 bcdybc Sample Output 0

0 19

APPROACH 1

1. Read in the number of genes noGenes and the list of genes genes.

2. Read in the list of health values healths corresponding to each gene.

3. Read in the number of DNA strands to be evaluated noStrands.

4. Create a dictionary geneHealthMapping where each key is a gene and its value is a list of two lists. The first list contains the indices of the gene in the original list of genes, and the second list contains the cumulative sum of the health values of the gene up to that index.

5. Create a set groupOfSets which stores all possible substrings of genes of length less than or equal to 500.

6. Loop through the noStrands DNA strands to be evaluated. For each strand: a. Read in the first and last indices first and last of the genes to consider for this strand. b. Read in the strand strand to be evaluated. c. Initialize two variables, h to store the health of the strand, and ls to store the length of the strand. d. Loop through all possible substrings of the strand. For each substring: i. Check if the substring exists in the groupOfSets set. If it doesn't, continue with the next substring. ii. If the substring exists in the geneHealthMapping dictionary, retrieve its indices and cumulative health values. iii. Use the binary search functions bLeft and bRight to find the indices corresponding to 1st. and last ind.list. iv. Add the health values of the genes in the given range to the h variable. e. Update the minimum and maximum health values found so far with the h variable.

7. Print the minimum and maximum health values found.


Reasoning:

This code is a solution to a problem that involves calculating the health of a DNA strand, based on its substrings, called genes. Given a list of genes and their health values, the health of a DNA strand is calculated by summing the health values of its substrings present in the genes list.

The code first takes in the number of genes, followed by the genes and their corresponding health values. Then it takes in the number of DNA strands, followed by the first and last indices of each strand, and the strand itself.

The code uses the defaultdict collection from the collections library to store a mapping between the genes and their health values, as well as a set of all unique substrings present in the genes, limited to a maximum length of 500.

For each DNA strand, the health of the strand is calculated by iterating through each substring of the strand, and if the substring is present in the geneHealthMapping, the health value for that substring is obtained and added to the total health of the strand. The minimum and maximum health values for all strands are then stored in variables hMin and hMax, which are printed as the final result.

This code uses the bisect library to efficiently find the indices of the first and last occurrences of the substrings in the geneHealthMapping, which optimizes the performance of the code.

TEST CASES

Test case 1:

Inputs:

noGenes: 6 genes: a b c aa d b Health: 1 2 3 4 5 6 noStrand: 3 Strand1: 1 5 caaab Strand2: 0 4 xyz Strand3: 2 4 bcdybc

Sample Output 0 19

Reasoning:

First the genes list is ['a','b','c','aa','d','b']
the healths list is [1,2,3,4,5,6]
the dictionary geneHealthMapping in populated with genes info as follows: {'a':[[0],[0], 'b':[[1,5][0],'c':[[2][0],'aa':[3][0],'d:[[4][0]]}
now the dictionary is populated with healths info as follows: {'a':[[0],[0,1], 'b':[[1,5][0,2,8],'c':[[2][0,3],'aa':[3][0,4],'d:[[4][0,5]]}
for the first strand 1 5 caaab, the min value is zero and the max value is 19(3 from c + 4 from aa + 4 from aa + 8 from b)
for the second strand 0 4 xyz, there is no match son min value is zero and max value is zero, but continues with last max value = 19
for the third strand 2 4 bcdybc, the min is zero and the max is 11 (b does not match, c is 3, d is 5, y does not match, b does not match and c is 3, total 11). Still max value keeps with first strand = 19
min value is 0 and max value is 19.

If you want to see the code click [here](code)
