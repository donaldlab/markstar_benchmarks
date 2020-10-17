# MARK\* Benchmark tests

Benchmark tests for the MARK\* protein design algorithm.
This repo contains design files that each specify a single protein design for binding affinity problem instance, along with test result files that describe algorithm performance on design problems.

These design problems were procedurally generated using PyMOL and (currently) unreleased tools.

## Usage

Install OSPREY and the python TOML module.
OSPREY ConfSpace objects can be generated from design files using methods in `tools.py`, after which designs can be run normally.

##Repository structure

* `tools.py`

	A python module with methods for loading design files and computing energy matrices.
	Requires the latest version of [OSPREY](https://github.com/donaldlab/OSPREY3) and the [TOML python module](https://pypi.org/project/toml/).
* `bin/`

	Contains example scripts for running MARK\* on design problems.
* `designs/`
	* `disc_binding_ms/`

		Contains multi-sequence designs for binding affinity, intended for a discrete formulation.
	* `disc_binding_ss/`

		Contains single-sequence designs for binding affinity, intended for a discrete formulation.
* `tests/`
	* `1810_disc_binding_ss_mark/`

		Contains test results generated by running the MARK\* algorithm with BBK\* on discrete problems previously reported in [the MARK\* paper](https://doi.org/10.1089/cmb.2019.0315).
		These tests were run on single-sequence design problems.
		Runtimes reflect the time required to compute the K\* score for the specified sequence.
	* `1810_disc_binding_ss_mark/`

		Contains test results generated by running the iMinDEE/A\*/K\* algorithm with BBK\* on discrete problems previously reported in [the MARK\* paper](https://doi.org/10.1089/cmb.2019.0315).
		These tests were run on single-sequence design problems.
		Runtimes reflect the time required to compute the K\* score for the specified sequence.

* `resources/`
	
	Contains PDB files and Rotamer library files.

## Description of design file syntax

Design files are formatted as TOML files with the following fields:

* molecule

	A pointer to the design PDB file
* strand_definitions

	A dictionary defining the terminal residues (inclusive) of design "strands."
	A strand is a protein state (e.g. protein, ligand).
	Residues are formatted as `<chain><resnum>`, where `chain` is the PDB chain identifier and `resnum` is the residue number.

* strand_mutations

	A dictionary defining the flexiblity for each protein strand.
	Each strand dictionary defines an assignment of one or more amino-acid types to a set of strand residues.
	If a strand residue is assigned exactly one amino-acid type, that residue will be flexible (but not mutable).
	If a strand residue is assigned more than one amino-acid type, that residue will be mutable.
	If a strand residue does not appear in this dictionary, that residue will be held rigid.
