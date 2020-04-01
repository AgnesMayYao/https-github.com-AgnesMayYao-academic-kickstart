+++
title = "Sound Classification"
subtitle = "Experience of Infant Fuss/Cry Classification"

date = 2020-03-31T00:00:00
lastmod = 2020-03-31T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["admin"]

tags = ["audio", "deep learning"]
summary = "my experience of using different features, models to classify different sounds"

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["internal-project"]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  # caption = "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""

  # Show image only in page previews?
  preview_only = false

# Set captions for image gallery.


+++
## Common Audio Classification Procedure
1. Preprocessing (filtering, smoothing, ..)
2. Feature Engineering (accoustic features, spectrograms, audio encoders, combination, ..)
3. Model training (classic machine learning models, CNNs, RNNs, ..)
4. Postprocessing(smoothing)


## Preprocessing
1. Know your data, examine your data
  * if you give trash to your ML algorithm, it will give back trash.
  * Remove irrelevant noises (eg. silence, beginning, ending,..). Give fewer confusing noises to your model and help your model to focus on the necessary.
2. Filtering ([scipy.signal](https://docs.scipy.org/doc/scipy-0.16.1/reference/signal.html))
  * High pass filter, low pass filter, bandpass filter
  * Eg. My project focuses on infant noises and infants have F0 > 400 Hz. So any sound doesn't have high energy at frequencies > 400 Hz should be excluded.
3. Smoothing ([scipy.signal](https://docs.scipy.org/doc/scipy-0.16.1/reference/signal.html))
  * reduce noise from white noises
  * median filter, Savitzky-Golay filter, ...
4. Voice Activity Detection
  * WebRTC Voice Activity Detector (VAD) (open source), CMU Sphinx, ...
  

## Feature Engineering
1. Accoustic features
  * Fundamental Frequency / Pitch, Zero Crossing Rate, MFCCs, Harmonic-to-noise Ratio, .... (commonly used)
  * libraries: librosa (easy to use), [pyAudioAnalysis](https://github.com/tyiannak/pyAudioAnalysis) (easy to use), yaafe, openSMILE, Matlab Audio Toolbox
  * You can try openSMILE to extract 6000+ features and then PCA 
  * **I suggest:** plot features with ground truth and manually select features that your want. No free lunch, and features work for other applications won't necessarily work for you. Learn your features so that you know why it works and why it doesn't.
2. Spectrogram
  * Energy at every frequency vs. time
  * Really shows a pattern. Used in my research
3. Other features
  * Bag-of-Audio-Words: One codebook is learnt for 65 LLDs and one for 65 delta LLDs. 
  * AUDEEP: Unsupervised representation learning with recurrent sequence-to-sequence autoencoders
4. Combination of different features


  
## Model Training
1. Classic Machine learning models (tune your parameters)
2. Deep learning
  * CNNs: good for spectrograms
  * RNNs: use it when your data show a strong sequential pattern, eg. infant fussing always leads to infant crying (which is wrong). 
3. CNNs + RNNs and other advanced/complicated/deeper models
  * Do the basics first. Make sure your preprocessing, features are really working. Though temptating, don't do this unless you really have tried everything else.
  * Learn these complicated models before you try blindly. Know how they work and where they work. 
  * Advanced/complicated/deeper models can have more parameters/hyperparameters, which is harder to tune and takes longer time to train. You don't have a huge dataset/supersupercomputer for reallife audio...
4. Unbalanced dataset
  * upsampling, downsampling
  * SMOTE (super long time for spectrograms)
  * [imbalanced-learn library](https://imbalanced-learn.readthedocs.io/en/stable/index.html)
  
## Postprocessing
1. Smoothing
  * Remove isolated predictions in the middle of nowhere
  * Combine neighbouring predictions


