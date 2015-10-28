# PSMoveService
A background service that communicates with the psmove and stores pose and button data.

# Download

`git clone --recursive https://github.com/cboulay/PSMoveService.git`
`cd PSMoveService`

# Build Dependencies

1. Compiler
    * Windows
	    * Visual Studio 2013 is required by OpenCV 3.0.0 pre-compiled binaries.
    * Mac
	    * Tested with XCode/clang. gcc may work.
1. OpenCV
    * I am opting for a system install of opencv instead of project-specific.
    * Windows
        * Follow steps 1-3 found [here](https://github.com/MicrocontrollersAndMore/OpenCV_3_Windows_10_Installation_Tutorial/blob/master/Installation%20Cheat%20Sheet%201%20-%20OpenCV%203%20and%20C%2B%2B.pdf)
        * Download from here: http://sourceforge.net/projects/opencvlibrary/files/opencv-win/3.0.0/opencv-3.0.0.exe/download
    * Mac
        * Install [homebrew](http://brew.sh/)
        * `brew tap homebrew/science`
        * `brew install opencv`
1. Boost
    * Windows
        * Download 32-bit boost for MSVC-2013 from here: http://sourceforge.net/projects/boost/files/boost-binaries/1.59.0/boost_1_59_0-msvc-12.0-32.exe/download
        * Install to a directory of your choice
        * This path will be referred to BOOST_ROOT later
1. Optional: libusb
    * Only necessary for PS3EYEDriver (required on Mac and Windows 64-bit)
    * Windows:
        * Open psmoveapi\external\libusb-1.0\msvc\libusb_2013.sln
        * Change the target to Release x64 (at the top of the Visual Studio window).
        * Right-click on libusb-1.0 (static) and select Properties.
        * In the properties Window, make sure the Platform is set to Active or All Platforms.
        * In the properties Window, navigate to Configuration Properties > C/C++ > Code Generation
        * Change "Runtime Library" to Multi-threaded DLL (/MD)
        * Click OK
        * Right-click on libusb-1.0 (static) and Build.
    * Mac:
        * `cd thirdparty/libusb`
        * `./autogen.sh`
        * `./configure`
        * `./configure` (yes, a second time)
        * `make`
1. Optional: [CL Eye Driver](https://codelaboratories.com/products/eye/driver/)
    * Only necessary for Windows 32-bit if not using PS3EYEDriver
	* Currently $2.99 USD (paypal or credit card)
	* Platform SDK not necessary

# Make PSMoveService

1. `mkdir build`
1. `cd build`
1. Run cmake
    * Windows: `cmake .. -G "Visual Studio 12" -DOpenCV_DIR=C:\OpenCV-3.0.0\build -DBOOST_ROOT=C:\boost_1_59_0`
    * Mac: `cmake ..`

# Build PSMoveService

### Windows

1. Open <path_to_repo>\build\PSMoveService.sln
1. Change to "Release" configuration
1. Remove _DEBUG preprocessor definition
    * TODO: Why is this happening?
	* Rt-click on the project name, Open 'Properties'
	* 'Configuration Properties' > 'C/C++' > Preprocessor
	* Edit "Preprocessor Definitions" and delete _DEBUG
1. Rt-click on the project and build