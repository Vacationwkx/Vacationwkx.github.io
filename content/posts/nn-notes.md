---
title: "NNN notes"
date: 2020-12-07T08:55:38+08:00
draft: false
categories: ComputerTech
tags:
  - machine-learning
---

In any case, you will need to get started with reading up on machine learning. i would suggest you first briefly start with neural networks, followed by deep convolutional neural networks just to get used to the idea of deep learning and subsequently focus on picking up reinforcement learning. As this machine learning field heavily requires you to be able to do programming, I would suggest that you try to implement the models you learnt and get familiar with the various packages of pytorch, tensorflow, fastai.

## Course

## CV

- [CS231n Winter 2016](https://www.youtube.com/watch?v=NfnWJUyUJYU)
- [Course | DEV290x | edX](https://courses.edx.org/courses/course-v1:Microsoft+DEV290x+1T2020a/course/)

## ML

- Coursera

## DL

### [Fundamental Recap](https://deeplizard.com/learn/video/gZmobeGL0Yg)

### [Fastai](https://course.fast.ai/)

- use Colab: fast set up, free | ahah, too slow, 👋🏻

- use GCP again

  - `gcloud compute config -ssh`  			

  - get error like:

    ```bash
    # error type 1
    External IP address was not found; defaulting to using IAP tunneling.
    ERROR: (gcloud.compute.start-iap-tunnel) Error while connecting [4033: u'not authorized'].
    kex_exchange_identification: Connection closed by remote host
    ERROR: (gcloud.compute.ssh) [/usr/bin/ssh] exited with return code [255].
    
    # error type 2
    ssh: connect to host 34.**.**.167 port 22: Resource temporarily unavailable
    ERROR: (gcloud.compute.ssh) [/usr/bin/ssh] exited with return code [255].
    ```

    try this :([quelle](https://stackoverflow.com/questions/26193535/error-gcloud-compute-ssh-usr-bin-ssh-exited-with-return-code-255#:~:text=If%20you%20have%20installed%20gcloud%20without%20sudo%2C%20you%20can%20omit%20sudo%20.&text=255%20is%20the%20interactive%20ssh,executed%20in%20the%20ssh%20session.&text=Go%20to%20your%20google%20cloud,tab%20and%20click%20on%20edit.))

    ![GCP](/general/gcp.png)

- use WSL in windows

  - 3 tips

  - can't get app-key, find [solution](https://stackoverflow.com/questions/46673717/gpg-cant-connect-to-the-agent-ipc-connect-call-failed)

    ```bash
    sudo apt remove gpg
    sudo apt-get update -y
    sudo apt-get install -y gnupg1
    ```

  - fresh hand following the tutorial, get cricked out because of ssh update after the buildung the instance. find solution [here](https://stackoverflow.com/questions/26193535/error-gcloud-compute-ssh-usr-bin-ssh-exited-with-return-code-255#:~:text=If%20you%20have%20installed%20gcloud%20without%20sudo%2C%20you%20can%20omit%20sudo%20.&text=255%20is%20the%20interactive%20ssh,executed%20in%20the%20ssh%20session.&text=Go%20to%20your%20google%20cloud,tab%20and%20click%20on%20edit.). MAKE SURE THE INSTANCE IS RUNNING!!!

### [Michael Nielsen](http://michaelnielsen.org/) 's guide 
[Neural networks and deep learning](http://neuralnetworksanddeeplearning.com/chap1.html)

- Tasks

    - [x] [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com/index.html)
    - [x] [What this book is about](http://neuralnetworksanddeeplearning.com/about.html)
    - [x] [On the exercises and problems](http://neuralnetworksanddeeplearning.com/exercises_and_problems.html)
    - [x] [Using neural nets to recognize handwritten digits](http://neuralnetworksanddeeplearning.com/chap1.html)
    - [x] [How the backpropagation algorithm works](http://neuralnetworksanddeeplearning.com/chap2.html) / 3
    - [x] [Improving the way neural networks learn](http://neuralnetworksanddeeplearning.com/chap3.html) - 3/6
    - [x] [A visual proof that neural nets can compute any function](http://neuralnetworksanddeeplearning.com/chap4.html) - 0/6
    - [x] [Why are deep neural networks hard to train?](http://neuralnetworksanddeeplearning.com/chap5.html) - 0/4

    - give up here since of the old code
    - [Deep learning](http://neuralnetworksanddeeplearning.com/chap6.html) - 0/6
    - [Appendix: Is there a *simple* algorithm for intelligence?](http://neuralnetworksanddeeplearning.com/sai.html)
    - [Acknowledgements](http://neuralnetworksanddeeplearning.com/acknowledgements.html)

- [Frequently Asked Questions](http://neuralnetworksanddeeplearning.com/faq.html)

### Hyper Parameter Choosing

[Hyperopt Documentation](http://hyperopt.github.io/hyperopt/)

[Random search for hyper-parameter optimization](https://dl.acm.org/doi/10.5555/2188385.2188395)

[Practical recommendations for gradient-based training of deep architectures](https://arxiv.org/abs/1206.5533)

## CNN

- A great [intro](https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53)
- Tips from stanford
    - [Tip 1](https://cs231n.github.io/neural-networks-1/)
    - [Tip 2](https://cs231n.github.io/neural-networks-2/)
    - [Tip 3](https://cs231n.github.io/neural-networks-3/)
- Loss Function
    - [keras](https://neptune.ai/blog/keras-loss-functions)
    - [choose](https://towardsdatascience.com/a-guide-to-an-efficient-way-to-build-neural-network-architectures-part-i-hyper-parameter-8129009f131b)
- [GIF](https://github.com/vdumoulin/conv_arithmetic) for better understanding
- [CNN Architecture](https://medium.com/@RaghavPrabhu/cnn-architectures-lenet-alexnet-vgg-googlenet-and-resnet-7c81c017b848#:~:text=VGG%2D16%20is%20a%20simpler,2%20with%20stride%20of%202.&text=The%20winner%20of%20ILSVRC%202014,also%20known%20as%20Inception%20Module.)
- [LeNet - 5](https://medium.com/towards-artificial-intelligence/the-architecture-implementation-of-lenet-5-eef03a68d1f7)

### Softmax or Sigmoid

maybe [answer](https://stats.stackexchange.com/questions/233658/softmax-vs-sigmoid-function-in-logistic-classifier)

### Loss Analysis

[Validation Loss](https://stats.stackexchange.com/questions/258166/good-accuracy-despite-high-loss-value/281651#281651)

[Nvidia-smi](https://www.andrey-melentyev.com/monitoring-gpus.html#:~:text=exceeding%20the%20capacity.-,Disp.,stats%20for%20a%20particular%20device.)