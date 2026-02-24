# assignment-2
# UCS654 Predictive Analysis Using Statistics  
## Assignment–2  
## Learning Probability Density Functions Using Roll-Number-Parameterized Non-Linear Model

---

## 1. Introduction

This assignment focuses on learning an unknown probability density function using real-world air quality data. A nonlinear transformation parameterized by the university roll number is applied to the data, and a Generative Adversarial Network (GAN) is used to learn the probability distribution of the transformed variable using samples only. No analytical or parametric form of the probability density function is assumed.

---

## 2. Dataset Information

The dataset used for this assignment is the **India Air Quality Dataset** obtained from Kaggle. From the complete dataset, only the Nitrogen Dioxide (**NO₂**) concentration values are used for analysis. These values are represented by the variable `x`. Missing and invalid entries in the NO₂ column are removed before further processing.

---

## 3. Methodology

The overall approach consists of three main stages as described below.

---

### Step 1: Roll-Number-Based Nonlinear Transformation

Each NO₂ data value `x` is transformed into a new variable `z` using the nonlinear transformation:

\[
z = x + a_r \sin(b_r x)
\]

The parameters `a_r` and `b_r` are calculated from the university roll number `r` using the formulas:

\[
a_r = 0.5 \times (r \bmod 7)
\]

\[
b_r = 0.3 \times ((r \bmod 5) + 1)
\]

For the roll number **102303731**, the computed values are:

| Parameter | Value |
|----------|-------|
| a_r | 2.5 |
| b_r | 0.6 |

This roll-number-dependent transformation ensures that each student works with a unique transformed dataset.

---

### Step 2: Learning the Probability Distribution Using GAN

The transformed variable `z` is assumed to be sampled from an **unknown probability distribution**. No parametric form (such as Gaussian or exponential) is assumed.

A **Generative Adversarial Network (GAN)** is designed and trained using only samples of `z`:

- The **Generator** takes random noise sampled from a standard normal distribution `N(0,1)` and generates fake samples of `z`.
- The **Discriminator** attempts to distinguish between real transformed samples and fake samples produced by the generator.

Both networks are trained adversarially until the generator produces samples that resemble the real transformed data.

---

### Step 3: PDF Approximation from Generator Samples

After training the GAN, a large number of samples are generated using the trained generator. These generated samples are used to estimate the probability density function of `z` using **Kernel Density Estimation (KDE)**.

The estimated density represents the learned probability distribution of the transformed variable.

---

## 4. GAN Architecture

### Generator Network
- Input: 10-dimensional random noise vector  
- Hidden Layers: Fully connected layers with ReLU activation  
- Output: Single scalar value representing generated `z`  

### Discriminator Network
- Input: Single `z` value  
- Hidden Layers: Fully connected layers with ReLU activation  
- Output: Probability indicating whether the sample is real or fake  

The architectures are lightweight and suitable for learning a one-dimensional probability distribution.

---

## 5. Results

The trained generator produces samples whose estimated probability density function closely matches the structure of the transformed data distribution. The learned PDF is smooth and captures the dominant characteristics of the data.

A plot of the estimated probability density function obtained from GAN-generated samples is shown below.

---

## 6. Observations

- **Mode Coverage:**  
  The generator captures the dominant mode of the distribution without collapsing to a single point.

- **Training Stability:**  
  Training remains stable with minor fluctuations, and no severe mode collapse is observed.

- **Quality of Generated Distribution:**  
  The generated samples result in a smooth and realistic probability density function that reflects the underlying structure of the transformed data.

---
## 7. Histogram

<img width="584" height="455" alt="download" src="https://github.com/user-attachments/assets/668ebc9c-3556-47f6-8e32-0aecfe52e3f6" />

---
## 8. Conclusion

In this assignment, a roll-number-based nonlinear transformation was applied to NO₂ air quality data. A Generative Adversarial Network was used to learn the probability density function of the transformed variable using data only, without assuming any analytical form. The results demonstrate the effectiveness of GANs in modeling unknown probability distributions.

---

## 9. Software and Tools Used

- Google Colab  
- Python  
- NumPy  
- Pandas  
- TensorFlow / Keras  
- Matplotlib  
- SciPy  


---
