
# PDF Estimation of Transformed NO₂ Data using GAN


## Overview

This project aims to learn the unknown probability density function (PDF) of a transformed NO₂ concentration variable using a Generative Adversarial Network (GAN).
No analytical or parametric form of the PDF is assumed. The distribution is learned only from data samples, as required in the assignment.
## Dataset

Dataset: India Air Quality Dataset

Feature Used: no2 (NO₂ concentration)

Preprocessing Steps:

Removed missing values

Removed extreme outliers (top 1%)
## Step 1: Data Transformation

Each NO₂ value 
𝑥
x is transformed using the function: z=x+ar​⋅sin(br​⋅x)

Transformation Parameters

University Roll Number: 102303958

a_r = 0.5 × (r mod 7) = 2.5

b_r = 0.3 × (r mod 5 + 1) = 1.2

Final Transformation  

This transformation introduces strong non-linearity, resulting in an unknown and non-parametric distribution for the transformed variable 
𝑧
z.



## Step 2: PDF Estimation using GAN

A Generative Adversarial Network (GAN) is designed and trained to learn the distribution of the transformed variable 
𝑧
z using only its samples.

GAN Architecture
Generator

Input: Random noise sampled from 
𝑁
(
0
,
1
)
N(0,1)

Architecture:
32 → 128 → 256 → 128 → 1

Activation Functions:

Leaky ReLU (hidden layers)

Linear (output layer)

Output: Generated samples 
𝑧
𝑓
z
f
	​


Discriminator

Input: Single scalar value

Architecture:
1 → 128 → 256 → 128 → 1

Activation Functions:

Leaky ReLU (hidden layers)

Sigmoid (output layer)

Output: Probability of the input being real

The discriminator learns to distinguish:

Real samples: 
𝑧
z

A Generative Adversarial Network (GAN) is designed and trained to learn the distribution of the transformed variable 
𝑧
z using only its samples.

GAN Architecture
Generator

Input: Random noise sampled from 
𝑁
(
0
,
1
)
N(0,1)

Architecture:
32 → 128 → 256 → 128 → 1

Activation Functions:

Leaky ReLU (hidden layers)

Linear (output layer)

Output: Generated samples 
𝑧
𝑓
z
f
	​


Discriminator

Input: Single scalar value

Architecture:
1 → 128 → 256 → 128 → 1

Activation Functions:

Leaky ReLU (hidden layers)

Sigmoid (output layer)

Output: Probability of the input being real

The discriminator learns to distinguish:

Real samples: 
𝑧
z

Fake samples: 
𝑧
𝑓

𝐺
(
𝜖
)
z
f
	​

=G(ϵ), where 
𝜖
∼
𝑁
(
0
,
1
)
ϵ∼N(0,1)

No parametric PDF (Gaussian, exponential, etc.) is assumed at any stage.
	​

=G(ϵ), where 
𝜖
∼
𝑁
(
0
,
1
)
ϵ∼N(0,1)

No parametric PDF (Gaussian, exponential, etc.) is assumed at any stage.
## Step 3: PDF Approximation from Generator Samples

After training the GAN:

A large number of samples are generated from the generator.

Kernel Density Estimation (KDE) is applied to approximate the learned PDF.

The KDE of generated samples is compared with the KDE of real transformed data.


![image alt](https://github.com/mahim83/Predictive-analytics-assignment-2/blob/2358fb8a140a5921844c1b95657aa526f50f222e/pdf.png)


## Final Results

Transformation Parameters

Roll Number : 102353018
a_r = 2.5
b_r = 1.2


GAN Architecture

Generator     : 32 → 128 → 256 → 128 → 1
Discriminator : 1 → 128 → 256 → 128 → 1


Observations

Mode Coverage

The GAN successfully captures the major modes of the transformed data.

No evidence of mode collapse is observed.

Mode Coverage: Good

Statistical Measures

KS Statistic      : 0.3762
Wasserstein Dist. : 11.15
