# Drug Similarity Finder

## What this project does
Calculates Tanimoto similarity between 24 common drugs 
using RDKit Morgan Fingerprints and visualizes results as a heatmap.

Drug structures (SMILES) were collected from ChEMBL (https://www.ebi.ac.uk/chembl/).

Dataset

The dataset contains 24 common drugs. SMILES strings were collected from the ChEMBL database (https://www.ebi.ac.uk/chembl/). Each SMILES was checked against the ChEMBL molecular weight for the same compound. Several entries had incorrect or incomplete structures and were corrected. Entries that could not be represented as a single small molecule (for example, insulin, a protein) were removed. A duplicate entry (acetaminophen and paracetamol, the same compound) was also removed. The final dataset is saved as drugs.csv.

Method
Molecule parsing: Each SMILES string is converted into an RDKit molecule object.
Descriptors: Molecular weight, Crippen logP, hydrogen bond donors (HBD), and hydrogen bond acceptors (HBA) are calculated with RDKit.
Fingerprints: Each molecule is converted into a 2048-bit Morgan fingerprint (radius 2, ECFP4-like), which encodes the local chemical environment of each atom.
Similarity: Pairwise Tanimoto similarity is calculated as the number of shared bits divided by the total number of distinct bits. Values range from 0 to 1.
Visualization: All pairwise similarities are shown as a Seaborn heatmap. The diagonal is always 1.0, since each molecule is identical to itself.

Limitations: Crippen logP can differ from ChEMBL’s AlogP. Morgan fingerprints capture local structure only and do not represent 3D shape or biological activity. Small molecules tend to get lower Tanimoto scores because they have fewer bits to share.

Results

The five drugs most similar to Aspirin (Tanimoto similarity) are:

Drug	Similarity	Reason
Warfarin	0.245	Shares an acetyl-like group and a benzene ring. Its larger coumarin structure reduces the overall score.
Acetaminophen	0.222	Shares the CC(=O) group and a benzene ring with a hydroxyl. The linker differs (NH instead of O).
Ibuprofen	0.195	Shares a benzene ring and a carboxylic acid group.
Penicillin G	0.175	Shares carboxylic acid and amide carbonyl environments.
Ciprofloxacin	0.167	Shares an aromatic carboxylic acid environment.

All scores are below 0.4, which means none of these drugs is a close structural analogue of Aspirin. The heatmap of all pairwise similarities is shown below: [heatmap image]


## Tools used
- Python
- RDKit
- Pandas
- Matplotlib
- Seaborn

## How to run
pip install rdkit
Open in Google Colab and run all cells.
