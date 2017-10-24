
# OpenCV Code

These notes are made with the goal of giving quick snippets that help with starting to write OpenCV code when doing a range of image processing techniques.

`CV_8UC1` means a 1 channel (C1) image where each pixel value is stored as an 8 bit unsigned integer (8U).

This code resizes images in OpenCV:
```c++
resize( image, smaller_image, Size( image1.cols/2, image.rows/2 ));
```

`<Vec3b>` means a vector with 3 byte entries.

In OpenCV, RGB images are stored in BGR format.

This code accesses a specific pixel within an image:
```c++
my_image.at<Vec3b>(row,col)
```

This code accesses each channel of a multichannel image:
```c++

void PrintChannelValues( Mat& my_image )
{
 CV_Assert( my_image.type() == CV_8UC3);‘
 for (int row=0; row < my_image.rows; row++)
   for (int col=0; col < my_image.cols; col++)
     for (int channel=0; channel < my_image.channels(); channel++)
        printf("%u\n", my_image.at<Vec3b>(row,col)[channel] );
}
```

The `at` function in OpenCV is computationally expensive, so it is better to access pixels with pointers to images' address spaces.

This code accesses each channel of a multichannel image without using the `at` function:
```c++
void PrintChannelValuesUsingPointers( Mat& image ){
  int image_rows = image.rows;
  int image_columns = image.cols;
  for (int row=0; row < image_rows; row++) {
    uchar* value = image.ptr<uchar>(row);
    for(int column=0; column < image_columns; column++)
    {
      printf("%u\n", *value++ );
      printf("%u\n", *value++ );
      printf("%u\n", *value++ );
    }
  }
}
```

This code converts images from one representation to another:
```c++
cvtColor(bgr_image, grey_image, CV_BGR2GRAY);
```

This code splits a colour image into a separate image for each of its component channels:
```c++
split(bgr_image, bgr_images);
```

In OpenCV hue values range between 0 and 179.

This code performs local averaging on an image:
```c++
blur(image,smoothed_image,Size(3,3));
```

This code performs Gaussian smoothing on an image:
```c++
GaussianBlur(image,smoothed_image,Size(5,5),1.5);
```

This code performs a binary threshold on an image:
```c++
threshold(gray_image,binary_image,threshold,
                               255,THRESH_BINARY);
```
