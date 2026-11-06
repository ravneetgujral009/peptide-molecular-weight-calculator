# Peptide Molecular Weight Calculator: Check the COA Before You Buy AOD 9604 Peptide Online

A free, open-source tool that calculates a peptide's molecular formula, average molecular weight and monoisotopic mass from its amino acid sequence, and then checks it against the molecular weight printed on a supplier's Certificate of Analysis (COA).

It works as a browser calculator (no installation needed) and as a Python script with no dependencies.

Live calculator: open index.html in any browser, or use the GitHub Pages link in the About section of this repository.

Why this tool exists

When researchers order a peptide, the COA is usually the only evidence of what is actually in the vial. Most people look straight at the HPLC purity figure and stop there.

That is a problem. HPLC tells you how clean a sample is. It does not tell you what the molecule is. A vial can be 99% pure and still contain the wrong peptide, the wrong modification, or a fragment in the wrong form.

The identity check on a COA is the mass spectrometry (MS) result, the observed molecular weight. But that number is only useful if you know what it should be. This calculator gives you the expected value in seconds, so you can compare the two before you rely on a batch, or before you place an order.

Worked example: AOD-9604

AOD-9604 is a 16-residue synthetic fragment from the C-terminal end of human growth hormone, with one disulfide bridge between its two cysteines. It is a good example because the bridge changes the expected mass.

Sequence: YLRIVQCRSVEGSCGF

Three-letter: Tyr-Leu-Arg-Ile-Val-Gln-Cys-Arg-Ser-Val-Glu-Gly-Ser-Cys-Gly-Phe

With disulfide bridge (cyclic):

• Molecular formula: C78H123N23O23S2

• Average MW: 1815.08 Da

• Monoisotopic mass: 1813.8604 Da

Without bridge (reduced, linear):

• Molecular formula: C78H125N23O23S2

• Average MW: 1817.10 Da

• Monoisotopic mass: 1815.8760 Da

The two forms differ by about 2 Da, the mass of the two hydrogen atoms lost when the S–S bond forms. That is small, but a properly reported mass spec result can resolve it. If a COA labelled "AOD-9604" reports a value that matches neither form, that is worth questioning.

Running the check with the command:

python peptide_mw.py YLRIVQCRSVEGSCGF --disulfide 1 --observed 1815.1

gives this result:

• Sequence: YLRIVQCRSVEGSCGF

• Length: 16 residues

• Disulfide bridges: 1

• Molecular formula: C78H123N23O23S2

• Average MW: 1815.08 Da

• Monoisotopic mass: 1813.8604 Da

• COA observed MW: 1815.10 Da

• Difference: +0.02 Da

• Result: MATCH (within ±1.0 Da)

How to use it

Option 1: In your browser

1. Open the live calculator (GitHub Pages link in the About section), or download index.html and open it.
2. Enter the one-letter sequence.
3. Set the number of disulfide bridges and tick any terminal modifications.
4. Optionally enter the molecular weight from the COA and a tolerance.
5. Click Calculate. You'll see a green Match or a red Mismatch.

The "Example: AOD-9604" and "Example: BPC-157" buttons fill in known sequences so you can see how it works.

Option 2: Python (command line)

Requires Python 3.8 or later. No packages to install.

Basic calculation:

python peptide_mw.py GEPPPGKPADDAGLV

With one disulfide bridge:

python peptide_mw.py YLRIVQCRSVEGSCGF --disulfide 1

Compare with a COA value (exit code 0 = match, 1 = mismatch):

python peptide_mw.py YLRIVQCRSVEGSCGF --disulfide 1 --observed 1815.1 --tolerance 1.0

Terminal modifications:

python peptide_mw.py YOURSEQUENCE --acetyl --amide

Options:

• sequence: one-letter amino acid sequence (spaces and dashes are ignored)

• disulfide N: number of disulfide bridges (removes 2 H per bridge)

• acetyl: N-terminal acetylation (adds C2H2O)

• amide: C-terminal amidation (replaces –OH with –NH2)

• observed X: molecular weight reported on the COA, in Da

• tolerance X: allowed difference in Da (default 1.0)

How the calculation works

1. Each amino acid is added as a residue (the free amino acid minus one water molecule), using its exact elemental formula.
2. One water molecule is added back for the free N- and C-termini.
3. Each disulfide bridge removes two hydrogen atoms.
4. Optional terminal modifications adjust the formula.
5. The formula is converted to mass using IUPAC standard atomic weights (average MW) and the most abundant isotope of each element (monoisotopic mass).

Because the tool builds the full molecular formula first, you can compare the formula as well as the mass with the COA.

Which value should I compare? Most COAs report average molecular weight. Some high-resolution MS reports give the monoisotopic mass or a charged ion (for example [M+2H]²⁺). Check which one your COA shows before comparing.

Validation: the outputs match published reference values, for example C78H123N23O23S2 at 1815.08 Da for AOD-9604 and 1419.54 Da for BPC-157 (GEPPPGKPADDAGLV).

A five-point COA check

Before relying on any peptide batch, or before you order from a new supplier, check that the COA shows:

• Compound name and sequence that match what you ordered

• Lot number that matches the label on the vial

• HPLC purity stated as a figure (typically ≥98–99% for research grade)

• Mass spec result within tolerance of the value this calculator gives

• Testing lab named, ideally independent and ISO 17025 accredited

If the mass doesn't match, check your inputs first (sequence, bridges, modifications). If it still doesn't match, ask the supplier for an explanation and the raw MS data.

Limitations

• Supports the 20 standard amino acids only. Non-standard residues, D-amino acids (same mass as L-forms), PEGylation, lipidation and salt forms (e.g. acetate or TFA counter-ions) are not modelled.

• Calculates the neutral molecule. It does not calculate charged ion m/z values.

• It is a check on identity by mass, not a replacement for proper analytical testing.

Files

• index.html: browser calculator, works offline and on GitHub Pages

• peptide_mw.py: command-line calculator, Python 3.8+, no dependencies

• LICENSE: MIT License

Contributing

Suggestions and corrections are welcome. Open an issue or a pull request, especially if you'd like support for additional modifications.

Research use only

This tool and the compounds it refers to are for laboratory and analytical research use only. Nothing in this repository is medical advice, and no compound mentioned here is intended for human consumption.

About

Maintained by RetraLabs, a Bengaluru-based supplier of research peptides. Their AOD-9604 is supplied as a sterile, lyophilised, nitrogen-sealed 5 mg vial, with a Certificate of Analysis included with every order and testing by an ISO 17025 accredited third-party laboratory, so you can run exactly this kind of check on the batch you receive.

If you're looking to buy AOD 9604 peptide online with batch documentation you can verify using this calculator, view the product details here: [AOD-9604 Peptide 5mg](https://retralabs.in/product/aod-9604)
