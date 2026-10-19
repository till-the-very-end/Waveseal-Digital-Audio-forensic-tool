
WaveSeal — Digital Audio Forensics Tool
Modern Education Society’s Wadia College of Engineering, Pune
Department of Computer Engineering
Academic Year: 2026–27
Mini Project Report
Subject: 410244(C): Cyber Security and Digital Forensics
Project Title: Design and Develop a Tool for Digital Forensics of Audio
Project Name: WaveSeal
Faculty Name: Prof. J. A. Kalbhor
Deployed Application: https://waveseal.streamlit.app/
Submitted By
Name	PRN
Pranav Sarmukaddam	F2311057
Prachi Nailkar	F2311054


Class: B.E. Computer Engineering
Table of Contents
1. Abstract
2. Introduction
3. Audio Evidence Description
4. System Architecture and Technology Stack
5. Audio Preprocessing and Feature Extraction
6. Forensic Detection Model
7. Implementation Details
8. Performance Evaluation
9. Screenshots and Visualisations
10. Conclusion and Future Scope
Project Workflow
Audio Evidence → Hashing → Metadata Extraction → Signal Processing → Forensic Analysis → Authenticity Score → Verdict → Report
Five Forensic Pillars
Forensic Pillar	Weight
Acoustic Continuity	30%
Noise Floor Stability	25%
Silence Authenticity	20%
Signal Dynamics and ENF	15%
Container and Metadata	10%


The five pillars provide independent indicators that are combined into a single preliminary forensic assessment rather than relying on one signal characteristic alone.
1. Abstract
WaveSeal is a digital audio forensic tool developed for the preliminary examination of audio recordings for possible signs of manipulation. Digital audio can be modified through cutting, splicing, replacement, or insertion of artificial silence, making systematic examination important when a recording is used as digital evidence.

The system accepts common audio formats, including WAV, MP3, FLAC, OGG, and M4A. It examines uploaded evidence using signal-processing techniques together with file metadata and cryptographic analysis.

WaveSeal uses five forensic pillars: Acoustic Continuity, Noise Floor Stability, Silence Authenticity, Signal Dynamics and ENF, and Container and Metadata Analysis. These modules examine possible splice boundaries, changes in background noise, digitally inserted silence, signal characteristics, and possible editing-software signatures.

The results are combined into a weighted Forensic Authenticity Index (FAI) ranging from 0 to 100 percent. The system produces a corresponding forensic verdict and provides visual evidence such as waveform and spectrogram analysis.

Cryptographic MD5, SHA-1, SHA-256, and SHA-512 hashes are generated for evidence identification. A structured PDF forensic report containing evidence information, hashes, findings, and visual evidence can also be generated.

The application is implemented using Python-based signal-processing libraries and deployed through Streamlit, providing a browser-based interface for preliminary digital audio forensic examination.
2. Introduction
2.1 Background
Digital audio recordings are increasingly used as digital evidence in investigations, journalism, legal proceedings, surveillance, and institutional activities.

The availability of audio-editing software has also made manipulation easier. A recording may be cut, spliced, reordered, muted, or combined with another recording while still appearing normal during playback.

Digital audio forensics examines the technical properties of a recording to identify possible indicators of such manipulation. These indicators can occur within the audio signal as well as in the file structure and metadata.

WaveSeal applies signal-processing and file-analysis techniques to perform this preliminary examination in a single application.
2.2 Problem Statement
Traditional audio forensic examination may require specialised software and trained analysts. Preliminary examination can therefore become time-consuming when several recordings need to be checked.

The project aims to develop an accessible tool that accepts an audio recording, analyses multiple forensic indicators, and presents the findings in a structured form.
2.3 Objectives
The main objectives are:
- Develop a web-based audio forensic examination tool.
- Support commonly used audio formats.
- Generate cryptographic hashes for evidence identification.
- Extract metadata and possible software signatures.
- Detect acoustic discontinuities and possible splice locations.
- Analyse background noise consistency and digital silence.
- Analyse signal dynamics and ENF-related characteristics.
- Generate an authenticity score and forensic report.
2.4 Scope
WaveSeal focuses on preliminary examination of digital audio using signal-processing and file-level forensic techniques.

