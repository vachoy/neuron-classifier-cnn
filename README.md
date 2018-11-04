## Neuron Classifier CNN

*LINK TO GOOGLE COLAB NOTEBOOK WITH MODEL*
https://colab.research.google.com/drive/1llOyxxIETn_X2WLkvHSKWx_414LdWVm1

### Background-
    A convolutional neural network that attempts to classify different types of pyramidal 
    neurons. I chose to create this because I am a neuroscience and behavior major and hope 
    to use machine learning to aid neuroscience research in graduate school and beyond. A 
    neural network such as this one (when fully optimized) could help distinguish types of 
    neurons between different species.
    The Neuron Classifier CNN follows an architecture using the tensorflow layers module
    similar to the kind used to evaluate the popular MNIST dataset. Methods can be broken 
    down into 3 main categories for easier understanding: data preprocessing, the model
    itself, and training/output.

### Data Preprocessing-
    Each neuron image was originally obtained from Neuromorpho.org. They are of three
    distinct categories:
        0. human
        1. mouse
        2. rat
    All neurons are pyramidal and originate from either the neocortex or hippocampus of their
    respective species. To prepare for upload to the neural network, each image was first
    resized to conform to the 90 x 72 image size standard for the network. Each image was then
    converted to grayscale because for the purposes of this network color channels have no
    significant influence on neuronal type. From there, the image was converted into a numpy
    array by representing each pixel as a number from 0-255 where each number was a representation
    of a particular shade of gray (0 = black, 255 = white). The array was then converted from
    a square shape to one long row of values. Each row was then uploaded to a csv file and labeled
    from 0-2 depending on the neuron's type.

### The Model-
    Please see code comments for line-by-line explanations of how the code works, as this is an
    overview of the model's general structure.
    The`tf.layers` used in this CNN are as follows:
    - Input Layer
        Reshapes the input to make sure it conforms to the size standards.
    - Convolutional Layer
        Applies 64 5 x 5 filters using a ReLU activation function.
    - Pool Layer
        Applies max pooling to help control overfitting, using the standard 2 x 2 filter with a
        stride of 2.
    - Convolutional Layer 2
        Applies 128 5 x 5 filters using a ReLU activation function.
    - Pool Layer 2
        Same as previous pool layer.
    - Dense Layer
        Layer that performs classification using 1024 neurons and ReLU activation function. Also
        apply dropout regularization here because of use of the ReLU function. Dropout rate is 40%.
    - Logits Layer
        Second dense layer with 3 neurons (one for each class). Returns the raw values of the
        predictions.
    --
    Predictions
        Utilizes `tf.argmax` to find the class with the highest raw probability score. Then
        uses a softmax activation function to generate a prediction from output of the logits layer.
    Loss
        Loss is calculated using cross-entropy, which is a common function used for image
        classification. Also creates one-hot encoding for the three classes.
    Training
        This network uses stochastic gradient descent for the optimization algorithm, via
        `tf.train.GradientDescentOptimizer` and a learning rate of 0.003.

### Training/Output
    Data is loaded into the model as pandas DataFrames which are then converted to numpy arrays.
    Training is done in batches of 45 examples and probabilities are logged as output every 100
    steps. The model trains for a total of 10000 steps at a time. The model is then evaluated
    on the test data and total loss, accuracy, and number of global steps taken is printed.
    
### Results
    In its current form, the model classifies neurons with approximately 55% accuracy. The model
    is still a work in progress and hyperparameters may still be able to be tuned to aid
    accuracy (without overfitting). The model's layer structure can also still be experimented
    with and this repository will be updated accordingly if a more accurate structure is found
    in the future. It would also be interesting to see how well the model extrapolates to images
    of neurons directly from stained slides, given that the NeuroMorpho images are digital
    reconstructions of actual neurons. The network would also likely benefit from more training 
    examples per class, which is an avenue that will be explored in the future.
    
### How to Run the Code
    The network is all located in one file for ease of use. Run each cell from top to
    bottom. To input the datasets, choose your train/test sets when prompted after running the second
    cell. The csv files used while creating this network are also available in the repository. The third cell
    is provided to verify a successful upload, and will print the names of the files and their length
    in bytes. In the fourth cell, change the names of the files 'simpletraindata.csv' and 'simplevaldata.csv'
    if you are uploading your own files. Otherwise there is no need to change them as long as you
    upload the corresponding csv files with the same name. After that, all you need to do is continue
    running each cell from top to bottom. The last cell, titled with `# load data`, will run for a
    period of time while the model makes predictions. Every 100 training steps, TensorFlow will output
    the network's progress so you can monitor it.
