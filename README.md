## Crosslinking MS tutorial- crosslink visualization
#### EMBO course Grenoble June 2024

Dataset: Cullin4-Ubiquitin ligase + SAMHD1 + Vpr [citation](https://journals.plos.org/plospathogens/article?id=10.1371/journal.ppat.1009775) . The crosslinker is sulfo-SDA and it is searched from K,S,T,Y,nterm to any amino acid.


![System](https://private-user-images.githubusercontent.com/44289027/337014006-ce5f4358-264f-43ab-a226-ef946a93de18.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTc2MjI0OTUsIm5iZiI6MTcxNzYyMjE5NSwicGF0aCI6Ii80NDI4OTAyNy8zMzcwMTQwMDYtY2U1ZjQzNTgtMjY0Zi00M2FiLWEyMjYtZWY5NDZhOTNkZTE4LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDA2MDUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwNjA1VDIxMTYzNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWIxYzM1NGUwYTZjMzA5NmNkYjJiYWEzNzY1MDBhN2IzZGZhNTRmYTRkZjU5Y2MyNTFlNzY4N2FjZjQyN2QzMDEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.VQvQRjxMyesJuGawkp9ERmh4PGYKAD3t7i9bPgy9BvE)


### From raw data to crosslinks
Open xiSEARCH. 

In the files tab, load peak files (recal*.mgf files) and sequence file (complex.fasta) and select an output name.

In the settings tab, tick on "multiple crosslinkers" and select SDA and non-covalent, deselect BS3. Why is that? [citation](https://pubs.acs.org/doi/epdf/10.1021/acs.analchem.8b04037)

Select number of threads, memory and set missed cleavages to 4.

In variable modifications, deselect BS3 modifications and select SDA-loop and SDA-OH.

Tick "Do FDR" and keep threshold to 2% at the residue pair level, boosting heteromeric crosslinks.

This is a very simplified "how to" guide, but there is a lot of complexity to this. In particular, the size of the database may need to be adjusted to include contaminants, and the FDR settings may need to be tweaked in order to have enough targets and decoys to properly model the noise and to do a proper statistical control of the results.

[documentation for the search engine here](https://github.com/Rappsilber-Laboratory/xisearch)

[documentation for FDR estimation engine here](https://github.com/Rappsilber-Laboratory/xifdr)

### analyze crosslinking MS dataset on xiview.org

Create your own account in xiview.org and upload the results, or else proceed with the pregenerated dataset as below.

Open the dataset in the xiview.org interactive viewer [here](https://xiview.org/network.php?upload=27449-11563-41954-87027-74439). You can expand each protein with the right click of the mouse to see where the crosslinks are localised on the sequence. 

Crosslinks may also be visualised in the circle plot, accessible from "views"... "circular"

At the bottom of the viewer, you have several toggles:

- self/heteromeric: toggle crosslinks within protein sequences or between protein sequences on or off. As the experimnt is peptide based, a "self" link can also be between multiple copies of the same protein
- overlap/non-overlap: toggle crosslinks that are self but between multiple copies of the same protein (not relevant here)
- Score: crosslink score. This is an arbitrary number specific to each search engine. The higher, the better- a greater number indicates a better quality of peptide-spectrum match. This slider should be used for visualization purposes only. A key property of FDR control is that the results after FDR control are not further subsettable, or else the FDR becomes unknowable. For a more stringent dataset, repeat the FDR procedure with a tighter threshold.
- Distance: Filter by distance once a PDB is uploaded to the session.
- Residue pairs per PPI: filter the network so that only protein pairs with more than X crosslinks are displayed
- filter boxes: filter by peptide sequence, protein name, description. On the right also boxes for  run name and scan number.

Top panel includes tabs for uploading various files, including PDB files, and for analysing crosslink data.

#### Gathering statistics
All run files for the experiments with low SDA concentrations are called "Ratio24". The ones with the high SDA concentrations are called "Ratio56". Using the filters, take a look at how many crosslinks and how many heteromeric crosslinks correspond to either condition.

#### Viewing spectra
Let's get an idea for what crosslinked peptide spectra look like. In the scan box, select scan 7144 and select the resulting crosslink. From the dropdown menu at the top, select views-> spectrum.

Take a moment to familiarize yourself with the viewer. At the top of the spectral window you see the error in matching the precursor (whole peptide) and its mass and charge state. 

The vertical hockey pucks along the sequence are the fragment ions covering the sequence. You can hover over them with the mouse to reveal which part of the sequence they cover and to which peak they correspond. Each fragment ion may have more than one peak supporting it, as there may be versions that are unmodified and versions that have sustained the loss of water or ammonia groups.

Sometimes for this crosslinker, the exact crosslink site is not known as backbone fragmentation is incomplete. In this case, the program assigns the site to the last compatible amino acid in a stretch of equivalent linkage positions. 

You can check how the spectrum would look with a different assignment by moving the crosslink site with a mouse. For more radical reannotations, you can click on the wheel and change the sequence or enter custom annotation commands.

The group of Andrea Sinz [has observed](https://pubs.acs.org/doi/10.1021/acs.analchem.7b04915) that diazirine crosslinkers such as sulfo-sda may cleave in the gas phase. We can check if this has happened here by introducing a custom annotation for it. 

Inside the spectral viewer, click the wheel and then the "custom" tab, copy the following line

    crosslinker:AsymetricSingleAminoAcidRestrictedCrossLinker:Name:SDA;MASS:82.04186484;FIRSTLINKEDAMINOACIDS:*;SECONDLINKEDAMINOACIDS:K,S,T,Y,nterm;STUBS:A,82.041864,S,0

that accounts for a cleavable crosslinker, and click "apply".


Is this annotation better than the previous one? click "butterfly" at the top of the viewer to check.

Finally, let's look at crosslinks supported by scans that barely pass the FDR. Filter to a low spectral matching score (<10) and select a crosslink. Open the spectrum viewer. Check the difference with the high ranking spectra. 

Always check the quality of the spectra before staking a biological interpretation on sparse crosslinking data!

#### Interacting with the dataset
In the "Histogram" and "scatterplot sections of the view, several properties of the dataset may be investigated.

Using the box to select "frac6" and "frac9", check out if there is a difference in number of crosslinks, charge state and precursor mass of earlier chromatographic fractions and latter ones.

What consequences does this have for experimental design?

In the upload tab, go to "sequence annotations  " and upload the file XXX.csv. In the "annotation" tab at the top, toggle annotations on. You should now see domains highlighted on the sequence. 

In this case, we used a custom sequence annotation file (sequence_annotations.csv), as our proteins are recombinant and we searched with an in-house sequence file containing the tags. For proteins with uniprot IDs in the sequence file headers, xiview will automatically download this information from uniprot.


#### Working with PDB files
Upload the file "state-3_fit_chains.pdb" from the course package. in view, select the 3d viewer. In the "annotation" tab at the top, toggle off the domains and select "PDB aligned region". What do you notice? Which protein is missing from the experimental structure?

Let's look at the 3d structure now. To check if the crosslinks are satisfied by this model, open "view", "legends and colors" and then color the crosslinks by distance. Let's set satisfied up to 25 angstrom, borderline 25-30 and violated over 30 angstrom. Go back to the 3d viewer. What do you see? You can also toggle between all crosslinks and heteromeric only. Monitor the distances on the circle plot.

For a more quantitative overview, check the histogram tab and plot by distance, or the scatterplot tab and plot crosslink score vs distance.

### In-depth 3d analysis

#### Binding patch
Select SAMHD1 crosslinks in the protein selection box, and toggle off self links.

Go back to the 3d viewer and toggle the display to "residues with half links" from the dropdown menu.

#### Flexibility
Within the 3d viewer, you can upload the 3 different PDBs and check the distance of critical crosslinks.

To work with crosslinking data in chimerax, one can export the links from the 3d viewer by clicking on 3d export.. chimerax pseudobond file.

To work directly in chimerax, you can instead use the X-MAS plugin. X-MAS is a plugin by the Scheltema group [citation](https://www.biorxiv.org/content/10.1101/2022.04.21.489026v2)

Open chimerax and load the session.cxs from the course package.

Go to tools... more tools and install x-mas plugin.

Go to tools.. structure analysis... XMAS. In the tool, click on "import files". Navigate to results files and load the "peptide pairs" file. Select State 2 pdb and map crosslinks.

Click on "visualize". You can color by distance here, or export to other programs like DisVis for mapping patches and similar.

To remove dashes, you set dashes to 0 inside X-mas or use the command

    style pbonds dashes 0

The advantage of working in chimerax is that you may load densities at the same time, as well as take advantage of much powerful visualization options.

### Modeling
Disvis. Check out DisVis [here](https://wenmr.science.uu.nl/disvis/) or, later, download the package and run locally, from [here](https://github.com/haddocking/disvis). DisVis calculates the volume of the positions of the center of mass of protein B consistent with N restraints stemming from protein A. In our case, we can position the SAMHD1 CTD against Vpr with it.

AlphaLink. A modified version of AlphaFold 2 that pays attention to experimental crosslinks. Run via colab [here](https://colab.research.google.com/github/Rappsilber-Laboratory/AlphaLink2/blob/main/notebooks/alphalink2.ipynb). Citation [here](https://www.nature.com/articles/s41587-023-01704-z).

Other programs include: [IMP](https://integrativemodeling.org/) (integrative modeling platform), [Assembline](https://www.embl-hamburg.de/Assembline/), [HADDOCK](https://wenmr.science.uu.nl/haddock2.4/) .