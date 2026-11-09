# GC skew analysis of the E. coli genome
Finding the origin of DNA replication in the *E. coli* K-12 MG1655 genome
using cumulative GC skew, with Python and Biopython.

## Background
In bacteria, replication starts at one origin and proceeds in both
directions. The two DNA strands are copied differently, which leaves a
small bias in the ratio of G to C bases. Plotting the cumulative GC skew
along the genome gives a curve that changes direction at the origin
(minimum) and the terminus (maximum).

## What this project does
1. Downloads the genome (NCBI accession NC_000913.3) with Biopython
2. Calculates GC content and GC skew in 10,000 bp windows
3. Plots the cumulative GC skew
4. Estimates the positions of the origin and terminus

## Result
![Cumulative GC skew](results/gc_skew.png)

The minimum of the curve is at about 3.92 Mb and the maximum at about 1.54 Mb. The minimum matches the annotated origin of replication (oriC) of E. coli K-12 MG1655 at roughly 3.92 Mb. The maximum falls near the terminus region, which the genome map places at around 1.6-1.7 Mb. The terminus estimate is less precise than the origin, and both depend on the 10 kb window size. GC skew here is calculated as (G-C)/(G+C).

## How to run it
```
git clone https://github.com/tojotkaa/ecoli-gc-skew.git
cd ecoli-gc-skew
python -m venv venv
venv\Scripts\activate
pip install biopython pandas matplotlib numpy jupyter
mkdir data
jupyter notebook
```
Open `notebooks/gc_skew.ipynb` and run all cells. The genome is downloaded
automatically.
Before running, replace the email address in the `Entrez.email` line of the notebook with your own (NCBI requires one).

## Tools
Python, Biopython, NumPy, Matplotlib, Jupyter

## Next steps
- Compare different window sizes (1 kb to 50 kb) and see how the curve and the estimates change
- Repeat the analysis on another bacterium, such as Bacillus subtilis, and compare the skew pattern
