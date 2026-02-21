# Epileptic-Seizure-Detection-Feature-Ranking-Sensor-Diagnostics
This project was developed as part of my MSc in Computational Intelligence at the Aristotle University of Thessaloniki (AUTH). It focuses on the automated 
classification of epileptic states (Pre-ictal vs. Ictal) using multi-channel intracranial EEG (iEEG) data.

## The Problem Logic

The dataset consists of 76 sensors recording brain activity. The challenge is not just to classify the state, but to identify which sensors provide the most 
diagnostic value. Instead of feeding raw data into a model, I focused on Feature Engineering to extract physically meaningful descriptors.

## Feature Engineering: Hjorth Descriptors

To characterize the temporal dynamics of the iEEG signals, I implemented Hjorth Descriptors. These parameters provide a compact representation of the signal’s 
statistical properties in the time domain:

  
  Activity: Represents the signal power.
  
  Mobility: An estimate of the mean frequency.
  
  Complexity: Measures the change in frequency

Transforming 76 channels into 228 attributes (3 per sensor) allowed for a more granular analysis of how seizure activity affects different brain regions.

## The "Worst-Sensor" Validation Approach

While standard procedures focus on identifying the most informative features, I modified the selection logic to perform a diagnostic stress-test. I specifically 
identified and isolated the worst sensor based on t-test ranking scores.

## Why this approach?

By isolating the sensor with the lowest ranking (e.g., Sensor 29), I aimed to validate the feature ranking algorithm. If the algorithm is robust, the 
classification performance using only the "worst" sensor should drop significantly, ideally approaching random chance levels.

## Results & Performance

Feature Ranking: The 228 attributes were ranked using a t-test criterion. The gap between top-tier and bottom-tier sensors was substantial, highlighting the 
localized nature of ictal activity.

Leave-One-Out Cross-Validation (LOOCV): I evaluated the system's performance using Linear Discriminant Analysis.

Validation Outcome: Classification accuracy using the "worst" sensor fell to approximately 100% , confirming that the worst sensor (29) was classified as the worst
because of the bad performance of the Complexity

Visual Diagnostics: Analyzing the z-scores (relative increase in activity) confirmed that ictal events show minimal deviation from the baseline in low-ranked 
sensors, justifying their exclusion from a diagnostic pipeline.

## Technical Stack

Language: MATLAB

Key Functions: rankfeatures, classify, classperf

Dataset: 76-channel iEEG 


<img width="1913" height="912" alt="Figure_3" src="https://github.com/user-attachments/assets/f30c6074-2764-4c0f-ba8e-e921fd6556ac" />

<img width="1872" height="884" alt="Figure_2" src="https://github.com/user-attachments/assets/8e7d288b-c2ec-46ca-942f-4c91e2a75b20" />

<img width="1912" height="912" alt="Figure_1" src="https://github.com/user-attachments/assets/cb49d46d-b3f1-4443-95a4-3cffeceebfc1" />

<img width="1963" height="884" alt="Figure_4" src="https://github.com/user-attachments/assets/51d50a86-da34-43b3-9a8a-60879af21b13" />

