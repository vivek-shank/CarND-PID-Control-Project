# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Impact of PID components

While it is fascinating that a simple PID controller can perform as well as this in comparison with the elaborate Behavioral cloning project in Term1, I took a while to figure that Cross Track Error computation which needs Truth is a actually severe limitation. Term1 project performed well even in an unknown environment.

In this case, the relevance of this the components are described below.

* P(proportional):
 * As apparent from the name, this is the steer angle applied in proportion to the CTE. This is the workhorse of the PID controller which does all the heavy lifting. A Stand-alone P controller results in oscillatory trajectory as we never achieve perfect convergence.
 
* D(Derivative/Differential):
 * In order to avoid the oscillatory behavior in the P controller, we add a differential of CTE to steer angle to aggressively approach the truth when we are far apart and introduce a counter-steer component to provide smoothing when we are close to the Truth trajectory.
 
* I(Integral):
 * Whenever we have Steering drift in the front axle wheels, we have a constant error called Systematic Bias. In order to eliminate this, we keep track of accumulated CTE. In a regular system, the accumulated error will gradually increase and stay constant once we converge. In the error case, however, the accumulated error builds up therby prompting us to steer more towards the truth.
 
 
## Selection of PID coefficients 

In the interest of time, I did not attempt Twiddle factor method. I knew that there is no Systematic Bias in this system and hence, chose a small value for 'kI' first. So, I manually played with the other two components balancing between wavering hard out of the track or not reacting fast to a turn. This combination works well on the simulator track.