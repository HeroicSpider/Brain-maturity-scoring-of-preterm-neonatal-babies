**The EEG component of this dataset is available as part of R1.0.0 at https://legacy.openfmri.org/dataset/ds000116/**

Data acquisition methods have been described in detail in Walz et al. (2013, J Neurosci), but we outline them here and provide file information for clarity and ease of use.

————————————————————————————————
ODDBALL PARADIGM
————————————————————————————————

3 runs each of separate auditory and visual tasks
20% target stimuli (requiring button response), 80% standard stimuli (to be ignored)
stimulus duration 200 ms
ITI 2-3 sec, uniformly distributed 
first 2 stimuli constrained to be standards
each run consisted of 125 total stimuli

AUDITORY
target - broadband “laser gun” sound
standard - 390 Hz tone 

VISUAL
target - large red circle on isoluminant grey background (3.45 degree visual angle)
standard - small green circle on isoluminant grey background (1.15 degree visual angle)


————————————————————————————————
EEG DATA
————————————————————————————————

custom built MR-compatible EEG system with differential amplifier
custom cap configuration using bipolar electrode pairs and twisted leads
1000 Hz sampling rate
49 channels 
start triggered by fMRI scan start and EEG clock synced with scanner clock on each TR.


CHANNEL KEY

chan 1-43 (or 1-34 in the re-referenced electrode space)
EEG (for locations refer to cap diagram and bipolar mapping table, described in SUPPLEMENTARY FILES section below)

chan 44 
EOG - horizontal

chan 45
EOG - vertical

chan 46-47 (or chan 35 in the re-referenced electrode space)
ECG

chan 48 (or chan 36 in the re-referenced electrode space)
stimulus event markers
baseline 0 value jumps to 25 at start of task
value 125 is auditory standards
value 150 is auditory targets
value 225 is visual standards
value 250 is visual targets

chan 49 (or chan 37 in the re-referenced electrode space)
behavioral event markers
baseline value 0 with value 100 indicating response 


RAW EEG DATA (EEG_raw.mat)

This is the completely raw EEG recording, contaminated with gradient and BCG artifacts. 
range is -8 to +8 V (amplifier gain was set to 10K)


GRADIENT-FREE EEG DATA (EEG_noGA.mat)

units of uV
This is the data following gradient-artifact removal using mean (across TRs for each channel) subtraction method and standard filtering. BCG artifact remains. 
Note: these are the data we used for classification in our study.


RE-REFERENCED GRADIENT-FREE EEG DATA (EEG_rereferenced.mat)

units of uV
This is the same data as above, but in the 34-channel electrode space. Re-referencing is performed via a basic matrix operation using the shortestpath.m (see SUPPLEMENTARY FILES section below).  Noisy channels (subjectively determined by visual inspection) were excluded prior to re-referencing; due to oversampled system design, this does not cause loss of electrodes.

subject	excluded bipolar pair channels
sub001 	[8 24]
sub002 	[5 30]	
sub003 	[29 30 34 36]
sub004 	[23 24 30]
sub005 	[8 30]
sub006 	[9 24 30]
sub007 	[30]
sub008 	[28 29 30 33 36]
sub009 	[29 30 33]
sub010 	[24 29 33]
sub011 	[16 24 30]
sub012 	[30]
sub013 	[30]
sub014 	[30]
sub015 	[8 16 28 34 37]
sub016 	[16 24 30 28 37]
sub017 	[7 33]


————————————————————————————————
BOLD fMRI DATA
————————————————————————————————

3T Philips Achieva MR Scanner
single channel send and receive head coil 
EPI sequence
170 TRs per run
2 s TR
25 ms TE 
32 slices
3x3x4 mm resolution 
no slice gap
AC-PC alignment


The supplied explanatory variable files 
- cond001.txt - target stimuli
- cond002.txt - standard stimuli
- cond003.txt - reaction time
contain only trials with correct responses and clean EEG. To include all trials, one can easily create new model files from the behavdata.txt files.  


IMPORTANT NOTES ABOUT PREPROCESSING

* Slices were not acquired in interleaved order. Refer to the slice_order.txt file (single column FSL format) if you choose to perform slice timing correction.

* The scanner began the EPI pulse sequence a few seconds prior to the start of recording, so there is no need to discard the first few TRs, as is commonly done with fMRI data. 

* EEG wires can create field inhomogeneities that are sometimes visible on the images, particularly on the left posterior region closest to where the wires were bunched together as they exited the coil. Bias field correction can optionally be performed using FSL FAST without the need of a field map.
 

————————————————————————————————
ANATOMICAL MRI DATA
————————————————————————————————

- highresSPGR001.nii.gz - SPGR 1x1x1 mm (present for all subjects except sub010)
- highresMPRAGE001.nii.gz - MPRAGE 1x1x1 mm (for sub010 and additionally exists for a few others)
- highresEPI001.nii.gz - high resolution single volume EPI 2x2x2 mm


————————————————————————————————
SUPPLEMENTARY FILES
————————————————————————————————

EEG RE-REFERENCING 

- shortestpath.m - Matlab function used to re-reference EEG data from 43-channel bipolar pair space to 34-channel electrode space. See function help for more info.  Dependencies are efmri36mastoids.ced location file (supplied) and EEGLAB readlocs.m function (free download from UCSD).

ELECTRODE LOCATIONS

- efmri36mastoids.ced - location file for re-referenced data that includes mastoid channels.
- locations_34_EEG.ced - location file for 34 electrodes.
- EEGfMRI_cap_diagram.png - for easy reference.
- EEGfMRI_cap_bipolar_pair_mapping.pdf - table showing mapping from bipolar pair space to electrode space.

fMRI ACQUISITION

- slice_order.txt - single column FSL format custom slice timing correction file. This is the order in which slices were acquired by the scanner (i.e. not interleaved).


————————————————————————————————
PUBLICATIONS
————————————————————————————————

Walz JM, Goldman RI, Carapezza M, Muraskin J, Brown TR, Sajda P (2015) “Prestimulus EEG Alpha Oscillations Modulate Task-Related fMRI BOLD Responses to Auditory Stimuli,” Neuroimage 113:153-163. doi: 10.1016/j.neuroimage.2015.03.028.

Conroy B, Walz JM, Cheung B, Sajda P (2014) “Fast Simultaneous Training of Generalized Linear Models (FaSTGLZ)” arXiv 1307.8430.

Walz JM, Goldman RI, Carapezza M, Muraskin J, Brown TR, Sajda P (2013) “Simultaneous EEG-fMRI Reveals Temporal Evolution of Coupling between Supramodal Cortical Attention Networks and the Brainstem,” J Neurosci 33(49):19212-22. doi: 10.1523/JNEUROSCI.2649-13.2013.

Walz JM, Goldman RI, Carapezza M, Muraskin J, Brown TR, Sajda P (2013) “Simultaneous EEG-fMRI reveals a temporal cascade of task-related and default-mode activations during a simple target detection task,” Neuroimage. 2013 Aug 17. pii: S1053-8119(13)00868-9. doi: 10.1016/j.neuroimage.2013.08.014.

Conroy BR, Walz JM, Sajda P (2013) “Fast bootstrapping and permutation testing for assessing reproducibility and interpretability of multivariate FMRI decoding models,” PLoS One. 2013 Nov 14;8(11):e79271. doi: 10.1371/journal.pone.0079271.
