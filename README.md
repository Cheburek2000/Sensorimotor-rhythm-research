# Sensorimotor-rhythm-research
Sensorimotor rhythm (mu-rhythm) is a type of electrical activity of the brain that occurs while moving or observing the movements of other people. Studies show that children with impaired speech development often experience a change in sensorimotor rhythm, which may indicate a violation of the functioning of the brain responsible for speech processes.

The study that uses this repository examines the correlations between the mu-rhythm of normotypic children aged 3-4 years and their speech development (speech development is assessed using the PLS-5 methodology). In the future, a sample of non-typical children of the same age cohort will be created to compare the results.

The file processing consists of 3 parts, first of all, downsampling of data up to 500 is carried out.
Then, standard preprocessing is performed: filtering (Low pass filter: 70 Hz, High pass filter: 0.5 Hz), selecting the desired segment (starting point s13, required recording length 292s), removing bad channels and segments (manually), interpolating bad channels, ICA with guidance (alice_ml), and re-referencing (average). The file is then saved for the first time, after which it is cut into epochs with the removal of bad epochs and saved for the second time.
The third stage is spectral analysis by C3 and C4 leads, and building an averaged graph.