The system is intended for academic work, preliminary screening, research demonstrations, and digital investigation workflows. It is not intended to replace detailed examination by a qualified forensic expert.
2.5 Working Process
1. Upload the audio evidence.
2. Generate cryptographic hashes.
3. Extract metadata and file information.
4. Decode and prepare the audio signal.
5. Perform signal and spectral analysis.
6. Execute the forensic analysis modules.
7. Calculate the Forensic Authenticity Index.
8. Generate the forensic verdict and report.
2.6 Expected Outcome
The system provides:
- Evidence information and cryptographic hashes.
- Forensic pillar scores.
- Detected anomaly locations.
- Waveform and spectrogram visualisations.
- Final forensic verdict.
- Downloadable forensic report.
2.7 Limitations
The current implementation primarily uses signal-processing heuristics rather than a trained machine-learning classifier.

Audio is standardised to 22,050 Hz and analysed in mono. Therefore, some high-frequency and stereo-phase information is not retained.

Advanced manipulations such as sophisticated time stretching and pitch shifting are not specifically detected.

The result is intended as a preliminary forensic assessment and requires expert examination when the evidence is being used for formal investigation.
3. Audio Evidence Description
3.1 Supported Evidence
WaveSeal works with audio evidence supplied by the investigator. The supported formats include WAV, MP3, FLAC, OGG, and M4A.
Format	Use
WAV	Uncompressed audio examination
MP3	Compressed audio examination
FLAC	Lossless compressed audio
OGG	Open compressed audio
M4A	Common compressed audio container


3.2 Evidence Information
The application extracts basic information such as:
- Filename and format.
- Duration and sample rate.
- Number of channels.
- Bitrate, where available.
- Metadata and software information.
3.3 Cryptographic Hashing
WaveSeal generates MD5, SHA-1, SHA-256, and SHA-512 hashes.

These hashes provide reproducible identifiers for the evidence file. The values are included in the forensic report so that the examined file can be identified and checked again later.
Purpose of Evidence Identification
Hashing does not determine whether an audio recording is authentic. Its purpose is to establish a stable digital identifier for the exact file that was examined.
3.4 Controlled Test Evidence
The project includes a synthetic test-sample generator. An authentic five-second PCM-16 signal at 22,050 Hz is used as the base sample.

A corresponding tampered sample contains a known foreign audio segment and a digitally inserted zero-energy silence segment. This provides a controlled environment for testing the forensic pipeline.
3.5 Audio Loading
Different audio formats may require different decoding libraries. WaveSeal therefore uses a fallback loading strategy based on SoundFile, Librosa, PyAV, pydub, and the Python wave module.

This improves compatibility between local environments and the Streamlit deployment.
3.6 Signal Preparation
After loading, the audio is converted into a numerical signal representation. The signal is prepared for:
- Time-domain analysis.
- Frequency-domain analysis.
- Noise-floor estimation.
- Silence detection.
- Audio-health measurements.
3.7 Audio Health Metrics
The system calculates peak amplitude, RMS level, clipping percentage, and crest factor.

These measurements provide supporting information about the characteristics of the recording before the main forensic analysis.
3.8 Evidence Handling
The original uploaded file is retained for hashing and metadata examination. Signal processing is performed on its decoded representation while the original file identity is preserved through cryptographic hashes.
4. System Architecture and Technology Stack
4.1 System Architecture
WaveSeal follows a modular layered architecture with four main layers.
Layer	Components
Presentation Layer	Streamlit web application and CLI
Core Analysis Layer	Audio Processor, Tamper Detector, Metadata Extractor
Output / Reporting Layer	Visualisations and PDF report
Utility / Data Layer	Synthetic Audio Generator and samples


4.2 Data Flow
Audio File
    |
    v
Hashing and Metadata Extraction
    |
    v
Signal Processing
    |
    v
Forensic Analysis
    |
    v
Authenticity Score and Verdict
    |
    v
PDF Report
4.3 Technology Stack
- Python: Main programming language.
- Streamlit: Web interface and deployment.
- Librosa: Audio signal processing.
- SoundFile: Audio input and output.
- Mutagen: Metadata extraction.
- NumPy and SciPy: Numerical and signal processing.
- Matplotlib: Forensic visualisation.
- FPDF2: PDF report generation.
4.4 Deployment
The application is deployed through Streamlit Community Cloud.

Deployed application: https://waveseal.streamlit.app/
5. Audio Preprocessing and Feature Extraction
5.1 Signal Representation
After an audio file is loaded, the recording is converted into a numerical signal that can be processed using digital signal-processing methods.

