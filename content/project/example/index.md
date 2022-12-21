---
title: (CV - Semantic Segmentation) Brain Tumor Segmentation Task Using U-Net
summary: Participated in the Imperial College of Science and Technology’s Data Science Summer School, complete a brain tumor segmentation task using U-Net. Use Keras to load datasets and do data preprocessing and augmentation on images, build U-Net, Res-UNet and U^2-Net networks, optimize using the dice loss.
tags:
  - Research
date: '2020-08-27T00:00:00Z'

# Optional external URL for project (replaces project detail page).
# external_link: 'https://github.com/ididChan/BrainTumorDetector/'

image:
  caption: Overall Architecture of Res-Unet
  focal_point: Smart

links:
#  - icon: twitter
#    icon_pack: fab
#    name: Follow
#    url: https://twitter.com/georgecushen
url_code: 'https://github.com/ididChan/BrainTumorDetector/'
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
#slides: example
---

Medical imaging technology has played an important role in the early diagnosis
and efficacy evaluation of diseases, especially in the field of tumor detection, which
has helped many patients. In tumor detection, the most used is magnetic resonance
imaging (MRI). Due to the high complexity of human brain tissue, a large amount of
data makes it difficult to segment images manually, which delays the optimal treatment
time for patients. Therefore, after deep learning methods have brought rapid
development in the field of computer vision, people have gradually begun to combine
artificial intelligence with medical image recognition, and many convolutional neural
network models have been proposed. These models provide doctors with a lot of help
and provide a more adequate scientific basis for medical diagnosis, treatment, and evaluation.

**FCN**

The traditional CNN-based segmentation method is a relatively mature model but
there are some problems[2]. First, a large amount of storage space is required, and the
increase in the number and size of sliding windows will result in a very large storage
space. Second, there is a large degree of repetition. Repeated calculations for a pixel
result in slow calculation speed and low efficiency of the model. Third, the size of the
pixel block will limit the size of the receptive field, so that only some local features can
be extracted, which ultimately results in the limitation of classification performance.
Therefore, a fully convolutional neural network is proposed.

There are three main differences between Fully Convolutional Neural Networks
(FCN) and traditional Convolutional Neural Networks (CNN).
The first is to convert the fully connected layer into a convolutional layer, and use
the deconvolution method for up sampling, which solves the problem of the effect of
convolution and pooling operations on the image size.
Secondly, use the transfer learning method for finetune. Some common classification
networks such as GoogleNet, VGG, etc. can be reinterpreted as FCN.
Thirdly, to ensure accuracy and robustness, a skip structure that combines the results
of different depth layers.

**U-Net**

U-Net is essentially based on FCN, and it has some improvements on FCN. U-Net
contains two serial paths, one is the contracting path for extracting image features and
capturing image content, and the other is the expanding path for precise positioning[3].
U-Net retains a large number of feature channels during the up-sampling process. It
superimposes the feature maps of the same size of the contracting path and the expanding
path, and then continue the convolution and up sampling work, which effectively
reduces the loss of image information on the compression path.

In addition, the classic convolutional network in skip connection needs to be trained
with a large number of labeled training samples, but in biomedical image processing,
due to the small amount of data, there is not enough data set for training, so data enhancement
is required. Commonly used methods to increase training samples include
rotating images, mirroring transformations, etc. In the article, image augmentation
with elastic deformation is used. At the same time, due to the vitality of human cells
and tissues, irregular distortions always occur at the boundaries of cell tissues, so data
enhancement is very necessary. The article uses sampling from a Gaussian distribution
with a 10-pixel standard deviation and uses bicubic interpolation to calculate the displacement
of each pixel. Finally, place the drop-out layer at the end of the contracting
path to further increase data.

**Res-Unet**

To further optimize and obtain more accurate results, Res-UNet was tried to be
adopted. The model is based on the original U-Net model and adds a weighted attention
mechanism. After adding skip connection, the details of the image can be
extracted better, and the accuracy rate has been further improved. In addition, we also
used Cyclic LR training method and got better results. At the same time, we add
some batch normalization layers in between, which can accelerate the training process
and avoid over-fitting.
