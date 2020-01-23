# ads_catkin

A catkin wrapper for the Beckhoff ADS library. Builds the ADS library from the external source code.

The library is included with `include <AdsLib/AdsLib.h>` when built with catkin_tools.

## Troubleshooting

In case the source code from Beckhoff's ADS library can not be loaded automatically from their repository, you can use the branch containing the source code:

[Source Branch](https://github.com/ethz-msrl/ads_catkin/tree/source)

The version tested by @chautemc is provided in [this commit of the source branch](https://github.com/ethz-msrl/ads_catkin/tree/831139202f208f0702897de956f8a1d70164a89f).