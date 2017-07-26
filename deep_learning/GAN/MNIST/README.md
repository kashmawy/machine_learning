# MNIST Generative Adversarial Networks

This project is aimed at exploring Generative Adversial Networks for MNIST.
The main components are:

1. Discriminator: The discriminator job is to take a 28x28x1 image as input and give the probability that the image is a digit. 
2. Generator: The generator job is to generate a 28x28x1 image that resemeble MNIST image.
3. Adversarial: The adversarial network consists of the generator followed by the discriminator.

The following shows the discriminator architecture:

Input is: 28x28x1

| Layer (type)                                     | Size                     |
| ------------------------------------------------ |:------------------------:|
| 5x5 Convolution with stride of 2                 | Batchx14x14x64           |
| Leaky RELU with alpha of 0.2                     | SAME                     |
| Dropout with 0.4 probability                     | SAME                     |
| 5x5 Convolution with stride of 2                 | Batchx7x7x128            |
| Leaky RELU with alpha of 0.2                     | SAME                     |
| Dropout with 0.4 probability                     | SAME                     |
| 5x5 Convolution with stride of 2                 | Batchx4x4x256            |
| Leaky RELU with alpha of 0.2                     | SAME                     |
| Dropout with 0.4 probability                     | SAME                     |
| 5x5 Convolution with stride of 2                 | Batchx4x4x512            |
| Leaky RELU with alpha of 0.2                     | SAME                     |
| Dropout with 0.4 probability                     | SAME                     |
| Reshape to 8192                                  | Batchx8192               |
| Fully Connected Layer                            | Batchx1                  |
| Sigmoid activation                               | SAME                     |

Output is the probability that 28x28x1 is a digit and it is between 0.0 and 1.0

The following shows the generator architecture:

Input is: 100

| Layer (type)                                     | Size                            |
| ------------------------------------------------ |:-------------------------------:|
| Fully Connected Layer                            | Batchx12544 (7x7x(64+64+64+64)) |
| Batch Normalization                              | SAME                            |
| RELU                                             | SAME                            |
| Reshape                                          | 7x7x(64+64+64+64)               |
| Dropout with 0.4 probability                     | SAME                            |
| UpSampling2D                                     | 14x14x(64+64+64+64)             |
| Conv2DTranspose with 128 filters and SAME padding| 14x14x(64+64)                   |
| BatchNormalization                               | SAME                            |
| RELU activation                                  | SAME                            |
| UpSampling2D                                     | 28x28x(64+64)                   |
| Conv2DTranspose with 64 filters and SAME padding | 28x28x(64)                      |
| Batch Normalization                              | SAME                            |
| RELU activation                                  | SAME                            |
| Conv2D Tranpose with 32 filters and SAME padding | 28x28x32                        |
| Batch Normalization                              | SAME                            |
| RELU activation                                  | SAME                            |
| Conv2D Tranpose with 1 filter and SAME padding   | 28x28x1                         |
| Sigmoid activation                               | SAME                            |

Output is 28x28x1 which the generator will try to make to resemble a digit.



