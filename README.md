# EEG-AI-Saliency

There seems to be only 3 sources with similar approach to visual saliency detection. We will explain the method used in each of them:

--------------------------------------------------------------------------

#### [Visual saliency detection guided by neural signals:](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ieeexplore.ieee.org/document/9320159&ved=2ahUKEwig94aDu-yHAxX0TKQEHTeMAf0QFnoECBMQAQ&usg=AOvVaw3ztGyfYLu_r6N34G0MAfA4)

Aim: capture correspondences between visual elements and neural activities, successfully generalizing to unseen images to identify their most salient regions.

- Inputs: EEG, original image
- Output: Image saliency map

Steps:
1. Preprocessing
2. Encoding the EEG and Image data into a common space. 
3. Training the encoders as a classification problem based on the definition of a compatibility function. The encoders are trained to maximize the similarity between the embeddings of corresponding images and EEGs. This aims to capture the relationship between what a person is seeing and their brain activity.
4. Analyzing the saliency score of each pixel. Once trained, these encoders analyze how the compatibility between the EEG and image embeddings changes when different regions of the image are suppressed. Regions whose removal causes significant variations in compatibility are considered salient, resulting in a visual saliency map.

![image](https://github.com/user-attachments/assets/f388e6f5-aed0-4ef4-af45-10e4fdab6f2b)

- For detailed Explanation visit [here](https://github.com/ab-mahdi/EEG-AI-Salience/blob/main/Guided%20by%20neural%20signals.md) 

------------------------------------------------------------
#### [Visual Saliency and Image Reconstruction from EEG Signals via an Effective Geometric Deep Network-Based Generative Adversarial Network:](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ieeexplore.ieee.org/document/9320159&ved=2ahUKEwig94aDu-yHAxX0TKQEHTeMAf0QFnoECBMQAQ&usg=AOvVaw3ztGyfYLu_r6N34G0MAfA4)

- Inputs: EEG, Ground truth obtained by eye tracking
- Output: Image saliency map and full reconstructed image

steps:
1. Turn EEG data into a graph representation
2. Extract the features of the graph using unsupervised method
3. Train the GAN model based on the extracted featues in the last step and ground truth input and obtain the image saliency map and full reconstructed image

![steps](https://github.com/user-attachments/assets/5aba1387-f8f6-43e5-943f-eed0f37e522f)

Let's take a deep dive into each step:

1. Preprocessing: The first part is obtaining the functional connectivity-based graph representation of the EEG channels. This is done by **Chebyshev graph convolutional layers**.

2. Unsupervised Feature Extraction: **Geometric Deep Network (GDN)** is an unsupervised method that takes the graph representation of EEG channels as input, extracts discriminative features from the graph to categorize the EEG signals into different visual patterns.

3. Training: **Generative Adversarial Network (GAN) for Saliency and Image Reconstruction:** The features extracted by the GDN are fed into the GAN. This GAN consists of a generator and a discriminator. The generator aims to create a saliency map from the EEG features, while the discriminator tries to distinguish between real saliency maps (derived from eye-tracking data) and those generated by the generator using **saliency metrics**. Through this adversarial process, the generator learns to produce accurate saliency maps from EEG signals.
* The trained GDN-GAN can then be fine-tuned to perform image reconstruction from the EEG signals, going beyond just saliency detection.

- For detailed Explanation visit [here](https://github.com/ab-mahdi/EEG-AI-Salience/blob/main/GDN-GAN) 

-----------------------------------


#### [Salient arithmetic data extraction from brain activity via an improved deep network:](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://ieeexplore.ieee.org/document/9320159&ved=2ahUKEwig94aDu-yHAxX0TKQEHTeMAf0QFnoECBMQAQ&usg=AOvVaw3ztGyfYLu_r6N34G0MAfA4)

Aim: To consider the Impact of arithmetic concepts on vision-related brain records.


- Inputs: EEG, Ground truth obtained by eye tracking
- Outputs: Image saliency map and full reconstructed image

Steps:
1. Normalize EEG data
2. Feed EEG data into 3 layers of one dimentional CNN's to extract the features and classify the data into 10 classes
3. Train the GAN model based on the output of the trained CNN. This GAN is trained to reconstruct both the salient parts of the MNIST digit images (using SALICON-generated images as ground truth) and the original MNIST digit images themselves. 
Proposes a Convolutional Neural Network-based Generative Adversarial Network (CNN-GAN) for identifying and extracting arithmetic content (digits 0-9) from visually evoked EEG signals. The method involves:
* The approach aims to extract not only the category of the visual stimulus but also reconstruct the image itself, particularly the salient regions, directly from EEG data. 

![image](https://github.com/user-attachments/assets/e049051b-4b7b-4c2d-bccd-863e318548b4)

Let's take a deep dive into each step:

1. Preprocessing: Normalization

2. EEG Classification:
   - A 14-channel time sample of the normalized EEG data is imposed directly as an input signal to a layers of one dimensional CNN to classify the brain signals into 10 different categories according to MNIST image digits.
   - The removal of feature vector extraction step results in decreasing the computational load.
   - The performance of the proposed CNN part is evaluated via the visually provoked 14-channel MindBigData recorded by David Vivancos, corresponding to images of 10 digits. An average accuracy of 95.4% is obtained for the CNN part for classification.

4. Training: **Generative Adversarial Network (GAN) for Saliency and Image Reconstruction:** The output of the CNN part is fed into the GAN. This GAN consists of a generator and a discriminator. The generator aims to create a saliency map from the EEG features, while the discriminator tries to distinguish between real saliency maps (derived from the MNIST dataset) and those generated by the generator using **saliency metrics**. Through this adversarial process, the generator learns to produce accurate saliency maps from EEG signals.
* The trained GDN-GAN can then be fine-tuned to perform image reconstruction from the EEG signals, going beyond just saliency detection.
- The performance of the proposed CNN-GAN is evaluated based on saliency metrics of SSIM and CC equal to 92.9% and 97.28%, respectively.
- For detailed Explanation visit [here](https://github.com/ab-mahdi/EEG-AI-Salience/blob/main/Salient%20arithmetic.md) 
