# Evening QC Cyto 2025

<img src="https://github.com/DavidRach/EveningQC_Cyto2025/blob/main/EveningQCPoster.png" >


This repository is for our '““Wait, when was QC last run???” Evaluating MFI drift after morning QC and its impact on unmixing.”' poster. It contains the data and R code needed to hopefully reproduce our analysis and figures, as well as the .svg files used to create the figures in Inkscape.

## Organization

The .csv files for the respective analyses are stored in the data folder, from which they can be accessed by the code. The code is contained within the Quarto Markdown (.qmd) files named after the respective figure. The .svg files can be opened with Inkscape to access the Figure assembly layout. 

## Luciernaga

Please note, you will need to install [Luciernaga](https://github.com/DavidRach/Luciernaga) to reproduce some of the Figures. The package version utilized for running of the code in this manuscript was the 0.99.4 release. 

## Raw Data

Due to size constraints, this repository only contains the processed data files derrived from our original .fcs files. The actual .fcs files are being uploaded to ImmPort (SDY3080) and will be available at the next release cycle. 

## Abstract

**““Wait, when was QC last run???” Evaluating MFI drift after morning QC and its impact on unmixing.”**

David Rach1, Mikayla Trainor2, Natarajan Ayithan2, Xiaoxuan Fan2

1 Molecular Microbiology and Immunology Graduate Program, University of Maryland School of Medicine, Baltimore, USA 2 Flow Cytometry Shared Resource, University of Maryland Greenebaum Comprehensive Cancer Center, Baltimore, USA

At our core, quality control (QC) beads are run daily on Cytek Aurora instruments as part of the instrument startup process. Based on the beads initial observed MFI values for each detector, the SpectroFlo software adjusts the gains and laser settings of the instrument to ensure that the after-QC MFI values match lot-specific thresholds. This accounts for instrumental changes, allowing specimens acquired on different days to be comparable, and reducing the frequency of MFI-based batch effects in large spectral flow cytometry panels. We recently implemented a website to monitor daily QC for our instruments at our core https://umgccfcss.github.io/InstrumentQC/, visualizing longitudinal changes in gain, RCV, and bead MFI values before and after daily QC. In the process, we observed various detectors for which MFI values pre-QC were consistently different from the MFI values observed after QC the day before. While MFI was reset to baseline at the following QC, we were curious whether these observed MFI drifts would have already occurred by the evening before, or were a result of the instrument shutdown. Additionally, we wanted to evaluate whether these drifts were sufficient to impact unmixing when samples were acquired in the evening compared to shortly after morning QC.

To evaluate this, we acquired 5000 SpectroFlo QC beads as fcs files, i) before morning QC, ii) after morning QC, iii) before evening QC, and iv) after evening QC. These samples were acquired on a 3, 4, and 5-laser Aurora over a several month period, for both the 2005 and 2006 SpectroFlo QC bead lots. For analysis, acquired FCS files were imported to R, singlet beads gated, and gate placement validated using the flowWorkspace, openCyto and Luciernaga R packages. From the gated events, median MFI and RCV values were calculated for each detector, and voltage/gain metadata for individual .fcs files was retrieved using the Luciernaga package. We then visualized this data in R using various tidyverse packages. We observed that for most detectors, there were limited changes in MFI values between the After Morning QC and Before Evening QC timepoints. However, we noted consistent and significant shifts in MFI for a few detectors by the time of evening QC, notably the YG2, YG3, and R1 detectors. To evaluate whether these observed drifts in MFI would have altered normalized fluorescent signature, we simulated the equivalent day-specific adjustment to reference signatures of over 100 fluorophores, plotting the adjusted signatures against the original reference signature. We observed that the drift in the handful of detectors did not significantly alter the normalized fluorescent spectra of the fluorophore, with exception of a few fluorophores where the detector in question landed on the secondary peak of the spectra. When evaluating the signatures by their cosine value, the differences were within range we would anticipate limited impact on unmixing.

Finally using the same approach, we adjusted raw reference controls and full-stained samples acquired following morning QC and imported into SpectroFlo for unmixing. We did not observe any major changes to the unmixing in medium-sized panels. In summary, for the instruments at our core, the majority of detector MFI values remain stable following morning QC. Additionally, for the few detectors that did consistently shift, based on both simulated and experimental data, the observed changes would have minimal impact for most fluorophores signatures and subsequent unmixing. Whether these observed small changes are enough to affect unmixing in large panels (40+) colors remains an area that merits further investigation.
