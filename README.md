# Sensorimotor-rhythm-research
The file processing consists of 3 parts, first of all, downsampling of data up to 500 is carried out.
Then, standard preprocessing is performed: filtering (Low pass filter: 70 Hz, High pass filter: 0.5 Hz), selecting the desired segment (starting point s13, required recording length 292s), removing bad channels and segments (manually), interpolating bad channels, ICA with guidance (alice_ml), and re-referencing (average). The file is then saved for the first time, after which it is cut into epochs with the removal of bad epochs and saved for the second time.
The third stage is spectral analysis by C3 and C4 leads, and building an averaged graph.
