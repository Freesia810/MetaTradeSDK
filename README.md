# MetaTradeSDK
Shared library in MetaTrade

## How to code
```c++
#include <MetaTradeApplication/MetaTradeApplication.h>

int main(){
    MetaTradeApplication application;

    
    //For init(pky file not found)
    //Create Config as you like
    //eg: CreateConfigByStr(const char* pky) CreateConfigByRandom(); 
    
    //Be sure that the return value is true
    ReadConfig();

    //false -- cancel mining service
    Init(true/false);

    //true -- run sync
    //false -- run async
    Run(true/false);

    //call apis -- see in `MetaTradeApplication.h`
    long long your_amount = QueryAmount("123", "0");
    long long your_trading_amount = QueryTransitAmount("123", "0");
    SubmitTrade("456", "0", 1000);

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
- Additional Dependencies: `libMetaTradeNode_d.lib;leveldb_debug.lib;cpprest141_2_10d.lib;%(AdditionalDependencies)`

### Build Release
#### Compile
- Include Directory: `PATH_TO_YOUR_PROJECT/Release/include;$(IncludePath)`
- Library Directory: `PATH_TO_YOUR_PROJECT/Release/lib;$(LibraryPath)`
#### Link
- Additional Library: `PATH_TO_YOUR_PROJECT/Release/lib;%(AdditionalLibraryDirectories)`
- Additional Dependencies: `leveldb.lib;libMetaTradeNode.lib;cpprest141_2_10.lib;%(AdditionalDependencies)`