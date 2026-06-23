# Plan: Deploy The Tutorial With GitHub Pages

## Summary
Deploy the tutorial as a static GitHub Pages site from the `website` branch. The published page should remain a contained `index.html`; all practical course files should be downloaded from the shared Google Drive folder.

Course files:
https://drive.google.com/drive/folders/1P5WDwfDGmUzZPOy35eC9pzqVHvLYQWO1?usp=sharing

## Deployment Model
- Host the webpage with GitHub Pages.
- Use branch `website`.
- Use folder `/root`.
- Keep `index.html` at the repository root as the site entry point.
- Keep large data and practical files in Google Drive, not in the GitHub Pages payload.
- Use the website as the guided tutorial and file map; use Drive as the course-material download location.

## Course File Strategy
All course files used in the practical should be available from the Google Drive folder:
- `peakfiles/recal*.mgf`: recalibrated MS2 peak files for xiSEARCH.
- `complex.fasta`: reduced search database.
- `state-2_fit-chains.pdb`, `state-3_fit-chains.pdb`, `state-4_fit-chains.pdb`: structural models for xiview, ChimeraX, and DisVis interpretation.
- `result files/*.csv`: xiSEARCH pre-FDR output.
- `result files/*.mzID`: mzIdentML output for public deposition and for generating xiview sessions.
- `result files/CSM table`: FDR-controlled xiFDR output at the CSM level.
- `result files/Links table`: FDR-controlled xiFDR output at the residue-pair/link level.
- `result files/Peptide pair table`: FDR-controlled xiFDR output at the peptide-pair level.
- `sequence_annotations.csv`: xiview annotations, if included.
- `disvis/`: precomputed DisVis inputs and outputs, including Vpr-localization maps.

## Pre-Deployment Checklist
- Confirm `index.html` links to the Drive folder with a clear `Download course material` button.
- Confirm the `File or resource` table says files come from Google Drive.
- Confirm the Drive folder is shared as `Anyone with the link can view`.
- Confirm Drive folder names match the tutorial text:
  - `peakfiles`
  - `result files`
  - `disvis`
- Confirm filenames in Drive match the tutorial examples closely enough for students to find them.
- Commit `index.html` and `PLAN.md` on the `website` branch.
- Leave `.idea/` untracked.

## GitHub Pages Setup
1. Push branch `website` to GitHub.
2. Open the GitHub repository settings.
3. Go to `Settings -> Pages`.
4. Set `Source` to `Deploy from a branch`.
5. Select branch `website`.
6. Select folder `/root`.
7. Save the Pages settings.
8. Wait for the Pages deployment to finish.

Expected URL:
https://grandrea.github.io/crosslinking-ms-tutorial/

## Post-Deployment Test Plan
- Open the GitHub Pages URL.
- Verify the homepage loads at `/crosslinking-ms-tutorial/`.
- Verify the `Download course material` button opens the Google Drive folder without sign-in.
- Verify the `Open xiview dataset` button opens the pregenerated xiview session.
- Verify embedded xiview screenshots and the gel image render.
- Verify internal section links work from the left navigation.
- Verify checkboxes, collapsible panels, and copy buttons work.
- Verify external links to xiSEARCH, xiFDR, xiview, PRIDE, DisVis, HADDOCK, ChimeraX, X-MAS, and citations open correctly.
- Verify Drive file descriptions match the actual folder contents.
- Test in one desktop viewport and one mobile viewport.

## Maintenance Notes
- If Drive folder or file organization changes, update only `index.html` and this plan.
- If direct Drive links to individual files become stable, they can replace the single folder link in the table.
- Keep the repository lightweight; do not commit MGF files, large result files, DisVis maps, or large archives.
- If the site later needs analytics, custom styling, or generated assets, add them without introducing a build step unless there is a clear need.
