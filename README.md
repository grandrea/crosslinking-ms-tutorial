## Crosslinking MS tutorial- crosslink visualization
#### EMBO course Grenoble June 2024

Dataset: Cullin4-Ubiquitin ligase + SAMHD1 + Vpr [citation]()

### First part - analyze crosslinking MS dataset on xiview.org

Open the dataset in the xiview.org interactive viewer [here](). You can expand each protein with the right click of the mouse to see where the crosslinks are localised on the sequence.

At the bottom of the viewer, you have several toggles:

- self/heteromeric: toggle crosslinks within protein sequences or between protein sequences on or off. As the experimnt is peptide based, a "self" link can also be between multiple copies of the same protein
- overlap/non-overlap: toggle crosslinks that are self but between multiple copies of the same protein (not relevant here)
- filter boxes: filter by protein name, run name, and so on
- Score: crosslink score. This is an arbitrary number specific to each search engine. The higher, the better- a greater number indicates a better quality of peptide-spectrum match. This slider should be used for visualization purposes only. A key property of FDR control is that the results after FDR control are not further subsettable, or else the FDR becomes unknowable. For a more stringent dataset, repeat the FDR procedure with a tighter threshold.
- Distance: Filter by distance once a PDB is uploaded to the session.
- Residue pairs per PPI: filter the network so that only protein pairs with more than X crosslinks are displayed.
- 