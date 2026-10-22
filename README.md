# EEG-Based Emotion and Mental Stress Recognition Using Machine Learning

## 📌 Project Overview

This project develops a machine-learning-based system to recognize emotion-related conditions and detect cognitive stress from Electroencephalogram (EEG) signals. It integrates signal processing, feature extraction, and machine learning models into an interactive **Streamlit web application**.

The application allows users to upload EEG recordings and view predicted emotional conditions, stress probabilities, alpha and beta band power, and a valence-arousal visualization.

## 🎯 Objectives

- Develop an EEG preprocessing and feature extraction pipeline.
- Recognize four emotion-related conditions using the GAMEEMO dataset.
- Detect cognitive stress by distinguishing resting EEG from EEG recorded during mental arithmetic.
- Train and compare Random Forest, Logistic Regression, and 1D Convolutional Neural Network (1D-CNN) models.
- Evaluate model performance on subjects excluded from training.
- Build an interactive web application for EEG analysis and visualization.

## 🧠 Datasets

### 1. GAMEEMO Dataset — Emotion Recognition

- Contains EEG recordings from 28 subjects using a 14-channel Emotiv EPOC+ headset.
- Includes four game-related conditions:
  - Boring
  - Calm
  - Horror
  - Funny
- Used for four-class emotion-related condition recognition.

Dataset: [GAMEEMO on Mendeley Data](https://data.mendeley.com/datasets/b3pn4kwpmn/3)

### 2. PhysioNet EEG Dataset — Cognitive Stress Detection

- Contains EEG recordings from 36 subjects.
- Includes resting-state and mental arithmetic task recordings.
- Used to distinguish rest from task-related cognitive load.

Dataset: [EEG During Mental Arithmetic Task Performance](https://physionet.org/content/eegmat/1.0.0/)

## ⚙️ Methodology

The system follows these stages:

1. **EEG data loading:** Load recordings from the supported datasets.
2. **Signal preprocessing:** Remove DC offsets, apply a 1–45 Hz band-pass filter, and resample signals where required.
3. **Window segmentation:** Divide EEG signals into 4-second windows with a 2-second step.
4. **Artifact rejection:** Remove windows containing extreme signal amplitudes.
5. **Feature extraction:** Calculate logarithmic spectral power across delta, theta, alpha, beta, and gamma frequency bands.
6. **Additional features:** Extract hemispheric asymmetry and alpha/beta ratio features.
7. **Normalization and calibration:** Apply subject-specific normalization or rest-baseline calibration where supported.
8. **Classification:** Predict emotion-related conditions or cognitive stress using trained machine-learning models.
9. **Visualization:** Display prediction results and EEG feature analysis through the Streamlit application.

## 📊 EEG Frequency Bands

| Band | Frequency Range |
|---|---|
| Delta | 1–4 Hz |
| Theta | 4–8 Hz |
| Alpha | 8–13 Hz |
| Beta | 13–30 Hz |
| Gamma | 30–45 Hz |

Alpha and beta power are highlighted in the application to help users explore differences in EEG activity.

## 🤖 Machine Learning Models

- **Random Forest:** Main classification model for emotion recognition and stress detection.
- **Logistic Regression:** Baseline model for performance comparison.
- **1D-CNN:** Deep-learning model evaluated for emotion recognition.

Model evaluation uses leave-subjects-out cross-validation to assess generalization to previously unseen subjects and reduce the risk of data leakage.

## 📈 Reported Results

The following results were obtained during evaluation on held-out subjects, as documented in the project report.

### Cognitive Stress Detection

| Evaluation Setting | Window-Level ROC-AUC | Recording-Level ROC-AUC |
|---|---:|---:|
| With rest calibration | 0.878 | 0.942 |
| Without calibration | 0.748 | 0.789 |

### Emotion Recognition

| Model | Macro-F1 | ROC-AUC |
|---|---:|---:|
| Logistic Regression | 0.568 | 0.803 |
| Random Forest | 0.755 | 0.927 |
| 1D-CNN | 0.609 | 0.825 |
| Random Forest + CNN average | 0.686 | 0.908 |

*Note: Emotion recognition results shown here use per-person normalization. Performance can vary depending on calibration, data quality, and the evaluation setting.*

## 🌐 Streamlit Web Application

The application provides two analysis modes.

### Emotion Recognition Mode

- Upload supported GAMEEMO EEG recordings.
- View predicted emotion-related conditions and class probabilities.
- Explore alpha and beta band power and the alpha/beta ratio.
- Visualize the predicted condition on a valence-arousal plane.

### Cognitive Stress Detection Mode

- Upload a resting EEG recording and a recording to analyze.
- Use the resting recording for baseline calibration.
- View the predicted state and stress probability.
- Inspect per-window probability traces and frequency-band power.

## 🛠️ Technology Stack

- **Programming Language:** Python
- **Machine Learning:** Scikit-learn
- **Deep Learning:** TensorFlow/Keras
- **Signal Processing:** SciPy, MNE-Python
- **Data Processing:** NumPy, Pandas
- **Visualization:** Matplotlib
- **Web Framework:** Streamlit
- **Model Persistence:** Joblib
- **Development Environment:** Google Colab

## 🚀 Installation and Usage

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
```

Replace the repository URL with your actual GitHub repository address.

### 2. Install Dependencies

Make sure Python is installed, then install the required packages:

```bash
pip install numpy pandas scipy scikit-learn mne tensorflow streamlit matplotlib joblib
```

Additional dependencies may be required depending on the files and imports used in your implementation.

### 3. Prepare the Project Files

Ensure that the application, shared preprocessing modules, trained model files, and other required assets are available in the expected directory structure.

The application requires compatible trained models and supported EEG recordings to perform inference.

### 4. Run the Streamlit Application

```bash
streamlit run app.py
```

Open the local URL displayed in the terminal to access the application.

For Google Colab, run Streamlit in the notebook environment and configure a suitable tunnel if external browser access is required.
