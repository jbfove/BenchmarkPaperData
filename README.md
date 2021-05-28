# Benchmark Paper Data

This repository contains raw data for an eye-tracker benchmark. It can be used to reproduce the results contained in the paper [Important Considerations of Data Collection and Curation for Reliable Benchmarking of End-User Eye-Tracking Systems](https://dl.acm.org/doi/proceedings/10.1145/3448017), published with ETRA '21, the ACM Symposium on Eye Tracking Research and Applications.

It is also useful as a generally available real-world eye-tracking dataset for testing data curation and processing methods.

## Structure

This repository contains a set of 157 data collections, each corresponding to one participant. The data was collected in 2018 and 2019, primarily in Japan, but also small amounts were collected in various other countries.

Each participant was asked to look at a series of random static points in a VR headset, and the 3D virtual location of those points, as well as the eye tracker output, were recorded. Many more details of the collection process are included in the paper.

For each collection, there is a JSON file containing limited information about the participant, especially things of possible relevance to eye-tracker performance, such as ethnicity, eye color, makeup, etc. This data is reported by the participants themselves.

The corresponding CSV for each collection contains the raw data. The data is organized as follows:

| Column          | Meaning                                                   |
|-----------------|-----------------------------------------------------------|
| 1. Timestamp    | How many seconds into the collection the sample was taken |
| 2. Eye          | 0 for the left eye, 1 for the right eye                   |
| 3. GroundTruthX | Horizontal component of virtual target                    |
| 4. GroundTruthY | Vertical component of virtual target                      |
| 5. GroundTruthZ | Forward component of virtual target                       |
| 6. ETGazeX      | Horizontal component of estimated gaze vector             |
| 7. ETGazeY      | Vertical component of estimated gaze vector               |
| 8. ETGazeZ      | Forward component of estimated gaze vector                |

## Interpretation

* +X is to the participants right
* +Y is upwards
* +Z is forwards, in front of the participant

The CSV files contain only frames with valid ET output. For every target displayed to the participant, frame recordings started at the moment when the participant made a click to represent that they are fixated on the target, and each recording lasted for at least 250ms. Frames where the eye-tracker failed to output a gaze estimation were not included into the data.

The ETGaze vector is a unit vector representing the output of the eye-tracker gaze estimation for that eye, and only has directional information.

The GroundTruth vector is the location of the virtual target that was displayed to the participant in VR.

For datasets 1 through 147, the GroundTruth vector represents the 3D location of the target displayed to the participant in VR. The origin point (0, 0, 0) represents the midpoint between the participants eyes.

Datasets 148 through 157 instead use a "real world-based" ground truth definition instead of "projection matrix-based". The ground truth vector is instead defined as a directional unit vector for each eye separately.

The VR system used (FOVE 0) has a fixed IPD of 63mm. The participants IPD was not measured.
