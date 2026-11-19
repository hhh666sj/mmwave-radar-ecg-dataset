# Paired mmWave Radar and ECG Dataset

## Overview

This dataset contains 32 paired radar and electrocardiogram (ECG) records from eight participants. Each participant contributes four 60-second records. Radar data were collected using a TI AWR1843 radar.

## Files and naming

| Directory / file | Description |
| --- | --- |
| `radar_32x60s/` | 32 raw radar ADC binary files |
| `ecg_32x60s/` | 32 ECG CSV files |
| `metadata.csv` | Record index, relative paths, sampling settings, and file sizes |
| `S1.zip` through `S8.zip` (Releases) | One ZIP per participant; four radar and four ECG files |

Files are named `S<participant>-<record>`. Participant IDs range from S1 to S8; record numbers range from 1 to 4. For example, `S1-1.bin` and `S1-1.csv` form one paired record from participant S1.

## Radar data

Each BIN file contains 184,320,000 bytes of headerless raw ADC data. The acquisition configuration used by the existing processing pipeline is:

| Parameter | Value |
| --- | --- |
| Radar | TI AWR1843 |
| ADC representation | Complex signed 16-bit samples |
| ADC samples per chirp | 256 |
| Receive channels | 4 |
| Transmit channels | 3 |
| TDM cycles per frame | 1 |
| Frame rate | 250 frames/s |
| Frames per record | 15,000 |
| Record duration | 60 s |

BIN files contain no embedded acquisition configuration. The original radar configuration and an ADC decoder should accompany any processing code; the table alone does not specify the complete binary packing or RF configuration.

## ECG data

Each CSV contains a header and 15,000 samples. The sampling rate used by the existing processing pipeline is 250 Hz, corresponding to 60 seconds per file. There is no timestamp column; sample time can be constructed as `t = sample_index / 250`, starting at zero.

| Column | Description |
| --- | --- |
| `Raw_ECG` | Raw ECG device output |
| `Filtered_ECG` | Filtered ECG device output |
| `Heart_Rate_BPM` | Device-provided heart rate in beats per minute |

ECG waveform amplitudes are retained in the device's native numerical scale; no conversion to millivolts is specified. Device-provided heart rate is not independently validated ground truth. Zero entries should not be interpreted as a physiological heart rate of zero.

Records are paired by filename. A shared time origin is assumed by the existing processing pipeline; no independently estimated synchronization offset is supplied here.

## Download

Download the eight participant archives from [Releases](https://github.com/hhh666sj/mmwave-radar-ecg-dataset/releases).
Each archive contains four radar BIN files and four paired ECG CSV files.
Extract all eight archives into one directory, preserving their `radar_32x60s/` and `ecg_32x60s/` subdirectories.
The extracted dataset occupies approximately 5.91 GB.

The Git repository contains documentation and metadata. The data files are distributed as Release attachments; Git LFS is not required.

## Use and citation

This repository currently contains data and documentation. No processing results or diagnostic claims are implied. A dataset reuse license and paper citation have not yet been specified by the owner; public availability alone does not grant unrestricted reuse rights.
