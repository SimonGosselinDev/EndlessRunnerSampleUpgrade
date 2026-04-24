# EndlessRunnerSampleUpgrade

Simon Gosselin	simongosselin.dev@gmail.com

Upgraded EndlessRunnerSampleUpgrade from Unity version 2021.3.6f1 LTS to version 6000.3.14f1 LTS

Notable Changes
- Upgraded materials to newer URP version.
- Upgraded Addressable assets to newer build version.
- Turned on Incremental Garbage Collection in Player Settings to fix a stuttering issue found in 6.3

To build, just use the Unity Build functionality in the build menu. The default profile works for windows.
Addressables will needed to be built as well in order to use in a standalone build. 

In the future, work will need to be done to convert this to mobile devices. All the upgrading work was tested on Windows alone.




