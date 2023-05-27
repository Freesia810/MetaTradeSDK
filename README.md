# MetaTradeSDK
Shared library in MetaTrade

## How to code
```c++
#include <MetaTradeApplication/MetaTradeApplication.h>

int main() {
    MetaTradeApplication application;


    //For init(pky file not found)
    //Create Config as you like
    //eg: CreateConfigByStr(const char* pky) CreateConfigByRandom(); 

    //Be sure that the return value is true
    if (!application.ReadConfig()) {
        application.CreateConfigByRandom();
    }
    if (!application.ReadConfig()) {
        std::cerr << "error\n";
        return 0;
    }

    //false -- cancel mining service
    application.Init(false);

    //true -- run sync
    //false -- run async
    application.Run(false);

    //call apis -- see in `MetaTradeApplication.h`
    long long your_amount = application.QueryAmount("123", "0");

    StoreInfo* infos;
    uint64_t sz;
    application.QueryStoreInfoList(&infos, &sz);

    std::cout << sz << std::endl;

    for (uint64_t i = 0; i < sz; i++) {
        std::cout << "id: " << infos[i].id << " des: " << infos[i].description << std::endl;
    }

    ItemInfo* item_list;
    application.QueryItemInfoList(&item_list, &sz, infos[0].address);

    std::cout << sz << std::endl;

    for (uint64_t i = 0; i < sz; i++) {
        std::cout << "id: " << item_list[i].id << " des: " << item_list[i].description << std::endl;
    }

    return 0;
}

```
## How to build
### Build envrionment
- Compiler: `msvc-v143` in `Visual Studio 2022`
- Platform: `Windows 10/11 (Windows SDK 10.0)`

### Build Debug
#### Compile
- Include Directory: `PATH_TO_YOUR_PROJECT/Debug/include;$(IncludePath)`
- Library Directory: `PATH_TO_YOUR_PROJECT/Debug/lib;$(LibraryPath)`
#### Link
- Additional Library: `PATH_TO_YOUR_PROJECT/Debug/lib;%(AdditionalLibraryDirectories)`
- Additional Dependencies: `libcrypto.lib;libssl.lib;libMetaTrade_d.lib;libMetaTradeNode_d.lib;leveldb_debug.lib;cpprest141_2_10d.lib;%(AdditionalDependencies)`

### Build Release
#### Compile
- Include Directory: `PATH_TO_YOUR_PROJECT/Release/include;$(IncludePath)`
- Library Directory: `PATH_TO_YOUR_PROJECT/Release/lib;$(LibraryPath)`
#### Link
- Additional Library: `PATH_TO_YOUR_PROJECT/Release/lib;%(AdditionalLibraryDirectories)`
- Additional Dependencies: `libcrypto.lib;libssl.lib;libMetaTrade.lib;leveldb.lib;libMetaTradeNode.lib;cpprest141_2_10.lib;%(AdditionalDependencies)`
