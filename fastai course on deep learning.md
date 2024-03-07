# fastai course on deep learning
created:: 2022-08-31 05:17
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/gnosis
kind:: #literature #coursework
status:: #status/seed
annotation:: 
parent:: [[∂ Learning Dashboard]], [[π Data Science Learning]]
***


**LESSON 1**

fastai has four applications:

- collaborative filtering
- computer vision
- natural language processing
- tabular data

Academic datasets are curated with the purpose of benchmarking. They help give baselines.

Fine grained classification: classifying between multiple similar categories.

the help function in python: help(function)

the doc function in python: doc(function) -- this gives you much more information about the function.

images are the same shape because GPUs need this in order to perform the operations in parallel, quickly. 224 x 224 is the most common size, and somehow leads to better results, for reasons yet to be explained.

in fastai, everything you work with will be in a DataBunch object. Contains two or three datasets: training, validation, test.

In deep learning, normalization of input data is almost always necessary.

in fastai, training is done with a "learner". For example, ConvLearner instantiates a convolutional neural network.

A particular kind of CNN, called a **resnet**, works really well for a lot of applications. Resnet 34 and Resnet 50. Smaller resnet will train faster.

Resnet has already been pretrained on millions of images. So we can download the model with the pretrained weights, so we don't have to start from scratch. This is transfer learning.

"One cycle learning" is dramatically better and faster training. There is a paper showing this in 2017.

If you don't know what to pass into a function, you can press Shift-Tab within the parentheses, and jupyter will show you the parameters that are required.

After training a model and verifying that it is working as expected, you can "unfreeze" it and train it some more for fine-tuning. Critically, unfreezing will unfreeze "all" layers of a model. When fine-tuning, however, it isn't always desirable to retrain every layer of the model. When you're retraining a pretrained model, it is important to understand that the earlier layers in the model will likely not need as much tuning. They will consist of low-level features that are most likely shared between the original dataset and your specific dataset. The deeper you go into the model, the more likely it is that the layer contains neurons that are specialized to the dataset. These higher-order features are the ones that need the most attention when retraining. You can address this by changing the learning rate based on the layer while training.

**LESSON 2**

In jupyter notebook, ??Function will give you the source code of the function.

In python, x@a means a matrix product

tensor means array (specifically, an array of regular shape)

rank means how many dimensions are there (a color image is typically a rank 3 tensor)

n=100

x = torch.ones(n,2)

x[:,0].uniform_(-1,1)

- This last command is going to replace the first column of ones with uniformly random numbers between -1 and 1. Note that when you have a function with an underscore after (e.g., "uniform_"), it means to not return the result, but to replace the indexed data in the object.

in fastai, if you're working with images, you will always load your data with the function

ImageDataBunch. You can name the images with the following methods:

.from_csv

.from_df

.from_folder

.from_lists

.from_name_func

.from_name_re