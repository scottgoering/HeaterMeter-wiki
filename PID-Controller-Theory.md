### How does HeaterMeter control the pit temperature?
HeaterMeter uses an feedback algorithm called PID, which stands for proportional–integral–derivative. This method uses 3 constants to convert temperature difference into fan speed when added together.

## Proportional
Run the fan **proportional to temperature error**. That is, for every degree the current temperature is from the set point run the fan at P%. For example, for P=5 if our setpoint temperature is 200F and we're currently at 190F, run the fan at (200 - 190) x 5% = 50%. A proportional-only algorithm oscillates up and down with a amplitude relative to the size of P.

## Integral
Increase or decrease the fan speed based on **accumulated temperature error**. That is, for every degree of error per second add I% to the fan speed. For example, for I=0.1, setpoint=200F, and current=190F after one second add (200 - 190) x 0.1% = 1%. Assuming the current temperature stays the same, the integral term will increase 1% every second. The integral term is responsible for shifting the oscillation created by the proportional term so that it oscillates on each side of the setpoint.

## Derivative
Increase or decrease the fan speed based on **change in temperature**. That is, for every degree the temperature has changed over the last T seconds, add D% to the fan speed. For example, for D=10, setpoint=200F and the temperature has decreased from 210F to 205F over the past T seconds, add (210 - 205) x 10% = 50%. The D term is the value that is trying to look ahead to see what is going to happen to the temperature over time. This value prevents overshoot when starting the grill, as well as starts stoking the fire before the temperature has gone below the setpoint.

## Anti-Windup
Anti-windup is a method for preventing the integral term from building up while the pit is "out of controllable range". The pit it considered uncontrolled when the fan is running at 0% or 100%. It is assumed when the fan is running full speed or not at all that the error in the system is larger than we are currently compensating for. Consider when you first start the BBQ and the temperature is 100F, setpoint 225F. The integral term will increase by I x 125% every second as the BBQ heats up. By the temperature has reached 225F, the integral term has accumulated so much error that the fan will keep running at 100% essentially one second for every second it was below temperature.

## Bias
Because our Integral term can only be accumulated while the fan is running (greater than 0%) HeaterMeter uses a fourth parameter called the bias. The bias parameter allows the integral term to decrease even if the current temperature is above the setpoint.

## Pseudocode
    error = setpoint - temperature

    if 0 < fanSpeed < 100 then
        accumulatedError = accumulatedError + error

    fanSpeed = 
        PidB + 
        PidP * error + 
        PidI * accumulatedError + 
        PidD * (averageTemp - temperature)

### Startup Error Cut
When you first start up your BBQ or when you raise the setpoint, HeaterMeter accumulates a somewhat large integral term as the fire is gently stoked to the target. The first time the temperature is reached after one of these periods, the integral term is zeroed when the temperature crosses the setpoint. This prevents the temperature from "riding high" for the first few oscillation cycles. This should not be confused with "overshoot protection" which is created by the derivative term as a function of the rising temperature.