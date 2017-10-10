# Computer Vision
A repository for Computer Vision projects written in OpenCV.

## How to Set up your OpenCV environment on Mac

* [Install XCode](https://itunes.apple.com/ie/app/xcode/id497799835?mt=12)
* [Install CMake](https://cmake.org/download/)
* Download OpenCV:
  1. [Get the latest release of OpenCV](https://github.com/opencv/opencv/releases)
  2. Create a folder called 'build' within the OpenCV folder you downloaded
  3. Open CMake
  4. Select the downloaded folder as the source file
  5. Select your new 'build' folder as where to build the binaries.
  6. Click 'configure', check that 'Unix Makefiles' is the generator for the project and that 'Use default native compilers' is checked.
  7. Click 'done'.
  8. When the configuration is done, click 'generate'.
* Inside your build folder in the downloaded OpenCV folder, run ```make```. (You might need to run ```brew install make gcc```)
* In the same directory, run ```sudo make install```
* Open XCode and select 'create new XCode project'.
* Select the 'Command Line Tool' template under 'macOS'.
* Name and create your project (Make sure you select 'C++' as the language for the project)
* Update the Project's search paths:
  1. In 'Build Settings' search for 'Search Paths' (Make sure you are searching 'All' build settings and not just 'Basic' ones)
  2. Make sure that 'Always Search User Paths' is set to 'Yes'.
  3. Add `/usr/local/lib` to 'Framework Search Paths'.
  4. Add `/usr/local/include` to 'Header Search Paths'.
  5. Add `<The path to your build folder>/lib` to 'Library Search Paths'.
* Search the Build Settings for 'Other Linker Flags' and add every file except the 'cv2.so' from the 'lib' folder now inside your 'build' folder from before. (You can drag and drop these into the 'Other Linker Flags' in XCode)

You can test that you have set up OpenCV correctly by replacing the code in your main.cpp with this code and running it:
```cpp
#include <iostream>
#include <opencv2/opencv.hpp>

int main(int argc, const char * argv[]) {
    std::cout << "Open CV Version:" << CV_VERSION << std::endl;
    return 0;
}
```


