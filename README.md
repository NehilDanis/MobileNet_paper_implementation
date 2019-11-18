# MobileNet_paper_implementation
The MobileNet paper implemented for Malaria detection.

The dataset which is going to be used for training validation and testing processes are taken from followig website, under the link of cell_images.zip. 

Please to try the application download the dataset and put it into the directory that you are working on and run the following command.

$ sudo unzip cell_images.zip
$ sudo chown {user_name}:{user_name} -R cell_images


# QUICK INTRO TO SPATIAL SEPARABLE AND DEPTHWISE SEPARABLE CONVOLUTIONS

Basically, in the spatial convolutions, the aim is two divide the convolution filter into two parts that give the same effect after applying them sequentially as only applying the single filter.

[[5, 10, 15], [10, 20, 30], [15, 30, 45]] = [[5], [10], [15]] . [[1, 2, 3]]

Instead of applying the 3 by 3 filter we can apply first the 3 by 1 filter and get an intermediate image and then we can apply the second 1 by 3 filter. In the end, we will get the same result by doing less operations. This makes the convolution more efficient.

However the problem with the spatial separable convolution is that you won't be able to find two subfilters whose multiiplication gives you the bigger filter. So sometimes you won't be able to separate your matrix into two.


In the case of depthwise convolution, the convolution process will be divided into two distinct parts, which are depthwise and pointwise convolution. 

## Part 1 - Depthwise Convolution

Let's consider we have 12x12x3 input image and we have 256 5x5x3 filters. In the normal convolution the result would be 8x8x256. But in depthwise convolution we basically consider each channel of the filter and the image seperately. Also we will only use one kernel in this part of the process. 

So 12x12x3 image and 1 5x5x3 filter; the output will be 8x8x3.

## Part 2 - Pointwise Convolution

1d convolution is called pointwise convolution. Basicall it is for changing the depth without changing the spatial size of the output. As we already specified we want to have 256 filters, but in the first part of the depthwise convolution we only used one filter and get the output size 8x8x3.

Let's assume we have 256 1x1x3 filter. If we apply it to the output of part one, we will get 8x8x256 as a result.



## Why Mobile-Net uses depthwise separable filters?

In the end we will get the same result as if we apply a regular convolution. But the number of operations that we need to handle is much less. 

Let's make a small calculation!
In case of regular convolution we will have 8x8 times 5x5x3x256 multiplications so it will make up to 8x8x5x5x3x256 = 1228800 multiplication. On the other hand if we use depthwise separable convolution we will only need to make 8x8x5x5x3 + 8x8x256x3 which add up to 49152 multiplication. 

This will give our network a really good speed.








