# CarND-Controls-PID
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)



## Overview

The purpose of this project was to implement a PID controller to control a car in Udacity's simulator. The simulator sends cross-track error(CTE), speed and angle to the PID controller using WebSocket.  And PID controller receives the steering angle ([-1, 1] normalized) and the throttle to drive the car reliably around the simulator track.

## PID effections

1. Proportional(P) based controller steer the car toward the center line (against the cross-track error). If used along, the car overshoots the central line very easily and go out of the road very quickly. This [video](https://youtu.be/3dgt6mo-wu4)is the example of using P controller only.

2. Integral(I) based controller eliminate a possible bias on the controlled system by accounting the past values of the error that could prevent the error to be eliminated. If used along, it makes the car to go in circles. This [video](https://youtu.be/aHTsgL_ByHg) is the example of using I controller only.

3. Differential(D) based controller helps to counteract the proportional trend to overshoot the center line by smoothing the approach to it. This [video](https://youtu.be/riUOQ9LHelU) is the example of using D controller only.

## How to tune the parameters?

The parameters were chosen manually by try and error.

* Step1. I started with Proportional(P) cause it steer the car toward to center, I started from 1 then reduced it gradually until the car following the road better. The final P is 0.15.
* Step2. I added the Differential(D) to overcome the overshooting. I started from 1 then increased to 3. The car finally could drive around the track.
* Step3. I turned Integral(I) from 0 to 0.0005 so the car can drive smoothly.

The final parameters were [P: 0.15, I: 0.0005, D: 3].
This is the final [video](https://youtu.be/MIpe3QhXvLE).

## Possible Improvements

Sebastian Thrun demonstrated how to turn parameters automatically by Twiddle algorithm. I will try to implement twiddle in the future.

<img src="outputs/twiddle.png" width="480" />

With twiddle the PID controller converges faster but we overshoot drastically at first so it's a tradeoff. 
<img src="outputs/compare.png" width="480" />


## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

Fellow students have put together a guide to Windows set-up for the project [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/files/Kidnapped_Vehicle_Windows_Setup.pdf) if the environment you have set up for the Sensor Fusion projects does not work for this project. There's also an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3).

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

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
