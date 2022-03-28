# Training data and DFT confirmation

This folder contains the training data used to develop models for organic radical redox potentials and stability.

## Starting radical database
`radical_db_*` contains the main radical database, using radicals derived from Pubchem molecules.

`radical_db_redox_potentials.csv.gz` begins with the following rows:

|                       smiles | oxidation | reduction |
|-----------------------------:|----------:|----------:|
| C#C/C(=C/C=O)[C](C)C         | NaN       | -0.059920 |
| C#C/C(=C\[CH2])CC            | NaN       | -0.943918 |
| C#C/C(C)=C(/[CH2])C          | 0.781466  | -0.915292 |
| C#C/C(C)=C(\C)C[CH]C         | 0.313277  | -1.811318 |
| C#C/C(C)=C(\C)[C@@H]([CH2])C | NaN       | -1.526529 |

Here, oxidation and reduction values are the reduction potential of the oxidation or reduction half-reaction (in V relative to SHE). Where oxidation or reduction columns are `NaN`, the corresponding optimization failed or was otherwised discarded as described in the Methods.

`radical_db_spins_and_bv.csv.gz` begins with the following rows:

|        smiles | atom_type | atom_index |      spin | buried_vol | fractional_spin |
|--------------:|----------:|-----------:|----------:|-----------:|----------------:|
| [CH2]C1=COCC1 | C         | 0          | 0.586646  | 30.291542  | 0.405000        |
| [CH2]C1=COCC1 | C         | 1          | -0.180922 | 41.879991  | 0.124902        |
| [CH2]C1=COCC1 | C         | 2          | 0.570409  | 38.252099  | 0.393790        |
| [CH2]C1=COCC1 | O         | 3          | 0.096694  | 33.700549  | 0.066754        |
| [CH2]C1=COCC1 | C         | 4          | -0.002564 | 34.074425  | 0.001770        |

This file describes the DFT-calculated unpaired electron spin (spin), buried volume (in percent), and the spin term normalized to an absolute, fractional quantity (sum = 1.0 for each molecule).


## High scoring radicals

`radical_db_redox_potentials.csv.gz` and `radical_db_spins_and_bv.csv.gz` contain approximately 4,000 high-scoring, DFT-optimized molecules from previous iterations of the RL algorithm, added to the training dataset above to give better predictive performance in the region of interest. The format of the files is identical to the training database files above.


## RL candidates

`rl_candidates_ml_and_dft.csv` contains ML-predicted and DFT-calculated values for the 1078 top-performing RL candidates. This file includes columns (`*_ml` and `*_dft`) for
* `max_spin`: the maximum fractional spin over all atoms in the molecule
* `spin_buried_vol`: the buried volume at the location of maximum spin
* `ionization_energy`: the reduction potential of the reduction half-reaction (in V)
* `electron_affinity`: the reduction potential of the oxidation half-reaction (in V)
* `stability`: the calculated stability score from max_spin and spin_buried_vol

`rl_candidates_spin_bv.csv.gz` contains the electron spins and buried volumes (calculated via DFT) used to derive the stability estimates in a format similar to the radical database above.
