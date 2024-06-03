# Fashion MNIST CNN for trainsfer-learning

## Goal
All pre-trained models broadly available in the internet are trained on three channel images. You can adapt them to gray images problems, but it isn't efficient, so goal of this project is to create small lightweight model that can be used in transfer-learning scenario, without waisting resources.  

## Methodology
Following things where tried: 
1. Pure CNN architecture exploration:
   - Network shape (amount of layers, filters etc.)
   - Batch Normalization impact
   - Classification architecture: dense classifier vs global average pooling vs combination of both
   - Regularization methods like dropout, spatial dropout and data augmentation
   - 0ptimizers - Adam, Nadam, AdamW
   - Activation functions - relu, selu, gelu
2. Automatic fine-tuning with keras Tuners
   - Architecture shape exploration with hyperband tuner
   - Optimizer hyperparameters tuning with bayesian optimization
3. Unsupervised learning for initial feature learning
   - Encoder from auto-encoder network used as a base of classifier
   - VAE - Encoder for feature learning + whole network for data augmentation (in progress)

## Results
- Best acc achieved (acc=93%; params<400k, epoch=40):  
  `global_avg_model` from [01_cnn_mnist notebook](notebooks/01_cnn_mnist.ipynb).
- Fastest learner (acc=90%; params<400k; epoch=3)  
  `only_optimizer` from [02_tuner notebook](notebooks/02_tuner.ipynb)
- Smallest (acc=90%; params<20k; epochs=30)  
  `pure_dense` from [03_autoencoder notebook](notebooks/03_autoencoder.ipynb)


## Limitation
Because of training data nature (shape 28x28x1) model cannot be used in cases where distinguishing details is crucial for classification. It is only suited for cases where shapes and colors of thing will be enough to classify object.