---
title: Cognition Computation
author: Giulio Umbrella
---

# Convolutional autoencoder

![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/orginal_reconstructed.png)

![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/conv_autoencoder_firstlayer_fiiters.png)


# Linear read-out

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


![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/dendogram_complete.png)

# Transfer learning

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


# Robustness to noise

![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/robustness_to_noise.png)

# Adversarial learning

![test](/Users/gumbrella/UNIPD/LM/AA2122/PrimoSemestre/CC/Progetto/images/robustness_to_adversarial_attacks.png)
