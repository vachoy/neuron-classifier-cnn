## Neuron Classifier CNN

### Background-
    This is, as the title says, a convolutional neural network that attempts to classify
    different types of pyramidal neurons. I chose to create this because I am a neuroscience 
    and behavior major and I hope to use machine learning to aid neuroscience research in
    graduate school and beyond. A neural network such as this one (when fully optimized)
    could help distinguish types of neurons between different species.
    The Neuron Classifier CNN follows an architecture using the tensorflow layers module
    similar to the kind used to evaluate the popular MNIST dataset. Methods can be broken 
    down into 3 main categories for easier understanding: data preprocessing, the model
    itself, and training/output. Each of these are detailed below.

### Data Preprocessing-
    Each neuron image was originally obtained from Neuromorpho.org. They are of five
    distinct categories:
        0. human, neocortex
        1. mouse, hippocampus
        2. rat, hippocampus
        3. rat, neocortex
        4. mouse, neocortex
    All neurons are pyramidal and originate from either the neocortex or hippocampus of their
    respective species. To prepare for upload to the neural network, each image was first
    resized to conform to the 90 x 72 image size standard for the network. Each image was then
    converted to grayscale because for the purposes of this network color channels have no
    significant influence on neuronal type. From there, the image was converted into a numpy
    array by representing each pixel as a number from 0-255 where each number was a representation
    of a particular shade of gray (0 = black, 255 = white). The array was then converted from
    a square shape to one long row of values. Each row was then uploaded to a csv file and labeled
    from 0-4 depending on the neuron's type. Each class had 100 training images, 20 validation
    images, and 35 test images, for a total of 500 training, 100 validation, and 175 test images.

### The Model-
    
