# Homework: DNA Analysis

## Overview

In this assignment, you will write a program that analyzes a sequence of DNA nucleotides.

<img width="3000" height="2100" alt="image" src="https://github.com/user-attachments/assets/cbe1b2b9-cb48-42ed-8fce-25f461d163a9" />


DNA sequences are made from four nucleotides:

* **A** — Adenine
* **C** — Cytosine
* **G** — Guanine
* **T** — Thymine

Your program will take a nucleotide sequence and produce information about it. Specifically, you will:

* Count how many times each nucleotide occurs.
* Calculate the percentage of the sequence's mass contributed by each nucleotide.
* Break the sequence into groups of three nucleotides called **codons**.
* Predict whether the sequence encodes a protein.

This assignment is intended to give you additional practice with **arrays**, **methods**, **loops**, and **String processing**, while introducing a basic bioinformatics problem.

---

## Protein Prediction

For this assignment, a DNA sequence will be considered a protein if **all** of the following conditions are true:

1. It begins with the start codon `ATG`.
2. It ends with one of the valid stop codons:

   * `TAA`
   * `TAG`
   * `TGA`
3. It contains at least **5 codons**, including the start and stop codons.
4. At least **30% of its total mass** comes from Cytosine (`C`) and Guanine (`G`) combined.

> [!NOTE]
> These rules are approximations created for this assignment. They are not the exact rules used in computational biology.

---

## Program Requirements

Your program must:

1. Accept a DNA nucleotide sequence.
2. Treat uppercase and lowercase nucleotide letters equivalently.
3. Count the occurrences of `A`, `C`, `G`, and `T`.
4. Store the nucleotide counts in an `int[]` of size 4.
5. Calculate the mass percentage of each nucleotide.
6. Store the mass percentages in a `double[]`.
7. Break the sequence into codons.
8. Store the codons in an array.
9. Determine whether the sequence meets the protein requirements.
10. Produce all final results from a single output method.

> [!IMPORTANT]
> You may assume that the number of nucleotides in a sequence is a multiple of 3.

---

## Nucleotide Mass

Use the following nucleotide masses:

```java
double[] masses = {135.128, 111.103, 151.128, 125.107};
```

The values correspond to:

```text
Index:       0        1        2        3
Nucleotide:  A        C        G        T
Mass:      135.128  111.103  151.128  125.107
```

For example, the sequence:

```text
ATGGAC
```

has a total mass of:

```text
808.722
```

Its approximate mass percentages are:

```text
A: 33.4%
C: 13.7%
G: 37.4%
T: 15.5%
```

Round mass percentages to **one digit after the decimal**.

One option is:

```java
double rounded = Math.round(num * 10.0) / 10.0;
```

---

## Breaking the Sequence into Codons

A **codon** is a group of three nucleotides.

For example:

```text
ATGCCACTATGGTAG
```

becomes:

```text
ATG CCA CTA TGG TAG
```

You may find methods such as these useful:

```java
substring()
charAt()
indexOf()
replace()
toUpperCase()
toLowerCase()
```

---

## Required Concepts

Your solution must use:

* An array for nucleotide counts
* An array for mass percentages
* An array for codons
* At least **four non-trivial methods** in addition to `main`
* Methods that accept arrays as parameters or return arrays when appropriate
* Separate methods for filling significant arrays
* A single method responsible for producing all final output

Your methods should be organized so that looking at `main` gives a clear overview of the major tasks performed by the program.

No individual method should become unnecessarily long.

All final output should be produced by one output method that receives the computed data as parameters. `main` should not directly produce the analysis output.

The only exception is output related to asking whether the user wants to analyze another sequence.

---

## Suggested Program Structure

One possible decomposition is:

```text
intro / input
    ↓
count nucleotides
    ↓
calculate mass percentages
    ↓
build codon array
    ↓
determine whether sequence is a protein
    ↓
print results
```

For example, you might create methods similar to:

```java
String intro(Scanner console)

int[] counts(String sequence)

double[] massPercent(int[] counts)

String[] codons(String sequence)

boolean isProtein(...)

void printResults(...)
```

You are not required to use these exact method names or parameters. Choose a design that keeps your program organized and avoids redundancy.

---

## Output Format

Your program should report:

```text
This program reports information about DNA
nucleotide sequences that may encode proteins.

Data of Sequence: SEQUENCE
Nuc. Counts: [A, C, G, T]
Codons List: [CODON1, CODON2, ...]
Total Mass%: [A%, C%, G%, T%]
Is Protein?: YES
```

Use `Arrays.toString()` when appropriate to display arrays.

---

## Sample Run

For the sequence:

```text
ATGCCACTATGGTAG
```

your output should resemble:

```text
This program reports information about DNA
nucleotide sequences that may encode proteins.

Data of Sequence: ATGCCACTATGGTAG
Nuc. Counts: [4, 3, 4, 4]
Codons List: [ATG, CCA, CTA, TGG, TAG]
Total Mass%: [27.3, 16.8, 30.6, 25.3]
Is Protein?: YES
```

Another example:

```text
Data of Sequence: ATgCCAACATGgATGCCcGATAtGGATTgA
Nuc. Counts: [9, 6, 8, 7]
Codons List: [ATG, CCA, ACA, TGG, ATG, CCC, GAT, ATG, GAT, TGA]
Total Mass%: [30.7, 16.8, 30.5, 22.1]
Is Protein?: YES
```

---

## Implementation Suggestions

A useful development order is:

1. Begin with a single DNA sequence.
2. Read and store the sequence.
3. Count `A`, `C`, `G`, and `T`.
4. Store those counts in an array.
5. Calculate the mass percentages.
6. Break the sequence into codons.
7. Determine whether the sequence qualifies as a protein.
8. Add the final output method.
9. Once one sequence works correctly, add support for processing additional sequences.

Build and test each part before moving on to the next.

---

## Extensions
Pick one of the following for 10 points extra credit.

### Option 1: Handle Junk Data

Make your program robust enough to process sequences containing dashes.

For example:

```text
ATG-----C-CC--GGG----TGA
```

Each dash:

* Has a mass of `100.0`
* Contributes to the total mass
* Does **not** count as a nucleotide
* Does **not** appear in the codon list

Example result:

```text
Region Name: Dash-non-protein-not-long-enough
Nucleotides: ATG-----C-CC--GGG----TGA
Nuc. Counts: [2, 3, 5, 2]
Total Mass%: [9.6, 11.9, 26.9, 8.9] of 2809.4
Codons List: [ATG, CCC, GGG, TGA]
Is Protein?: NO
```

### Option 2: Read DNA from Files

Extend your program so that DNA sequences can be read from a file rather than entered manually.

Test your program using the provided DNA data files.

---

### Option 3: Analyze an unknown number of DNA sequences

After displaying the result, ask:

```text
Compute another sequence? Yes
```

If the user answers yes, process another sequence.

Continue until the user chooses to stop.

---

## Submission

Submit your feedback PR to the Canvas submission page. 
