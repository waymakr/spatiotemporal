# spatiotemporal
# R Code for Spatiotemporal calcs
# Calculate Distance, Velocity, Accelerations and calcs on Accelerations.

Distance = sqrt((X - lag(X)) ^2 + (Y - lag(Y)) ^2),
Velocity = Distance/TimeDiff,
AccelerationRate = (Velocity - lag(Velocity))/TimeDiff,
Acceleration = if_else(AccelerationRate > 0, 1,0, missing = NULL),
Deceleration = if_else(AccelerationRate < 0, 1,0, missing = NULL),
Consec_Accelerations = as.numeric(str_replace_all(sequence(rle(as.character(Acceleration))$lengths),c("1"= "0", "[23456789]"="1"))),
IsSprint = if_else(Velocity > 4.17, 1,0, missing = NULL)

# Necessary Time Calculations
# For GPS units at 10Hz sampling Rate. 
# Where Sample numbers are for each 10th of a second

Seconds = as.numeric(hms(second(Time),minute(Time),hour(Time)))+as.numeric(str_sub(SampleNumber,-1,-1))/10,
TimeDiff = Seconds - lag(Seconds),
