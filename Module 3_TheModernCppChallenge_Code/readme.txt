Instructions for building the source code:

Mac OS X / Xcode
----------------------------

Prerequisites:
--------------

OpenSSL
1. Download openssl from https://www.openssl.org/.
2. Build and install openssl running the following commands:

   ./Configure darwin64-x86_64-cc shared enable-ec_nistp_64_gcc_128 no-ssl2 no-ssl3 no-comp --openssldir=/usr/local/ssl/macos-x86_64
   
   make depend
   
   sudo make install

Boost (optional)
1. Install Homebrew from https://brew.sh/.
2. Run the following command to download and install Boost automatically.
   
   brew install boost
   
3. After installation, the Boost library will be available at /usr/local/Cellar/boost/1.65.0.


Source code:
--------------

1. Build CMake scripts with the following commands:
   
   cd build
   
   cmake -G Xcode .. -DOPENSSL_ROOT_DIR=/usr/local/bin -DOPENSSL_INCLUDE_DIR=/usr/local/include/ -DBUILD_TESTING=OFF -DBUILD_CURL_EXE=OFF -DUSE_MANUAL=OFF 
   
   Should you use Boost.Filesystem or Boost.Optional instead of standard library, you need to specify three additional parameters: 
     BOOST_FILESYSTEM  set to ON
     BOOST_OPTIONAL    set to ON
     BOOST_INCLUDE_DIR the path to the Boost headers directory 
     BOOST_LIB_DIR     the path to the Boost libaries directory
   
   cmake -G Xcode .. -DOPENSSL_ROOT_DIR=/usr/local/bin -DOPENSSL_INCLUDE_DIR=/usr/local/include/ -DBUILD_TESTING=OFF -DBUILD_CURL_EXE=OFF -DUSE_MANUAL=OFF -DBOOST_FILESYSTEM=ON -DBOOST_OPTIONAL=ON -DBOOST_INCLUDE_DIR=/usr/local/Cellar/boost/1.65.0 -DBOOST_LIB_DIR=/usr/local/Cellar/boost/1.65.0/lib
   
2. Open the Xcode project from build/cppchallenger.xcodeproj



Windows / Visual Studio 2017
----------------------------

1. Build CMake scripts with the following commands:

   cd build
   
   cmake -G "Visual Studio 15 2017" .. -DCMAKE_USE_WINSSL=ON -DCURL_WINDOWS_SSPI=ON -DCURL_LIBRARY=libcurl -DCURL_INCLUDE_DIR=..\libs\curl\include -DBUILD_TESTING=OFF -DBUILD_CURL_EXE=OFF -DUSE_MANUAL=OFF
   
2. Open the Visual Studio solution from build/cppchallenger.sln
