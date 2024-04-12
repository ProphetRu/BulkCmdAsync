# BulkCmd Async
Educational project with [googletest](https://github.com/google/googletest) and [doxygen](https://github.com/doxygen/doxygen)

## Build local Linux
```shell
sudo apt-get update && sudo apt-get install cmake libgtest-dev -y

cd BulkCmdAsync
mkdir build && cd build

cmake ..

# build release
cmake --build . --config Release

# build deb-package
cmake --build . --target package
```

## Build local Windows
```shell
vcpkg install gtest
vcpkg integrate install

cd BulkCmdAsync
mkdir build && cd build

cmake .. -DCMAKE_TOOLCHAIN_FILE="path/to/vcpkg/scripts/buildsystems/vcpkg.cmake"

# build release
cmake --build . --config Release
```

## Usage
```cpp
#include "async.h"

int main()
{
    std::size_t bulk = 5;

    auto h = async::connect(bulk);
    auto h2 = async::connect(bulk);

    async::receive(h, "1", 1);
    async::receive(h2, "1\n", 2);
    async::receive(h, "\n2\n3\n4\n5\n6\n{\na\n", 15);
    async::receive(h, "b\nc\nd\n}\n89\n", 11);

    async::disconnect(h);
    async::disconnect(h2);
    
    return 0;
}
```