The system standardises the audio for analysis and uses the resulting signal for time-domain, frequency-domain, and anomaly analysis.
5.2 Short-Time Fourier Transform
The Short-Time Fourier Transform (STFT) is used to analyse how the frequency content of the audio changes over time.

WaveSeal uses an FFT size of 2048 and a hop length of 512. The resulting representation is also used to generate the spectrogram.
5.3 Audio Features
The acoustic analysis uses three important features:
- Spectral Flux: Measures change in spectral magnitude between successive frames.
- RMS Energy: Represents the energy level of the audio signal.
- Spectral Centroid: Represents the centre of spectral energy.
These features complement each other. A splice may produce a sudden change in frequency distribution, energy, or spectral position even when the waveform appears visually continuous.
5.4 Feature Normalisation
The extracted features are normalised using Median Absolute Deviation (MAD). This provides a robust measure that is less affected by isolated extreme values.

The normalised features are then used by the acoustic continuity detector to locate possible discontinuities.
5.5 Acoustic Continuity
The combined anomaly score is calculated as:
\[
S = 0.50F + 0.35R + 0.15C
\]
where:
- \(F\) represents spectral flux.
- \(R\) represents RMS difference.
- \(C\) represents spectral centroid difference.
An adaptive threshold is applied to the resulting score. Adjacent anomalous frames are grouped so that a single possible splice does not produce multiple unrelated detections.
5.6 Background Noise Floor
The recording is divided into one-second windows and the background noise floor is estimated using the tenth percentile of frame-level RMS energy.

A sudden change in the estimated noise floor may indicate that segments from different recording environments have been combined.
5.7 Digital Silence Detection
Natural recordings normally contain small amounts of room tone or microphone noise even during pauses.

WaveSeal examines gaps between non-silent sections. A gap with extremely low amplitude and variation can be reported as possible digitally inserted silence.
5.8 Signal Dynamics
The system also examines:
- Peak amplitude.
- RMS level.
- Clipping percentage.
- Crest factor.
- Power around 50 Hz and 60 Hz.
These measurements provide additional supporting information about the recording and are used as part of the overall forensic assessment.
6. Forensic Detection Model
6.1 Five-Pillar Model
WaveSeal combines five forensic components.
Pillar	Weight	Purpose
Acoustic Continuity	30%	Splice and cut detection
Noise Floor Stability	25%	Recording-environment changes
Silence Authenticity	20%	Digital silence detection
Signal Dynamics and ENF	15%	Signal characteristics
Container and Metadata	10%	File and software analysis


6.2 Forensic Authenticity Index
The composite score is calculated as:
\[
FAI = 0.30A + 0.25N + 0.20S + 0.15D + 0.10M
\]
where:
- \(A\) = Acoustic Continuity score.
- \(N\) = Noise Floor Stability score.
- \(S\) = Silence Authenticity score.
- \(D\) = Signal Dynamics and ENF score.
- \(M\) = Container and Metadata score.
The weighted score combines the individual indicators instead of depending on a single characteristic of the recording.
6.3 Metadata and Software Analysis
Metadata is extracted using Mutagen and selected binary regions are examined for possible software signatures.

The system checks for indicators associated with commonly used audio-editing tools. A software signature is treated only as supporting evidence and does not by itself prove manipulation.
6.4 Verdict Classification
Score	Verdict	Interpretation
≥ 88%	Authentic	No major manipulation indicators
70–87.9%	Inconclusive / Suspicious	Further review required
< 70%	Tampered / Manipulated	Strong manipulation indicators


Important: The verdict is a preliminary heuristic assessment, not proof of authenticity or tampering. Thresholds and scores should be validated against representative test data before being used in operational forensic decisions.
7. Implementation Details
7.1 Project Structure
WaveSeal/
├── app.py
├── cli.py
├── streamlit_app.py
├── core/
│   ├── audio_processor.py
│   ├── tamper_detector.py
│   ├── metadata_extractor.py
│   └── report_generator.py
├── utils/
│   └── audio_generator.py
├── assets/
├── samples/
└── requirements.txt
7.2 Major Modules
- Audio Processor: Handles audio loading, signal processing, health metrics, and visualisation.
- Tamper Detector: Implements the five-pillar forensic analysis and calculates the combined score.
- Metadata Extractor: Generates hashes and examines metadata and software signatures.
- Report Generator: Produces the structured forensic PDF report.
- Audio Generator: Creates controlled authentic and tampered test samples.
7.3 Processing Pipeline
Upload
  |
  v
