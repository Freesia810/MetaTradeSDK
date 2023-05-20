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