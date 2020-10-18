# LSO
local sequence optimality


READ THIS FILE BEFORE RUNNING

Goal: Compute a rough frustration analysis for PDBs. Frustrated positions
are defined as those for which Rosetta mutation scanning (filterscan)
identified at least 5 identities with lower energies (<=0) than the native

The frustration analysis has two steps:
1. relax
2. frustration

1. put your PDB files in in/<<"my dir">>/<<PDB>>.pdb.
2. Run the relax.snk relaxation procedure to relax the PDBs. This
   will result in a new directory, relax/<my dir>/<PDB>.pdb
3. Run the frustrate.snk frustration analysis. This will result in several
   new directories:
   a. temp_resfiles: temporary repository for resfiles. Most of it is deleted
      at the end of the run, but the score logs are saved
   b. resfiles: The final resfiles for each PDB
   c. pymol_scripts: a set of pymol scripts to load the relaxed PDB files
      and label the frustrated positions.
4. Using samba, connect to your WEXAC directory and from this, call
   pymol @pymol_scripts/master.pml
   this will load all of the relaxed files and label the frustrated positions

You can control the frustrate analysis through frustrate_config.yaml:
1. energy_cutoff_for_pymol: What is the energy cutoff by which to decide look
   for frustrated positions
2. identities_at_frustrated_pos: how many identities at a position count for
   being frustrated.
