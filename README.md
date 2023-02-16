# Hydrogen Mass Repartitioning (HMS)
Required Software
1. AmberTools22 https://ambermd.org/GetAmber.php
2. GROMACS https://manual.gromacs.org/current/download.html

This tutorial using AmberTools Version 22 and GROMACS version 2022.2
1. Seperate receptor:*grep ATOM 2nnq.pdb > rec.pdb*
2. Seperate Ligand: *grep T4B 2nnq.pdb > lig.pdb*
3. Open Protein in the chimera, Tools > Structure Editing > Dock Prep, uncheck write Mol2 file > Ok > Ok > On Assign Charges for dock prep click AM1-BCC and standard residues > File > Save PDB > overwrite the rec.pdb file
4. Open ligand in chimera, Tools > Structure Editing > Dock Prep, uncheck write Mol2 file > Ok > Ok > On Assign Charges for dock prep click AM1-BCC and nonstandard residues > File > Save PDB > overwrite file lig.pdb
5. Observe the charges that appear in Specify Net Charges, the amount of net charges will later be used when using antechamber -nc like the antechamber command below using -nc -1 from Chimera
6. Ligand paramterization:
*antechamber -i lig.pdb -fi pdb -o lig.am1bcc.mol2 -fo mol2 -at gaff2 -c bcc -rn LIG -nc -1*
7. Next run the following command: *parmchk2 -i lig.am1bcc.mol2 -f mol2 -o lig.am1bcc.frcmod*
8. The process of solvation and incorporation of proteins and ligands, Run the following command: *tleap -f leap.in*
9. Run google colab by clicking the following link: https://github.com/purnawanpp/HMS/blob/main/HMP.ipynb
Upload file namely solvated.prmtop and solvated.inpcrd on Google Colab.
10. Run google colab and dont forget to download file namely gromacs.gro dan gromacs.top. Move the two downloaded files to your work folder
11. Running this command to simulation your protein and ligand using GROMACS:
12. *gmx grompp -f min.mdp -c gromacs.gro -p gromacs.top -o em.tpr -maxwarn 1*
13. *gmx mdrun -v -deffnm em*
14. *gmx grompp -f nvt.mdp -c em.gro -r em.gro -p gromacs.top -o nvt.tpr -maxwarn 2*
15. *gmx mdrun -v -deffnm nvt &*
16. *gmx grompp -f npt.mdp -c nvt.gro -t nvt.cpt -r nvt.gro -p gromacs.top -o npt.tpr -maxwarn 2*
17. *gmx mdrun -v -s npt.tpr -deffnm npt &*
18. *export GMX_MAXCONSTRWARN=-1*
19. *gmx grompp -f md.mdp -c npt.gro -t npt.cpt -p gromacs.top -o md.tpr -maxwarn 1*
20. *gmx mdrun -v -s md.tpr -deffnm md &*

# Reference
1. https://pubs.acs.org/doi/10.1021/ct5010406
2. https://ambermd.org/doc12/Amber22.pdf
3. https://parmed.github.io/ParmEd/html/index.html
