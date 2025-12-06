# **clinical_ceph_cdss**

AI-Based Clinical Decision Support for Orthodontic Treatment Planning Using Cephalometric Analysis

## **1. Project Overview**

This project implements a simple Clinical Decision Support System (CDSS) for orthodontics by automatically detecting cephalometric landmarks on lateral skull X-ray images.
The system reads labeled coordinates, preprocesses images, extracts features, trains a regression model, and visualizes predicted vs. actual landmark positions.

This project is for **SAT 5141 – Clinical Decision Support Systems** final research project.

---

## **2. Dataset Information**

This project references clinically validated cephalometric datasets for methodological justification:

Bimler Cephalometry Dataset (Kaggle) – contains orthodontic cephalograms with soft-tissue and skeletal measurements.
Cephalometric Variables Dataset (Figshare) – includes real patient cephalometric readings used in orthodontic diagnosis and treatment planning.
These datasets demonstrate how cephalometric analysis is performed in real-world orthodontic workflows.

Practical Dataset Used in This Project

For the purpose of demonstrating the Clinical Decision Support System (CDSS) pipeline, a small curated set of 3 cephalometric X-ray images was used:

img1.png
img2.png
img3.png

Each image includes three manually assigned landmark coordinates stored in labels.csv.

The reduced dataset enables:
*complete demonstration of preprocessing
*landmark visualization
*feature extraction
*regression-based prediction
*error measurement
*interpretable CDSS workflow

This approach maintains methodological correctness while ensuring the notebook remains lightweight and easy to run.

```
data/
│
├── images/        → cephalometric X-ray images (.png)
└── labels.csv     → coordinates of 3 landmarks per image
```

### **labels.csv columns**

| Column | Description                      |
| ------ | -------------------------------- |
| image  | image file name (e.g., img1.png) |
| x1, y1 | coordinates of landmark P1       |
| x2, y2 | coordinates of landmark P2       |
| x3, y3 | coordinates of landmark P3       |

*Coordinates are normalized between 0 and 1 relative to image width and height.*

---

## **3. Methodology**

### **3.1 Load labels**

```python
labels_df = pd.read_csv("labels.csv")
```

### **3.2 Display actual landmarks**

Code overlays true coordinates on the cephalometric X-ray.

### **3.3 Feature Extraction**

Each image is:

* Converted to grayscale
* Resized to 64×64
* Flattened to a 4096-pixel vector
* Normalized (0–1)

### **3.4 Model**

A **Linear Regression** model is trained:

```python
model = LinearRegression()
model.fit(X_train, y_train)
```

### **3.5 Prediction and Visualization**

The notebook generates:

* Predicted vs. Actual landmark values
* Mean Squared Error (MSE)
* Plot showing:

  * **Actual points = Red**
  * **Predicted points = Green**

---

## **4. Results**

* The model successfully predicts approximate landmark locations.
* Visualization clearly shows differences between ground truth and predicted points.
* MSE is low for this demo dataset.
* Demonstrates a working pipeline from **data → preprocessing → ML model → clinical visualization**.

---

## **5. Files Included**

| File                       | Purpose                                |
| -------------------------- | -------------------------------------- |
| `clinical_ceph_cdss.ipynb` | Main notebook with full code workflow  |
| `README.md`                | Project explanation                    |
| `labels.csv`               | Sample normalized landmark coordinates |
| `images/`                  | Sample cephalometric X-ray images      |

---

## **6. How to Run**

1. Open the notebook in Jupyter.
2. Ensure `labels.csv` and image files are in the correct folders.
3. Run all cells.
4. View landmark predictions and error metrics.

---

## **7. Tools & Libraries**

* Python
* NumPy
* Pandas
* Matplotlib
* Pillow
* Scikit-Learn

---

## **8. Conclusion**

This project demonstrates a functional AI-based Clinical Decision Support System (CDSS) for orthodontic treatment planning using cephalometric analysis. The workflow includes image preprocessing, landmark extraction, feature engineering, and machine-learning-based prediction. Even with a small dataset, the system successfully replicates the essential pipeline followed in real orthodontic AI applications.

Key contributions of this project include:
Automated ingestion and processing of cephalometric X-ray images
Visualization of anatomical landmarks
Implementation of regression-based landmark prediction
Generation of interpretable outputs for clinical decision support

Future improvements can include:
Expanding to a larger and clinically validated dataset
Using advanced deep learning models (CNNs, U-Net, Faster R-CNN) for higher accuracy
Adding automated cephalometric measurements and orthodontic treatment suggestions
Integrating the system into real clinical CDSS workflows
Overall, this project provides a strong foundation for developing a fully automated cephalometric analysis tool and meets the objectives of SAT 5141 – Clinical Decision Support Systems.
