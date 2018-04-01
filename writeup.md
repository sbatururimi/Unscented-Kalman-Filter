## Writeup 

-----

**Unscented Kalman Filter Project**

[//]: # (Image References)

[image0]: ./nis_lidar.jpg "Nis Lidar"
[image1]: ./nis_radar.jpg "Nis Radar"
[image2]: ./chi-square_distribution_table.jpg "Chi Square distribution"


## Parameters and consistency

For the CTRV model, two parameters define the process noise:
- longitudinal acceleration noise
- yaw acceleration noise

In order to tune them, we compute the Normalized Innovation Squared (NIS) for the radar and the lidar. Using the chi-squared distribution table

![alt text][image2]

I have tuned the process noise parameters in order to obtain the expected NIS:

![alt text][image0]

![alt text][image1]

## Yaw acceleration noise

The Process noise standard deviation yaw acceleration is set to 𝛑/4 rad/s^2. Let's explain the intuition behind.
Imagine the bicycle is traveling in a circle with a constant yaw rate (angular velocity) of 𝛑/8 rad/s. If now the angular acceleration -𝛑/4 rad/s^2, then 
in just one second, the angular velocity would go from 𝛑/8 (rad/s)- 𝛑/4 (rad/s^2) * s = -𝛑/8 rad/s. With such angular acceleration, the circle is completed in 16s, which is reasonable.

## Longitudinal acceleration noise

The choice is of 2.4 m/s^2. In a Gaussian distribution, about 95% of your values are within 2 * 𝛔_a. By choosing 2,4 as the standard deviation longitudinal acceleration, 
we got 𝛔_a^2 = 5.76 m^2/s^4, so we expect the acceleration to be between -4.8 m/s^2 and 4.8 m/s^2 95% of the time which is quite logic for a bicycle.