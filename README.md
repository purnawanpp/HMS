# Hydrogen Mass Repartitioning (HMS)
This tutorial using AmberTools Version 22 and Gromacs version 2022.2
1. Seperate receptor:*grep ATOM 2nnq.pdb > rec.pdb*
2. Seperate Ligand: *grep T4B 2nnq.pdb > lig.pdb*
3. Open Protein in the chimera, Tools > Structure Editing > Dock Prep, uncheck write Mol2 file > Ok > Ok > On Assign Charges for dock prep click AM1-BCC and standard residues > File > Save PDB > overwrite the rec.pdb file
4. Open ligand in chimera, Tools > Structure Editing > Dock Prep, uncheck write Mol2 file > Ok > Ok > On Assign Charges for dock prep click AM1-BCC and nonstandard residues > File > Save PDB > overwrite file lig.pdb
5. Observe the charges that appear in Specify Net Charges, the amount of net charges will later be used when using antechamber -nc like the antechamber command below using -nc -1 from Chimera
6. Ligand paramterization:
*antechamber -i lig.pdb -fi pdb -o lig.am1bcc.mol2 -fo mol2 -at gaff2 -c bcc -rn LIG -nc -1*
7. Next run the following command: *parmchk2 -i lig.am1bcc.mol2 -f mol2 -o lig.am1bcc.frcmod*
8. The process of solvation and incorporation of proteins and ligands, Run the following command: *tleap -f leap.in*
9. Run google colab by clicking the following link: https://colab.research.google.com/github/purnawanpp/Rekap-script/blob/main/HMP.ipynb
Upload the solvated.prmtop solvated.inpcrd file on Google Colab like this
