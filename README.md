# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Introduction

In this project, I implemented a PID controller to make the car run properly along the path. the PID value I set was 0.16, 0.0, 4.0 after several tries. So strictly, it is a PD controller rather than PID controller since the integral coefficient is 0.

During the running, I found that the car swung heavily especially when it passed through a curved road. So I wrote a couple of lines of codes to play with the speed and throttle.

Here is the logic of controlling the speed.
```
Check if the car is keeping leaving the track.
If so, set the throttle negtive value to decrease the speed.
If not, speed up.
While the speed is less than 10mph and the car is keeping leaving the track,
set the throttle 0.1 to keep the car running.
```
Here is the code:

```          
if (pid.d_error > 0.05 && speed > 10){
  throttle = -0.1;
}
else if (pid.d_error > 0.05 && speed < 10) {
  throttle = min_throttle;
}
else if (pid.d_error < 0.05 && speed < 10) {
  if (throttle < min_throttle) {
    throttle = min_throttle;
  }
  throttle += 0.4;
  if (throttle > max_throttle) {
    throttle = max_throttle;
  }
}
```

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

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`.

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)
