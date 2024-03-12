# ads_catkin

This catkin wrapper is outdated. The recommended approach uses `FetchContent` directly in Cmake of the package that requires the Ads library. This solution generates less overhead by making the library available in the configure step of cmake and can easily be adapted to newer Ads versions.

Include the following commands into your `CMakeLists.txt` to fetch the Ads library:

```
include(FetchContent)
FetchContent_Declare(
  beck_ads
  GIT_REPOSITORY https://github.com/NanoFlexRobotics/ADS
  GIT_TAG        v12
)

FetchContent_MakeAvailable(beck_ads)
```

Then link the library:

```
target_link_libraries(${PROJECT_NAME} ads)
```

In your code, the library can be included as follows:

```
#include "AdsLib.h"
```
