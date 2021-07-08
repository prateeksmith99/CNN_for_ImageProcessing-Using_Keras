# CNN_for_ImageProcessing-Using_Keras
Image classification is the process of segmenting images into different categories based on their features. A feature could be the edges in an image, the pixel intensity, the change in pixel values, and many more

#### What is Image Classification?<hr>
* Image classification is the process of segmenting images into different categories based on their features. A feature could be the edges in an image, the pixel intensity, the change in pixel values, and many more.A same individual person however varies when compared across features like the color of the image, position of the face, the background color, color of the shirt, and many more. 
* The biggest challenge when working with images is the uncertainty of these features. To the human eye, it looks all the same, however, when converted to data you may not find a specific pattern across these images easily.

* An image consists of the smallest indivisible segments called pixels and every pixel has a strength often known as the pixel intensity. Whenever we study a digital image, it usually comes with three color channels, i.e. the Red-Green-Blue channels, popularly known as the “RGB” values. Why RGB? Because it has been seen that a combination of these three can produce all possible color pallets. Whenever we work with a color image, the image is made up of multiple pixels with every pixel consisting of three different values for the RGB channels
<br><br><br>
#### Understanding Image Dimensions<hr>
    image.shape
    (400, 400, 3)
    Note:

The Shape of the image is 400 x 408 x 3 where 400 represents the height, 400 the width and 3 represents the number of color channels. When we say 400 x 400 it means we have 1,60,000 pixels in the data and every pixel has a R-G-B value hence 3 color channels

    image[0][0]
    array([193, 159, 113], dtype=uint8)
    Note:
          image [0][0] provides us with the pixel and 193, 159, 113 are the R-G-B values
          
<br><br>        
#### The output of gray.shape is 400 x 400. What we see right now is an image consisting of 1,60,000 odd pixels but consists of one channel only.

When we try and covert the pixel values from the grayscale image into a tabular form this is what we observe.
    import numpy as np
    data = np.array(gray)
    flattened = data.flatten()
    flattened.shape

        Output: (192600,)
We have the grayscale value for all 192,600 pixels in the form of an array.

<br>
flattened
array([149, 147, 160, ..., 156, 137,  53], dtype=uint8)
Note a grayscale value can lie between 0 to 255, 0 signifies black and 255 signifies white.

* Now if we take multiple such images and try and label them as different individuals we can do it by analyzing the pixel values and looking for patterns in them. However, the challenge here is that since the background, the color scale, the clothing, etc. vary from image to image, it is hard to find patterns by analyzing the pixel values alone. Hence we might require a more advanced technique that can detect these edges or find the underlying pattern of different features in the face using which these images can be labeled or classified. This where a more advanced technique like CNN comes into the picture.

<br><br><br>
#### What is CNN?<hr>

* CNN or the convolutional neural network (CNN) is a class of deep learning neural networks. In short think of CNN as a machine learning algorithm that can take in an input image, assign importance (learnable weights and biases) to various aspects/objects in the image, and be able to differentiate one from the other.

* CNN works by extracting features from the images. Any CNN consists of the following:
  1 - The input layer which is a grayscale image
  2 - The Output layer which is a binary or multi-class labels
  3 - Hidden layers consisting of convolution layers, ReLU (rectified linear unit) layers, the pooling layers, and a fully connected Neural Network

It is very important to understand that ANN or Artificial Neural Networks, made up of multiple neurons is not capable of extracting features from the image. This is where a combination of convolution and pooling layers comes into the picture. Similarly, the convolution and pooling layers can’t perform classification hence we need a fully connected Neural Network.

Before we jump into the concepts further let’s try and understand these individual segments separately.
![Test_Image](https://miro.medium.com/max/2000/0*BVil_XCudTACe0vD.jpeg)

<br>
<strong>Why grayscale and not RGB/Color Images?</strong>

![Test_Image](https://miro.medium.com/max/688/0*6lrbxTDUty2RkGVB.png)

* The challenge with images having multiple color channels is that we have huge volumes of data to work with which makes the process computationally intensive. In other worlds think of it like a complicated process where the Neural Network or any machine learning algorithm has to work with three different data (R-G-B values in this case) to extract features of the images and classify them into their appropriate categories.
The role of CNN is to reduce the images into a form that is easier to process, without losing features critical towards a good prediction. This is important when we need to make the algorithm scalable to massive datasets.
<br><br>

<strong>What are convolutions?</strong>

* We understand that the training data consists of grayscale images which will be an input to the convolution layer to extract features. The convolution layer consists of one or more Kernels with different weights that are used to extract features from the input image. Say in the example above we are working with a Kernel (K) of size 3 x 3 x 1 (x 1 because we have one color channel in the input image), having weights outlined below.

* When we slide the Kernel over the input image (say the values in the input image are grayscale intensities) based on the weights of the Kernel we end up calculating features for different pixels based on their surrounding/neighboring pixel values. E.g. when the Kernel is applied on the image for the first time as illustrated in Figure 5 below we get a feature value equal to 4 in the convolved feature matrix as shown below.

![Test_Image](https://miro.medium.com/max/875/1*J-hFT0lYDiYBNi8M4_n2OA.png)

* If we observe Figure 4 carefully we will see that the kernel shifts 9 times across image. This process is called Stride. When we use a stride value of 1 (Non-Strided) operation we need 9 iterations to cover the entire image. The CNN learns the weights of these Kernels on its own. The result of this operation is a feature map that basically detects features from the images rather than looking into every single pixel value.

* Image features, such as edges and interest points, provide rich information on the image content. They correspond to local regions in the image and are fundamental in many applications in image analysis: recognition, matching, reconstruction, etc. Image features yield two different types of problem: the detection of the area of interest in the image, typically contours, and the description of local regions in the image, typically for matching in different images, (Image features. (n.d.))


    # 3x3 array for edge detection
    mat_y = np.array([[ -1, -2, -1], 
                    [ 0, 0, 0], 
                     [ 1, 2, 1]])
    mat_x = np.array([[ -1, 0, 1], 
                    [ 0, 0, 0], 
                       [ 1, 2, 1]])
  
    filtered_image = cv2.filter2D(gray, -1, mat_y)
    plt.imshow(filtered_image, cmap='gray')
    plt.show()
<br>

![Test_Image](https://miro.medium.com/max/498/1*DXO0ADta5SmnOanklrw4og.png)
