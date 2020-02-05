# Configuration Tutorial before Running code in Ubuntu 18.04 on PI4

**Attention: Architecture Difference ! ! !**  
Our Laptop: **x86**  
Raspberry Pi4: **arm**  
This is useful when you want to choose some software.

## 1.Install Pylon
  1. Go to the [pylon software download](https://www.baslerweb.com/en/sales-support/downloads/software-downloads/#type=pylonsoftware;language=all;version=all) site, and choose **More Downloads**, find [pylon-5-2-0-linux-arm-64-bit-debian](https://www.baslerweb.com/en/sales-support/downloads/software-downloads/pylon-5-2-0-linux-arm-64-bit-debian/). If you download other pakage without an "arm" word in it, you wll not be able to install it in your Ubuntu 18.04 system. (refer to the Architecture Difference I mentioned before.)
  2. Click `.deb` file and the installation would begin.
  3. Connect your camera module to USB3.0 port in your PI4.
  4. Test your pylon library  
  - Test with pylon software  
      - Click "Show Applications" in the left corner of your desktop, then search for "pylon", choose "Pylon Viewer";
      - If your camera connects successfully, you will see your device in the leftside of your screen;
      - double-click your device, then right click, choose "Continuous Shots". Now you will see a video stream in the right.
        You will only see a messy video if you do not have a lens installed.  
  - Test with c++ sample code  
  ```bash
      cd /opt/pylon5/Samples/C++
      make
      ./Grab/Grab
  ```
## 2. A missing file
  1. After you install your pylon, run 
  ```bash
  sudo apt-get update
  sudo apt-get upgrade
  ```
  you might see an error like this:
  ```bash
  Couldn't find DTB bcm2711-rpi-4-b.dtb on the following paths: /etc/flash-kernel/dtbs
  ```
  2. This should be caused be a missing file. Download `bcm2711-rpi-4-b.dtb` from [here](https://github.com/raspberrypi/firmware/tree/master/boot)
  3. `cd` to the directory where your `.dtb` file is at, then run:  
  ```bash
  sudo cp bcm2711-rpi-4-b.dtb /etc/flash-kernel/dtbs
  sudo apt-get upgrade
  ```
  4. You will not see the error message any more.

## 3. Install opencv ([refer](http://pydeeplearning.com/opencv/install-opencv-with-c-on-ubuntu-18-04/))
  1. The following linux command will install OpenCV on Ubuntu 18.04 with C++ libraries:  
  ```bash
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install libopencv-dev
  ```
  2. Make a directory for your test.  
  ```bash
    mkdir test
    cd test
  ```
  3. In you directory, copy the below code into a new `img-display.cpp` file  

    #include <opencv2/core/core.hpp>
    #include <opencv2/highgui/highgui.hpp>
    #include <iostream>

    using namespace cv;
    using namespace std;

    int main( int argc, char** argv )
    {
        if( argc != 2)
        {
         cout <<" Usage: display_image ImageToLoadAndDisplay" << endl;
         return -1;
        }

        Mat image;
        image = imread(argv[1], CV_LOAD_IMAGE_COLOR);   // Read the file

        if(! image.data )                              // Check for invalid input
        {
            cout << "Could not open or find the image" << std::endl ;
            return -1;
        }

        namedWindow( "Display window", WINDOW_AUTOSIZE );// Create a window for display.
        imshow( "Display window", image );                // Show our image inside it.

        waitKey(0);             // Wait for a keystroke in the window
        return 0;
    }

  4. Save an image from other place called `dog.jpg`, run the following commands in your `test` directory:  
  ```bash
    g++ img-display.cpp -o img-display `pkg-config --cflags --libs opencv`
    ./img-display dog.jpg
  ```
  5. Now you will see your picture
