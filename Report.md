---
title: Cognition Computation
author: Giulio Umbrella
geometry: margin=2cm
---

# Introduction

The goal of the project is to replicate the result of the lab practice lecture but with a different architecture, a **convolutional autoencoder**.

In [section 2](#convolutionl-autoencoder) I introduce the convolutionl autoencoder. In [section 3](#linear-read-out) I test the model ability to compress data using a simple perceptron as a linear readout. In [section 4](#feed-forward-network) I compare the linear readout with a feedforward network. In [section 5](#transfer-learning) I test the model's ability to identify basic component by applying the readout on a different dataset. In [section 6 ](#robustness-to-noise). In [section 7](#adversarial-learning).

# Convolutional autoencoder

The goal of an autoencoder is to learn how to compress the data. The autoencoder is organized in two main components the *encoder* takes the original dataset and obtain a smaller and simplified  representation. The decoder instead mirrors the encoder structure and reconstructs the original input, undoing the effect of the encoder on the compressed dataset.  

This type of learning is *unsupervised*, thus I does not require to provide any labeling.

## Dataset

The dataset for the training is the *MINST*, composed by handwritten digits of size 28*28 of values between 0 and 255. The dataset is initially normalized between 0 and 1 by dividing each observation by 255. The image is grayscale, thus the convolutional layer has only one channel in input.

The transfer learning is tested on the normalized *Fashion MINST* dataset.

## Network architecture

The encoder has four different layers, two convolutional and two fully connected. Each convolutional layer has a one unit padding and a two by two max pooling window. Thus the image size halves at each iteration.

1. enc1: 3x3 kernel, 1 channel in input, 32 different channels in output,
2. enc2: 3x3 kernel, 32 channels in input, 16 channels in outpu
3. linear1: fully connected layer with size (7 x 7 x 16, 80)
4. linear2: fully connected layer with size (80, 49)  

The decoder has the same structure in reverse order.

## Network training

The training of the model follows the standard pattern; first I define a ConvAutoencoder class representing the model, then I define a training function to compute the gradient descend.  

The training has the following components:

- Optimizer: Adam
- Loss function: as the goal is to reconstruct the compressed image rather than classify it, I applied the mean squared error loss function.
- Number of epochs: 5
- Batch size: 100

Table \ref{training_loss_table} shows that the training loss drops quickly.

Table: (Training loss by epoch) \label{training_loss_table}

| Epoch | Training loss |
|:-----:|:-------------:|
|   0   |     0.0463    |
|   1   |     0.0121    |
|   2   |     0.0080    |
|   3   |     0.0059    |
|   4   |     0.0047    |

To visual inspect the reconstruction capabilities of the model, I compared the original and reconstructed images. As an example, Figure \ref{org_rec} shows a comparison.  

![Original and Reconstructed image \label{org_rec}](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/orginal_reconstructed.png){width=75%}

## Layer analysis

The first convolutional layer produces in output 32 different channels and each of them has a 3x3 filter. Figure \ref{first_lyr_filters} shows the features identified by each channel after the training. To highlight the behavior, I set a 0.2 absolute value threshold when printing the image.

![First layer filters \label{first_lyr_filters}](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/conv_autoencoder_firstlayer_fiiters.png){width=75%}

In Figure \ref{first_lyr_filters} we can observe that the filters are indeed specializing in identifying some structural components of the digits. Among the other we can identify the following behaviors:

- Filter 05:
- Filter 12:        
- Filter 26: 

To show the effect of each filter on some digits, I take one digits and plot the effect of the first layer. Figure \ref{first_lyr_filters_sample_digit} shows how the filter of Figure \ref{first_lyr_filters} modify the input - together with the activation function and the pooling.

- Seven 05:
- Seven 12:        
- Seven 26:

![First layer filters sample digit \label{first_lyr_filters_sample_digit}](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/conv_autoencoder_firstlayer_fiiters_sample.png){width=75%}

The second layer is more complex because it has 32 input channels, so the number of parameters increases. For each of the 16 output channels, I have 32 kernels of size 3x3. The filter values scale to a lower order of magnitude, so I need to adjust the threshold constraints.

![Second layer filters sample \label{second_lyr_filters_sample}](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/conv_autoencoder_secondlayer_fiiters.png){width=75%}



# Linear read-out

To test the

![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/perceptron_receptive_fields.png)

| Perceptron | 0   | 1    | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
|------------|-----|------|-----|-----|-----|-----|-----|-----|-----|-----|
| 0          | 900 | 1    | 3   | 15  | 1   | 9   | 15  | 4   | 30  | 2   |
| 1          | 0   | 1085 | 7   | 7   | 0   | 1   | 4   | 0   | 31  | 0   |
| 2          | 18  | 7    | 837 | 32  | 31  | 19  | 41  | 16  | 27  | 4   |
| 3          | 5   | 20   | 59  | 754 | 1   | 58  | 6   | 34  | 57  | 16  |
| 4          | 3   | 5    | 5   | 0   | 812 | 2   | 13  | 6   | 11  | 125 |
| 5          | 14  | 21   | 29  | 142 | 28  | 565 | 15  | 15  | 48  | 15  |
| 6          | 7   | 21   | 29  | 1   | 13  | 17  | 862 | 0   | 8   | 0   |
| 7          | 3   | 24   | 12  | 7   | 15  | 1   | 0   | 855 | 21  | 90  |
| 8          | 15  | 37   | 9   | 63  | 16  | 55  | 21  | 29  | 716 | 13  |
| 9          | 11  | 17   | 5   | 15  | 63  | 4   | 0   | 55  | 25  | 814 |
Table: caption


![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/dendogram_complete.png)

![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/dendogram_single_linkage.png)


# Feed Forward Network

| FFN | 0   | 1    | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
|-----|-----|------|-----|-----|-----|-----|-----|-----|-----|-----|
| 0   | 934 | 0    | 4   | 3   | 1   | 5   | 24  | 1   | 8   | 0   |
| 1   | 0   | 1105 | 8   | 4   | 0   | 0   | 3   | 0   | 14  | 1   |
| 2   | 23  | 40   | 826 | 30  | 22  | 0   | 31  | 21  | 38  | 1   |
| 3   | 5   | 9    | 27  | 887 | 1   | 11  | 7   | 25  | 32  | 6   |
| 4   | 3   | 15   | 6   | 1   | 839 | 0   | 22  | 3   | 14  | 79  |
| 5   | 40  | 35   | 18  | 179 | 24  | 470 | 40  | 15  | 44  | 27  |
| 6   | 26  | 15   | 22  | 1   | 7   | 14  | 866 | 0   | 7   | 0   |
| 7   | 7   | 54   | 24  | 0   | 10  | 0   | 1   | 893 | 7   | 32  |
| 8   | 21  | 35   | 14  | 82  | 11  | 9   | 29  | 18  | 724 | 31  |
| 9   | 17  | 17   | 6   | 13  | 109 | 3   | 3   | 63  | 14  | 764 |
Table: caption

# Transfer learning

The model

To test the model ability to capture the basic elemn


# Robustness to noise

![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/robustness_to_noise.png)

# Adversarial learning

![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/robustness_to_adversarial_attacks.png)
