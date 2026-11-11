# project1-sequence-analysis-295950
"""NGSmutational Analysis"""

# purpose
# This program identifies base mismatches in NGS reads relative to a reference sequence and was applied to analyse the genomic impact of a genotoxic agent on S. pombe in six samples (three treated, three control).

# How to Run the Program
# 1.	Open this notebook in Google Colab.
# 2.	Execute the Setup Code cells at the top to automatically download and initialise the reference sequence (reference.txt) and sequencing reads (reads.csv).
# 3.	Execute the function definitions sequentially (Steps 1 through 5).
# 4.	Run the final cell in the Final analysis section to execute the full pipeline and output the summaries and statistical comparisons.

# Inputs and Outputs
# Inputs:
# A 200-nt reference sequence file (reference.txt).
#	A CSV file (reads.csv) containing 6,000 aligned, 200-nt single-end reads across 6 samples.
# Outputs:
# Group summary tables showing valid/invalid read counts, sample mismatch percentages, total mismatch events, and top mutation positions.
# Substitution frequency tables detailing mutation types and rates per 100 valid reads.
# Welch's two-sided t-test results comparing mismatch levels at the most mutated hotspots.

# Code Design Decisions
# Multi-Stage Validation: Inside validate_read, the sequence is normalised to uppercase. It handles mixed-case inputs gracefully and isolates multiple independent errors (wrong_length and invalid_characters) in a detailed list to prevent runtime crashes during bulk parsing.
# Data Structure Optimisation: Dict-based indexing is used in summarise_samples to group data dynamically on the fly. This ensures that the script handles an arbitrary number of samples, groups, or reads without code modification.
# Sorting Stability & Tie-Breaking: In Step 4 and Step 5, candidate hotspot positions are sorted with stable custom keys (lambda x: (-x[1], x[0])), guaranteeing that in the case of frequency ties, the position appearing earlier in the sequence is systematically selected.

# Tests
# Mock Unit Testing: Verified using mock sequence datasets containing known mutations, missing values, and high variance. Unit tests confirmed accurate mutation counts, percentage calculations, statistical handling of edge cases, and expected outputs.
# mixed-Case Normalisation Test: Target: validate_read; Details: Verified that mixed-case inputs (e.g., "gtga" vs. reference "ATGC") were correctly converted to uppercase and processed as valid sequences.
