# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets) == 0.13, but the master branch will probably work just fine
  * Follow the instructions in the [uWebSockets README](https://github.com/uWebSockets/uWebSockets/blob/master/README.md) to get setup for your platform. You can download the zip of the appropriate version from the [releases page](https://github.com/uWebSockets/uWebSockets/releases). Here's a link to the [v0.13 zip](https://github.com/uWebSockets/uWebSockets/archive/v0.13.0.zip).
  * If you run OSX and have homebrew installed you can just run the ./install-mac.sh script to install this
* Simulator. You can download these from the [project intro page](https://github.com/udacity/CarND-PID-Control-Project/releases) in the classroom.

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`.

## Windows Install Instructions 

1. Install, in your root `c:/` directory, vcpkg https://github.com/Microsoft/vcpkg   (15 - 30 minutes)
2. Be sure while installing vcpkg to carefully follow all instructions! This is NOT an easy install process.
3. Install python 2.7 (dependency for libuv) 
4. cd to directory with vcpkg .exe and `./vcpkg install uWebsockets` (20 min, mostly automatic)
5. Open CMakeSetting.json, check if `C:/vcpkg/scripts/buildsystems/vcpkg.cmake` is the correct directory to your vcpkg and `DCMAKE_TOOLCHAIN_FILE` matches the output from vcpkg integrate.
6. Open in VS17 community edition, build pid.exe in x86 debug.


## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.

## Hints!

* You don't have to follow this directory structure, but if you do, your work
  will span all of the .cpp files here. Keep an eye out for TODOs.

## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to we ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./

## Solution

I started with a low speed and just the proportional constant, to find a good value 
for the proportional correction of the CTE. [Video 1](https://github.com/fera0013/CarND-PID-Control-Project/blob/master/videos/t0_1p0_1i0d0s.webm) shows,
that a proportional value of 0.1 is sufficient to drive the car safely around the complete 
track with some minimal and temporary oscillation. 
With a higher throttle value of 0.2 and with the initial proportional value of 0.1, the oscillation increases considerably 
to a point at which the car completely runs of the track, as can be seen in [Video 2](https://github.com/fera0013/CarND-PID-Control-Project/blob/master/videos/t0_2p0_1i0d0f.webm).
The problem of an oscillation that builds up over time can be mitigated by the addition of a differential component.  [Video 3](https://github.com/fera0013/CarND-PID-Control-Project/blob/master/videos/t0_2p0_1i0d3s.webm) shows the significant effect of a differential value of 3, in combination with otherwise 
unchanged parameters: The car steers much more abruptly, rarely overshoots and makes it safely around the track. 
Even at a speed of 30 mph, the combination of a proportional component of 0.1 and a differential component of 3 still steers 
the car safely around the track. The driving experience is however much more unstable, as [video 4](https://github.com/fera0013/CarND-PID-Control-Project/blob/master/videos/t0_3p0_1i0d3s.webm)  shows.

It should be noted that the addition of an integral component did not help in combination with the chosen parameters. 
This is however not surprising, since the simplified simulation model does not seem to contain any systematic bias. 



