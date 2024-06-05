## Crosslinking MS tutorial- crosslink visualization
#### EMBO course Grenoble June 2024

Dataset: Cullin4-Ubiquitin ligase + SAMHD1 + Vpr [citation]() . The crosslinker is sulfo-SDA and it is searched from K,S,T,Y,nterm to any amino acid.

### First part - analyze crosslinking MS dataset on xiview.org

Open the dataset in the xiview.org interactive viewer [here](). You can expand each protein with the right click of the mouse to see where the crosslinks are localised on the sequence.

At the bottom of the viewer, you have several toggles:

- self/heteromeric: toggle crosslinks within protein sequences or between protein sequences on or off. As the experimnt is peptide based, a "self" link can also be between multiple copies of the same protein
- overlap/non-overlap: toggle crosslinks that are self but between multiple copies of the same protein (not relevant here)
- filter boxes: filter by protein name, run name, and so on
- Score: crosslink score. This is an arbitrary number specific to each search engine. The higher, the better- a greater number indicates a better quality of peptide-spectrum match. This slider should be used for visualization purposes only. A key property of FDR control is that the results after FDR control are not further subsettable, or else the FDR becomes unknowable. For a more stringent dataset, repeat the FDR procedure with a tighter threshold.
- Distance: Filter by distance once a PDB is uploaded to the session.
- Residue pairs per PPI: filter the network so that only protein pairs with more than X crosslinks are displayed.

Top panel includes tabs for uploading various files, including PDB files, and for analysing crosslink data.

#### Gathering statistics
All run files for the experiments with low SDA concentrations are called "Ratio24". The ones with the high SDA concentrations are called "Ratio56". Using the filters, take a look at how many crosslinks and how many heteromeric crosslinks correspond to either condition.

#### Viewing spectra
Let's get an idea for what crosslinked peptide spectra look like. In the scan box, select scan XXX. From the dropdown menu at the top, select view-> spectrum.

Take a moment to familiarize yourself with the viewer. At the top of the spectral window you see the error in matching the precursor (whole peptide) and its mass and charge state. 

The vertical hockey pucks along the sequence are the fragment ions covering the sequence. You can hover over them with the mouse to reveal which part of the sequence they cover and to which peak they correspond. Each fragment ion may have more than one peak supporting it, as there may be versions that are unmodified and versions that have sustained the loss of water or ammonia groups.

Sometimes for this crosslinker, the exact crosslink site is not known as backbone fragmentation is incomplete. In this case, the program assigns the site to the last compatible amino acid in a stretch of equivalent linkage positions. 

You can check how the spectrum would look with a different assignment by moving the crosslink site with a mouse. For more radical reannotations, you can click on the wheel and change the sequence or enter custom annotation commands.

The group of Andrea Sinz [has observed]() that diazirine crosslinkers such as sulfo-sda may cleave in the gas phase. We can check if this has happened here by introducing a custom annotation for it. 

Inside the spectral viewer, click the wheel and then the "custom" tab, copy the following line, that accounts for a cleavable crosslinker, and click "apply".


Is this annotation better than the previous one? click "butterfly" at the top of the viewer to check.

Finally, let's look at crosslinks supported by scans that barely pass the FDR. Filter to a low spectral matching score (<10) and select a crosslink. Open the spectrum viewer. Check the difference with the high ranking spectra. 

Always check the quality of the spectra before staking a biological interpretation on sparse crosslinking data!

#### Interacting with the dataset
In the "Histogram" and "scatterplot sections of the view, several properties of the dataset may be investigated.

Using the box to select "frac6" and "frac9", check out if there is a difference in number of crosslinks, charge state and precursor mass of earlier chromatographic fractions and latter ones.

What consequences does this have for experimental design?

In the uplad tab, go to "sequence metadata" and upload the file XXX.csv. In the "annotation" tab at the top, toggle annotations on. You should now see domais highlighted on the sequence. 

In this case, we used a custom sequence annotation file, as our proteins are recombinant and we searched with an in-house sequence file containing the tags. For proteins with uniprot IDs in the sequence file headers, xiview will automatically download this information from uniprot.

#### Working with PDB files
Upload the file "state 3.pdb" from the course package. in view, select the 3d viewer. In the "annotation" tab at the top, toggle off the domains and select "PDB aligned region". What do you notice? Which protein is missing from the experimental structure?

Let's look at the 3d structure now. To check if the crosslinks are satisfied by this model, open "view", "legends and colors" and then color the crosslinks by distance. Let's set satisfied up to 25 angstrom, borderline 25-30 and violated over 30 angstrom. Go back to the 3d viewer. What do you see? You can also toggle between all crosslinks and heteromeric only.

For a more quantitative overview, check the histogram tab and plot by distance, or the scatterplot tab and plot crosslink score vs distance.

### Second part - in-depth 3d analysis

#### Binding patch
Select SAMHD1 crosslinks in the protein selection box, and toggle off self links.

Go back to the 3d viewer and toggle the display to "residues with half links" from the dropdown menu.