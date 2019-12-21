---
title: Readings on Electroencephalography
layout: note
description: Notes on my readings in research papers containing Electroencephalography (EEG)
---

<table>
<thead><th>Paper</th><th>Key Ideas</th></thead>
<tbody>

<tr>
  <td>[2019]
  <a href="https://iopscience.iop.org/article/10.1088/1741-2552/ab405f/meta">
    HS-CNN: A CNN with Hybrid Convolution Scale for EEG Motor Imagery Classification
  </a></td>
  <td>
    <ul>
        <li>issues:
            <ul>
                <li>classification accuracy differ significantly from subject to subject or from time to time for the same subject</li>
                <li>CNN requires large amount of training data, but challenging as acquiring such data require subject to concentrate</li>
                <li>best kernel size varies from subject to subject</li>
                <li>different "band" with different Hz range, differs for different motor task</li>
            </ul>
        </li>
        <li>hybrid-scale CNN with data augmentation to address issues
            <ul>
                <li>3 different kernel size for each frequency band to extract time features</li>
                <li>data augmentation, segmentation crop, for same person same class do random swap to generate new data</li>
            </ul>
        </li>
        <li>dropout 0.8 and 0.01 L2 regularisation</li>
    </ul>
  </td>
</tr>

<tr>
  <td>[2017]
  <a href="http://www.ncbi.nlm.nih.gov.remotexs.ntu.edu.sg/pubmed/27900952">
    A novel deep learning approach for classification of EEG motor imagery signals
  </a></td>
  <td>
    <ul>
        <li>combine CNN and stacked autoencoders for classification</li>
        <li>instead of 2D filtering, used 1D (same height as the input) to handle vertical location</li>
        <li>autoencoders to learn features in hidden layer</li>
        <li>combine CNN and SAE to make it more robust to high noise low signal, and to vary among trials</li>
        <li>measure accuracy by subject, 10 fold cross validation</li>
        <li>use Kappa to measure accuracy, by removing effect from random classification</li>
    </ul>
  </td>
</tr>

<tr>
  <td>[2016]
  <a href="https://iopscience.iop.org/article/10.1088/1741-2552/aace8c/meta">
    EEGNet: a compact convolutional neural network for EEG-based brain–computer interfaces
  </a></td>
  <td>
    <ul>
        <li>evaluate on 4 dataset</li>
        <li>Depthwise Convolution of size (C,1) to learn a spatial filter. provides a direct way to learn spatial filters for each temporal filter, thus enabling the efficient extraction of frequency-specific spatial filters</li>
        <li>Separable Convolution, reduce number of parameters and decouple relationship across feature maps</li>
        <li>dropout: 0.25 for subject, 0.5 for cross subject</li>
    </ul>
  </td>
</tr>

<tr>
  <td>[2016]
  <a href="https://pdfs.semanticscholar.org/252d/90a65387b37ab5aba3a158c7bb400b6d4bac.pdf">
    EEG based eye state classification using deep belief network and stacked autoencoder
  </a></td>
  <td>
    <ul>
        <li>implement Deep Belief Network and Stacked AutoEncoder to predict eye state using EEG</li>
        <li>internal and external interference can affect EEG signals, external such as power equipments and environment, internal such as eye movements, muscle and respiratory</li>
        <li>use Deep Belief Network for classification</li>
        <li>use Stacked AutoEncoder to reconstruct input to extract features</li>
        <li>used Discrete Wavelet Transform to extract features from EEG signals</li>
    </ul>
  </td>
</tr>

<tr>
  <td>[2015]
  <a href="https://arxiv.org/abs/1511.06448">
    Learning representations from EEG with deep recurrent-convolutional neural networks
  </a></td>
  <td>
    <ul>
        <li>issues:
            <ul>
                <li>invariant inter- and intra- subject differences</li>
                <li>noise in EEG data collection</li>
                <li>existing work does not preserve EEG data within space, time and frequency</li>
            </ul>
        </li>
        <li>rather than representing EEG features as vectors, transform into multi-dimensional tensor, like a movie</li>
        <li>CNN to extract each frame, to extract spatial and spectral invariant representation</li>
        <li>LSTM to extract temporal patterns in frame sequence</li>
        <li>a single image has 3 channels for each of the 3 prominent frequency bands</li>
        <li>image generated from EEG using Fast Fourier Transform</li>
    </ul>
  </td>
</tr>


</tbody>
</table>



# Survey

[Deep learning-based electroencephalography analysis: a systematic review](https://iopscience.iop.org/article/10.1088/1741-2552/ab260c/meta)

stats/numbers
- research on EEG applications are relatively small, compared to other deep learning applications
- about 41% uses CNN, about 14% uses RNN, 15$ uses auto-encoders
- 54% uses public dataset, 42% reported results from private recording, 4% use both
- 19% have code available, 7% have code and uses public available data
- half of research used dataset contained fewer than 13 subjects
- vary number of electrodes in studies
- sampling rate also varied, 50% uses 250 Hz or less, highest 5000 Hz
- very few papers (3) explored impact of data augmentation
- DNN with 7 layers performed better than shallow (2-4) and deeper (>10)
- 47% did not report on optimiser, 30% uses Adam, usage of Adam is increasing

research on EEG
- classification sleep staging, seizure detection, brain computer interfaces
- improvement on feature extraction or visualising train models
- data augmentation, generation images

challenges of EEG
- low signal to noise ratio, need to filter noise to extract true brain activity
- non-stationary signal, generalize poorly even on same individual
- high inter-subject variability, physiological differences between individuals, 38% vs. 75% accuracy on unseen and seen subjects
- manually annotating windows of few seconds of signals requires a lot of time

DNN can help in these areas:
- learn and extract features from raw or minimally preprocessed data
- reduce domain specific processing and feature extraction
- features might be more expressive than those engineered by humans
- might be able to do transfer learning, on different analysis tasks

but EEG has issues with DNN:
- DNN needs large dataset, current lack of data
- EEG's low signal to noise ratio make it very difficult for DNN to learn (compared to CV and NLP)
- no standards performance metrics for reporting methodology
- lack of baseline performance

preprocessing
- downsampling
- band-pass filtering
- windowing

findings
- shallower architectures preferred when limited amount of data available
- data augmentation is useful when limited data
- overlapping is useful, but no consensus on best overlapping percentage
- no clear preference to use fourier filter extracted features or using raw EEG, but using raw EEG is upward trend, as CNN is effective for processing time series
- many different tasks, many different dataset were used, often private or limited, lack of reproducibility, low accountability

recommendation for future EEG studies to include
- describe architecture of model
- describe data used, number of subjects, number of samples, data augmentations
- compare performance against public dataset
- state and improve from existing state of the art baselines
- share internal recordings
- share experiment code, include hyperparameters, models file for re-run 