[![DOI](https://zenodo.org/badge/420130436.svg)](https://zenodo.org/badge/latestdoi/420130436)

# Data and trained models for predicting the stability and redox potentials of organic radicals

Part of an upcoming work on optimizing organic radical scaffolds for aqueous redox flow batteries.

* `data/radical_db_redox_potentials.csv.gz` contains the redox potentials (in V relative to SHE) calculated with Guassian 16c at the  M06-2x/def2-tzvp level of theory in an implicit water solvent
* `data/radical_db_spins_and_bv.csv.gz` contains the parsed electron spins, normalized 'fractional spins' (ensuring all spin values are positive and sum to 1.0, assuming hydrogen spins are zero), and calculated buried volumes at a 3.5 Angstrom radius for all heavy atoms in the dataset. Atom index corresponds to the atom index assigned by RDKit after parsing the SMILES string.
* `models/redox_model/` contains the trained weights for a GNN that predicts the oxidation and reduction potentials of a given radical input
* `models/stability_model/` predicts the fractional spin and buried volumes on each atom in the given input radical, and can be used to derive the combined stability score.


