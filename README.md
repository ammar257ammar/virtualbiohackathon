## Motivation

This repo contains a drug repurposing docking experiment against the COVID-19 main protease (PDB ID: [6LU7](https://www.rcsb.org/structure/6lu7)) in an attempt to highlight the compounds that are already approved by FDA and available in the market that maybe can be used to fight COVID-19 during this pandemic. Hopefully, this work can contribute to the global attempts to find a cure for the virus. 



## Docking Protocol:

1. Download PDB file of COVID-19 main protease: https://www.rcsb.org/structure/6lu7

2. Clean the PDB (using **bash** on Ubuntu 18.04): remove the ligand , hetero atoms and water molecules.

3. Download the structures of all FDA approved from **DrugBank**: https://www.drugbank.ca/releases/5-1-5/downloads/approved-structures 

4. Split the SDF file of the structures to individual molecules files and convert them from SDF to MOL2 files (this format is needed for later processing) using OpenBabel: http://openbabel.org/wiki/Main_Page

   Total number of drugs 2454 (2454 docking experiments)

5. Energy minimization for the ligands using the **MMFF94** force field with **OpenBabel**.

6. Define the grid box for docking which is the space that covers the binding pocket where the  ligands will be docked, using **AutoDockTools** which is provided as part of **MGLTools 1.5.6** https://ccsb.scripps.edu/autodock/adt/

7. Preprocess the protein PDB and ligands files using the scripts "prepare_receptor4.py" and "prepare_ligand4.py" from AutoDockTools respectively. The preprocessing adds hydrogens and defines the rotatable bonds for ligands. The output of those commands is PDBQT files which are ready for docking.

8. Using AutoDock Vina to perform the docking using 3 inputs: the receptor, the ligand and a config file of the defined grid box.

9. The docking tools are wrapped inside a docker image and the docking experiment was submitted as a Job to the Data Science Research Infrastructure (DSRI) at [Maastricht University](https://www.maastrichtuniversity.nl/). 

10. Top 50 drugs (DrugBank ID and drug name) with their corresponding binding affinity change (kcal/mol) are in the following table and they are also provided in this [CSV](https://github.com/ammar257ammar/virtualbiohackathon/blob/master/Covid19Top50.csv) file.



