# PWM_generator_module

## introduction about PWM signal

- Pulse Width Modulation explanation
> PWM is a technique which controls the duty cycle
        what an analog device sees is the average voltage which equals to 
        (duty cycle * VDD) 
        so controling the PWM signal which controls the duty cycle "d" allows us to
        control the voltage supplied to the analog devices for ex. LED's or a servo motor

- Resulotion explanation
> the duty cycle "d" can have infinite values from 0 -> 100% 
        so the resulotion "R" is the thing which detrmines the number of levels of "d", 
        so talking about R, R is the number of bits which the storage element contains
        for EX. if R=8bits >> so we have 256 levels from 0 -> 100% with minimum step of (1/2^R)
        which in our case will be minimum step of (1/256), so our duty cycles will be : 
        [0/256, 1/256, 2/256, ..., 256/256]

- switching frequency explanation
>  a PWM signal is still a periodic rectangular signal, 
    although it has different duty cycles, but still it's periodic
    since it's periodic so it will have a frequency "Fpwm"


## repo. contents
- pwm_basic module
- up_counter module
- timer module
- pwm_improved module
- RGB_driver module


## files and modules explanation

- pwm_basic module
>this module cosnsits of 2 parts : counter, comparator and input 
    which is the desired duty cycle.
    the output of the module will be 1 "high" as long as the counter's output value is less than the ouput duty cycle
    and when the counter exceeds the duty value the output of the module drops to zero, and that's it
    Now you have a Basic PWM module
    and this is just a basic module which has some issues, 
    and will be solved @ the improved module


- pwm_improved module
  > This module has two improvements rather than the basic.
    1. Frequency control over the PWM signal.
    2. Made the output signal synchronized with the clock.

    - First Improvement
      ![PWM-freq-equation](https://github.com/eslamsolyman01/PWM-generator-module/assets/138836583/46ab2da8-e636-4ea1-a577-159b02b78a83)

      > Here, it explains how we can control the frequency of the PWM signal using a timer.
      We need to set a final value for this timer, and the equation relating this value
      with the Fpwm is shown in the slide. Note that both the timer and the UP_counter
      both work with the system clock.

    - Second Improvement
      ![image](https://github.com/eslamsolyman01/PWM-generator-module/assets/138836583/5c26406b-e9df-4f9d-b727-f9ee1dd3b08a)

      > The final improvement here is adding D_FF. At the up counter with the written values,
      for example, there are 3 bits changing, and what might happen is one of them will change
      after the rest, meaning the number entering the comparator at that moment is not correct,
      which may cause a glitch. To ensure the counter value being compared is the right one,
      we will use this D_FF, which will wait for the clock edge, at which we will have the right
      values with no glitches.


- RGB_driver
> this module utilizes the improved_PWM we created before 
    it's used to drive RGB LEDs on an fpga kit 






## simulation output 

> two screent-shots were taken with two different timer values 
  as you will notice from the time at the screen,
  the final value of the timer controls the period of the PWM_signal as expected

        - timer_final_value= 128
![timer_final_value= 128](https://github.com/eslamsolyman01/PWM-generator-module/assets/138836583/2f7e73a9-a710-450f-83d4-a335e01318a4 "timer_final_value= 128")

 


        - timer_final_value= 1
![timer_final_value=1](https://github.com/eslamsolyman01/PWM-generator-module/assets/138836583/8a79b2cb-b18c-4388-b677-9e7dd3330c3b "Timer Final Value = 1, difference can be noticed from the period time")
