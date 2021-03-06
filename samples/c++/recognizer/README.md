- [Building](#building)
  - [Android](#building-android)
  - [iOS](#building-ios)
  - [Windows](#building-windows)
  - [Generic GCC](#building-generic-gcc)
  - [Raspberry Pi (Raspbian OS)](#building-rpi)
- [Testing](#testing)
  - [Usage](#testing-usage)
  - [Examples](#testing-examples)


This application is used as reference code for developers to show how to use the [C++ API](https://www.doubango.org/SDKs/mrz/docs/cpp-api.html) and could
be used to easily check the accuracy. The application accepts path to a JPEG/PNG/BMP file as input. This **is not the recommended** way to use the API. We recommend reading the data directly from the camera and feeding the SDK with the uncompressed **YUV data** without saving it to a file or converting it to RGB.

If you don't want to build this sample and is looking for a quick way to check the accuracy then, try
our cloud-based solution at [https://www.doubango.org/webapps/mrz/](https://www.doubango.org/webapps/mrz/).

This sample is open source and doesn't require registration or license key.

<a name="building"></a>
# Building #

This sample contains [a single C++ source file](main.cxx) and is easy to build. The documentation about the C++ API is at [https://www.doubango.org/SDKs/mrz/docs/cpp-api.html](https://www.doubango.org/SDKs/mrz/docs/cpp-api.html).

<a name="building-android"></a>
## Android ##
Please check [android](../../android) folder for Android samples.

<a name="building-ios"></a>
## iOS ##
Please check [iOS](../../ios) folder for iOS samples.

<a name="building-windows"></a>
## Windows ##
You'll need Visual Studio and the project is at [recognizer.vcxproj](recognizer.vcxproj).

<a name="building-generic-gcc"></a>
## Generic GCC ##
Next command is a generic GCC command:
```
cd ultimateMRZ-SDK/samples/c++/recognizer

g++ main.cxx -O3 -I../../../c++ -L../../../binaries/<yourOS>/<yourArch> -lultimate_mrz-sdk -o recognizer
```
- You've to change `yourOS` and  `yourArch` with the correct values. For example, on Android ARM64 they would be equal to `android` and `jniLibs/arm64-v8a` respectively.
- If you're cross compiling then, you'll have to change `g++` with the correct triplet. For example, on Android ARM64 the triplet would be equal to `aarch64-linux-android-g++`.

<a name="building-rpi"></a>
## Raspberry Pi (Raspbian OS) ##

To build the sample for Raspberry Pi you can either do it on the device itself or cross compile it on [Windows](#cross-compilation-rpi-install-windows), [Linux](#cross-compilation-rpi-install-ubunt) or OSX machines. 
For more information on how to install the toolchain for cross compilation please check [here](../README.md#cross-compilation-rpi).

```
cd ultimateMRZ-SDK/samples/c++/recognizer

arm-linux-gnueabihf-g++ main.cxx -O3 -I../../../c++ -L../../../binaries/raspbian/armv7l -lultimate_mrz-sdk -o recognizer
```
- On Windows: replace `arm-linux-gnueabihf-g++` with `arm-linux-gnueabihf-g++.exe`
- If you're building on the device itself: replace `arm-linux-gnueabihf-g++` with `g++` to use the default GCC

<a name="testing"></a>
# Testing #
After [building](#building) the application you can test it on your local machine.

<a name="testing-usage"></a>
## Usage ##

`recognizer` is a command line application with the following usage:
```
recognizer \
      --image <path-to-image-with-mrzdata-to-process> \
      [--assets <path-to-assets-folder>] \
      [--tokenfile <path-to-license-token-file>] \
      [--tokendata <base64-license-token-data>]
```
Options surrounded with **[]** are optional.
- `--image` Path to the image(JPEG/PNG/BMP) to process. You can use default image at [../../../assets/images/Czech_passport_2005_MRZ_orient1_1300x1002.jpg](../../../assets/images/Czech_passport_2005_MRZ_orient1_1300x1002.jpg).
- `--assets` Path to the [assets](../../../assets) folder containing the configuration files and models. Default value is the current folder.
- `--tokenfile` Path to the file containing the base64 license token if you have one. If not provided then, the application will act like a trial version. Default: *null*.
- `--tokendata` Base64 license token if you have one. If not provided then, the application will act like a trial version. Default: *null*.

<a name="testing-examples"></a>
## Examples ##

For example, on **Raspberry Pi** you may call the recognizer application using the following command:
```
LD_LIBRARY_PATH=../../../binaries/raspbian/armv7l:$LD_LIBRARY_PATH ./recognizer \
    --image ../../../assets/images/Czech_passport_2005_MRZ_orient1_1300x1002.jpg \
    --assets ../../../assets
```
On Android ARM64 you may use the next command:
```
LD_LIBRARY_PATH=../../../binaries/android/jniLibs/arm64-v8a:$LD_LIBRARY_PATH ./recognizer \
    --image ../../../assets/images/Czech_passport_2005_MRZ_orient1_1300x1002.jpg \
    --assets ../../../assets
```

Please note that if you're cross compiling the application then you've to make sure to copy the application and both the [assets](../../../assets) and [binaries](../../../binaries) folders to the target device.


