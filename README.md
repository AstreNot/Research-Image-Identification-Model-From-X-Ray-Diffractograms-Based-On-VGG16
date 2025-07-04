# Image Identification Model From X-Ray Diffractograms Based On VGG16
This project presents a deep learning approach for identifying material phases using X-ray diffractograms (XRD) images. Leveraging the power of the VGG16 convolutional neural network, the model classifies XRD patterns into specific material categories with the goal of automating phase recognition in material science. By converting diffractograms into images and fine-tuning a pre-trained VGG16 architecture, this project demonstrates how computer vision can enhance traditional material analysis, supporting faster and more scalable research workflows.
The repository includes the dataset preprocessing steps, model training scripts, evaluation metrics, and example predictions.

## 📥 Data Collection
The dataset was generated by simulating X-ray diffractograms from crystal structure files in CIF format. These CIFs were collected from the Crystallography Open Database (COD), which serves as the primary source of structural data. Each CIF file contains atomic coordinates and lattice parameters for a unique crystalline phase, which were used to calculate theoretical diffraction patterns.

## 🔗 Data Sources
Primary Source:

1. Crystallography Open Database (COD)
An open-access repository of crystal structures, providing CIF files for thousands of inorganic, organic, and metal-organic compounds.
Note:
Only synthetic diffractograms generated from these CIFs are used in the project. No experimental or proprietary XRD measurements are included.

## 🧹 Data Preparation
Diffractogram Simulation:
CIF files were parsed to extract structural information.
Simulation of the diffractograms was carried out using the open-source xrayutilities library that computes peak positions and intensities based on Bragg's Law and structure factor calculations.
Peak intensity vs. 2θ values were computed for Cu Kα radiation (λ = 1.5406 Å).

Image Generation:
Simulated XRD patterns were plotted using matplotlib.
Each plot was saved as a standardized PNG image (224x224 pixels, black background, white lines) for CNN training.
![calcium chlorite1-2](https://github.com/user-attachments/assets/fddb5a95-14ad-4fe8-86ae-9cdda89a51ef)

Preprocessing:
Images were resized and normalized to meet VGG16 input requirements.
Data augmentation (rotation, contrast shift) was applied to increase dataset diversity.

Labeling & Organization:
Each image was labeled according to its crystal class or material group (e.g., cubic, tetragonal, orthorhombic).
A clean directory structure was maintained

Dataset Splitting:
Training: 70%
Validation: 20%
Test: 10%

## 🧠 Model Architecture
This project utilizes the VGG16 convolutional neural network as the backbone for classifying simulated X-ray diffractogram images. VGG16 was selected for its deep but simple architecture and proven performance in image classification tasks.

### 🔧 Configuration:
Base Model: VGG16 (pre-trained on ImageNet)
Input Shape: 224 × 224 × 3
Trainable Layers: Last convolutional block
Architecture Modifications:
Removed original top layers (include_top=False)
Added GlobalAveragePooling2D
Added Dense layer(s) with ReLU activation
Final output layer with Softmax activation for multi-class classification


### 🧮 Training Setup:
Loss Function: Categorical Crossentropy
Optimizer: Adam (learning rate = 0.0001)
Metrics: Accuracy
Early Stopping: Based on validation loss
Epochs: 50 (with early stopping)
Batch Size: 32

The model was trained on a dataset of simulated XRD pattern images, categorized by crystal system or material class, to learn pattern-based features relevant to phase identification.
## 🏋️ Training & Evaluation
The training process was designed to fine-tune the VGG16 model on the simulated XRD image dataset while avoiding overfitting and maximizing generalization.

Training Details
Dataset Split:
Training Set: 70%
Validation Set: 20%
Test Set: 10%

Augmentation Techniques:
Peak area
2theta steps
Peak position shifts

Evaluation Metrics
Model performance was evaluated on the test set using:
Accuracy
Loss

A confusion matrix and classification report were generated to assess class-wise performance. The model showed potential to distinguish between visually similar diffractograms of different materials, though confusion remained between classes with overlapping peak positions.

| Metric            | Value |
| -------------     | ----- |
| Training Accuracy | 88.4% |
| Training Loss     | 0.356 |
| Testing Accuracy  | 76.4% |
| Testing Loss      | 0.863 |

