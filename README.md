Amnesia: The Dark Descent Source Code
=======================

Currently the engine uses fbx sdk 2012 which isn't avalable anymore which means the engine wont compile. If you want to give a shot anyway you can find the sdk here:
https://www.autodesk.com/fbx


Other than that, here is almost everything you need to build Amnesia: The Dark Descent. Included are project files for Visual Studio 2010 and CMake for Linux & macOS. 

Contributing Code
-----------------
We encourage everyone to contribute code to this project, so just sign up for a github account, create a fork and hack away at the codebase.

License Information
-------------------
All code is under the GPL Version 3 license. Read the LICENSE file for terms of use of the license.


Installation (notes by Python Blue)
-------------------
For building the game in Windows, open the Lux solution (in amnesia/src/game) in Visual Studio 2010 and compile from there. Building the editors, sadly, are more intensive as I've discovered they were made for earlier versions of Visual Studio than 2010 and therefore have several incompatibilities depending on the tool being built, a process I'm still trying to look into myself.

For building on Mac (and hopefully Linux):

1. Open the amnesia/src directory in CMake and configure. If you're running a 64-bit-only Mac such as Catalina, make sure "IS_APPLE_64" is checked in the options and reconfigure.

2. Generate for the compiler of your choice. If running Mac, I recommend XCode in case of issues. If you're not running macOS Catalina or later, then disregard the next step.

3. Open the newly generated project in XCode, making sure the following is set in Build Settings for the entire project before building:
	a. The architecture must be x86_64. If you checked "IS_APPLE_64" earlier, this should not be an issue.
	b. The SDK might not be found. If so, set it to the default macOS SDK.
	c. Deployment target must be set to a newer OS version due to a fixed AngelScript library, which I deployed to 10.9. Earlier versions like the intended 10.6 might be possible, but don't depend on it without the AngelScript source code.
	d. Make sure you either set the C Language Dialect to GNU99, or set the C++ Standard Library to libc++; otherwise, errors relating to the std libraries will be generated. Early tests did the latter, which is why I don't recommend building for 10.6 like intended (libc++ is only an option for 10.7 onward).

4. Build and test. I recommend building only one of the projects at a time in case of issues.


Additional Note (by Python Blue)
-------------------
This particular branch implements the color grading post effect from A Machine for Pigs. That in mind, you will need the following AMFP assets, not included, in your TDD directory as well or else the game won't launch:

-the GLSL shader for the effect (core/shaders/posteffect_color_grading_frag)
-the folder of gradingmaps (textures/gradingmaps), or at least "textures/gradingmaps/colorgrading_base.png"