Hash
  |
  v
Metadata
  |
  v
Signal Analysis
  |
  v
Forensic Audit
  |
  v
Verdict and Report
7.4 CLI Interface
The project also provides a command-line interface for running the forensic pipeline without the browser interface.
python cli.py path/to/audio.wav
The CLI provides access to evidence information, hashes, forensic scores, detected anomalies, and report generation.
8. Performance Evaluation
8.1 Evaluation Method
WaveSeal is a signal-processing-based forensic system rather than a supervised machine-learning classifier.

The system is evaluated using controlled audio samples containing known modifications. This provides a reproducible way to examine whether the forensic modules identify the expected anomalies.
8.2 Controlled Tampered Sample
The benchmark contains an authentic five-second PCM-16 signal sampled at 22,050 Hz and a corresponding tampered version.
Modification	Time	Expected Indicator
Foreign audio segment	2.0–2.5 s	Acoustic discontinuity
Digital zero silence	3.8–4.3 s	Digital silence


8.3 Expected Forensic Findings
The foreign audio segment is intended to create a detectable change in acoustic characteristics. The zero-energy region provides a controlled example for the digital silence detector.

The system records detected anomaly locations so that they can be compared with the known modification intervals.
8.4 Forensic Output
The system produces:
- Forensic Authenticity Index.
- Final verdict.
- Detected anomaly timestamps.
- Five-pillar scores.
- Audio-health measurements.
- Cryptographic hashes.
- Forensic visualisations.
- PDF forensic report.
The generated report provides a structured record of the examination that can be stored with the original evidence.

Evaluation note: The modification intervals above describe the test design and expected indicators. Actual detection accuracy, precision, recall, false-positive rate, and timing error should be reported only after running the implementation against labelled test samples.
9. Screenshots and Visualisations
Replace the placeholders below with screenshots captured from the deployed application or local implementation.

9.1 Home Page
The home page provides the audio upload interface and the starting point for the forensic examination.

Figure 1: WaveSeal home page and audio upload interface

![Figure 1: WaveSeal home page and audio upload interface](screenshots/home-page.png)
9.2 Forensic Overview
The overview displays the authenticity score, final verdict, and important forensic findings.

Figure 2: Forensic overview and final verdict

![Figure 2: Forensic overview and final verdict](screenshots/forensic-overview.png)
9.3 Waveform and Spectral Analysis
The analysis interface provides the waveform, detected anomaly locations, and spectral information.

Figure 3: Waveform and detected anomaly locations

![Figure 3: Waveform and detected anomaly locations](screenshots/waveform-anomalies.png)

Figure 4: Spectral analysis and audio-health information

![Figure 4: Spectral analysis and audio-health information](screenshots/spectral-analysis.png)
10. Conclusion and Future Scope
10.1 Conclusion
WaveSeal is a web-based digital audio forensic tool developed for the preliminary examination of audio evidence.

The system combines signal processing, metadata analysis, and cryptographic verification to identify possible indicators of manipulation. Its five-pillar model examines acoustic continuity, background noise, digital silence, signal characteristics, and file metadata.

The results are combined into a Forensic Authenticity Index and presented through a forensic verdict, visual evidence, cryptographic hashes, and a structured PDF report.

The project demonstrates the practical application of digital signal processing and digital forensics to audio evidence.
10.2 Project Outcomes
- Developed a web-based audio forensic tool.
- Implemented cryptographic hashing and metadata analysis.
- Implemented acoustic, noise, and silence analysis.
- Developed a weighted forensic authenticity score.
- Generated forensic visualisations and PDF reports.
- Deployed the application using Streamlit.
10.3 Future Scope
- Deep-learning-based splice detection.
- Advanced ENF and stereo analysis.
- Additional cepstral and reverberation features.
- Batch processing and forensic API support.
- Digital signatures for generated forensic reports.
References and Project Link
- WaveSeal deployed application: https://waveseal.streamlit.app/
- Python, Streamlit, Librosa, SoundFile, Mutagen, NumPy, SciPy, Matplotlib, and FPDF2 documentation may be cited according to the versions used in the implementation.
