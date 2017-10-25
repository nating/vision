# Computer Vision
If you came here looking for resources for CS4053, you just missed them. You can request access to a different repository with some available [here](https://github.com/nating/cs4053) if you want.

## How to Set up your OpenCV environment on Mac

*Please note: Keep in mind that it matters where your 'build' folder is when you run CMake, and this path is where your build folder's path should point to for eternity.*

* <a href="https://itunes.apple.com/ie/app/xcode/id497799835?mt=12" target="_blank">Install XCode</a>
* <a href="https://cmake.org/download/" target="_blank">Install CMake</a>
* Download OpenCV:
  1. <a href="https://github.com/opencv/opencv/releases" target="_blank">Get the latest release of OpenCV</a>
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
  5. Add `<The path to the build folder you made>/lib` to 'Library Search Paths'.
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


