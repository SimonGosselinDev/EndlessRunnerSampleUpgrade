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

Here's a much deeper look into the workflow I took:

I started by making this GitHub repo, creating a blank URP core Unity project in Version 2021.3.6f1 to get a baseline of how the game worked and looked.
Immediately afterwards I made a duplicate project on my local machine only so I could quickly reference potential inconsistencies and compare stats, the profiler, material settings, and package manager moving forward. 
Once I had my copy, I pushed my changes to master in the Git repo, then made a development branch that would be useful for staging changes before moving them into master for testing.
I made another branch for each version off of development, the idea being that it would keep everything separate and easy to reference going forwards if I needed to. Once I felt comfortable with the state that the current version was in, I could merge it to development then make a new branch for the next version off of the updated branch.
I wanted to work with incremental changes in Unity version to not only keep a better record of what broke when, but also because I had an idea that Unity would be much better at being able to handle minor version changes instead of a big shock if I went straight to Version 6.3. I decided that a year gap between each version number was probably sufficient in this case.

Verion 2021 -> 2022
- Before even launching the project, I deleted the Library folder, Temp folders, and everything else Unity could regenerate on its own. This may not have been necessary, but I felt it would help my chances with a clean update.
- Upon launching the project after moving versions I was immediately greeted with the message that the URP materials would have to be updated. Clicked proceed and went on, no issues there.
- There were no errors in the console log, and after hitting play no errors were found after trying to achieve all game states (playing through the level, visiting the store, leaderboards etc.)
- While the game was running at a similar framerate, I did note that the CPU Main was averaging about 50ms per frame instead of the 5ms it was preivously. This felt like minor enough not to be a problem, but I wanted to write it down if it became relevant later. 
- Felt confident in the performance, so I pushed the changes, merged into development, then pushed that. Made a new branch for 2023.

Version 2022 -> 2023
- Same thing as before, deleted all files Unity could regenerate before launching.
- Once again, Unity had to upgrade materials to the newer URP version.
- This time one of the packages was marked as depreciated: The Visual Studio Code Editor package. There was a new package called Visual Studio Editor which seemed like a new version, so I removed the old one and there were no real changes.
- No errors, gameplay felt identical.
- Oddly, the stats shown went back to having a CPU Main time of 5ms on average, similar to the original. My guess is that it was just an abnormality of the previous version.
- New warning stating that the Unity Game Services IAP was uninitialized. I created a simple script, pretty much identical to the Unity documentation, on how to initialize it, but I did not end up including it in the project because it required a legitmate Unity account with those services enabled to fully get rid of the warning.
- Pushed changes, merged into development, pushed, then made 6.3 branch.

Version 2023 -> 6.3
- Same thing as before, deleted all files Unity could regenerate before launching.
- Once again, Unity had to upgrade materials to the newer URP version.
- This time I recieved a message that the Mobile Dependency Resolver was necessary to resolve native dependencies. I followed the instructions given and it works as intended.
- I noticed at this point that while playing the latest version that there would be a frame stutter every 10-15 seconds. After looking in the profiler, I realized that I needed to turn Deep Profiling off, which was part of it, but the stutter was because of a Garbage Collection process that happened 20,000 times in one frame. I checked the project settings and Incremental Garbage Collection was not checked, so I turned it on and the stuttering went away completely.
- I made a build to test my final changes, and nothing loaded because I had not made an Addressables build, so I set up the path to create one on my local machine and tested it. After the new build, everything ran as expected. If I was to do this again, I think my biggest mistake was not making a build until this point. I got carried away with the testing in the editor and didn't confirm my findings in a real build, which is a learning point for me moving forward. 