# PeptideMassCounter

# Description
PeptideMassCounter is a Python script designed to estimate the number of possible linear peptides (composed of known amino acid masses) that result in a given total mass m. This is particularly useful in mass spectrometry-based proteomics, where it's important to evaluate the combinatorial space of peptide candidates that correspond to a specific observed mass.

The script uses dynamic programming to efficiently compute the number of combinations of amino acid masses that sum to a target mass. It also estimates the growth rate constant (C) for peptide enumeration by comparing the number of peptides for mass m+1 and m.

# Functionality
count_peptides_with_mass(m)
Purpose: Returns the number of distinct peptide sequences (regardless of order) whose total mass is exactly m, considering standard amino acid mass values.

# Approach:

* Uses a bottom-up dynamic programming strategy with memoization (dp list).
* Iterates over all possible masses from 1 to m, summing combinations from the allowed amino acid masses.
* Can be used to compute the growth constant C, which approximates how fast the number of peptide combinations grows with increasing mass.

# Parameters
m (int): The target peptide mass.

# Returns
int: The total number of distinct peptides with mass exactly m.

# Example Usage
```

AMINO_ACID_MASS = {
    57, 71, 87, 97, 99, 101, 103,
    113, 114, 115, 128, 129, 131,
    137, 147, 156, 163, 186
}

def count_peptides_with_mass(m):
    dp = [0] * (m + 1)
    dp[0] = 1

    for i in range(1, m + 1):
        for x in AMINO_ACID_MASS:
            if i - x >= 0:
                dp[i] += dp[i - x]
    return dp[m]

# Estimate growth constant C
m = 400
C_estimate = count_peptides_with_mass(m + 1) / count_peptides_with_mass(m)
print(C_estimate)
```
 
# Output Example:
1.2448979591836735


# Applications
This tool is useful in:

* Mass Spectrometry Analysis: Estimating the number of peptide candidates for a given mass peak.
* Theoretical Proteomics: Studying peptide space complexity.
* Bioinformatics Education: Teaching dynamic programming and combinatorial enumeration.
* Algorithm Design: Supporting scoring systems and search space pruning in peptide-spectrum matching algorithms.

# Requirements
* Python 3.x
* No external libraries required.

# License
This project is licensed under the MIT License – see the LICENSE file for details.






