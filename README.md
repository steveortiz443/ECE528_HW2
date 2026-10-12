# ECE528_HW2

*Section I: Review Questions*

**1. What is a hardware timer? What kinds of tasks do embedded systems commonly use hardware timers for?**
A hardware timer is a circuit inside a microcontroller or processor that counts clock pulses. This is used for common tasks, such as periodic execution of operations, like reading a sensor or changing the state of a LED, measuring time, like when debouncing a button, or when generating pulse width modulation, to control motor speed or servo position.

**2. What is a clock signal used for in embedded systems? List the primary clock sources available on the MSP432P401R microcontroller and briefly describe each clock source.**
A clock signal is used as a reference to drive peripherals and ccoordinate operations.
The primary clock sources available on the MSP432P401R are as follows:
• LFXT - Uses low-frequency 32.768kHz crystals
• HFXT - Uses high frequency crystals, capable of reaching 48 MHz
• DCO - A power-efficient tunable internal oscillator that generates up to 48 MHz. Supports a high-precision mode when using an external precision resistor.
• Very Low-Power Low-Frequency Oscillator (VLO) - an ultra-low-power internal oscillator that generates a low-accuracy clock signal around 9.4 kHz.
• Low-Frequency Reference Oscillator (REFO) - An internal source configurable to a a low-power lower-accuracy source of a 32.768 kHz clock, instead of the LFXT, or as a 128 kHz clock.
• Module Oscillator (MODOSC) - Internal 25 MHz oscillator with low-latency, used to supply a "clock on request" to different modules, like the ADC operation.
• System Oscillator (SYSOSC) - Internal 5 MHz used for ADC operation at 200ksps sampling rate, along with the timing of various system-level control and management operations.

**3. Consider a 16-bit timer (e.g. Timer_A configured in up mode). If it counts upward, what is the maximum count value before it rolls over? Show your work.**
The maximum count value would be 0xFFFF in hexadecimal, or 2^16 - 1.

**4. If a 24-bit timer counts upward from zero at 10 MHz, what is its overflow period? Show your work.**
A 24-bit timer overflows after 2^24 ticks. At a rate of 10 MHz, each tick lasts 100ns, or 1/(10x10^6). The overflow period would then be: (2^24)/(10x10^6) = 16,777,216/10,000,000 = 1.6777216s.

**5. Describe the SysTick timer on the MSP432P401R microcontroller. Provide two example applications for SysTick in embedded systems. Which clock sources can the SysTick timer use and how can they be selected?**

**6. How many registers does the SysTick timer have on the MSP432P401R microcontroller and what is the purpose of each? Name them and provide a short description per register.**

**7. Describe the Timer_A peripheral on the MSP432P401R microcontroller. List the main operating modes of Timer_A and briefly explain each.**

**8. Briefly state the purpose of the following Timer_A registers.**
• TAxCTL
• TAxCCTLn
• TAxR
• TAxCCRn
• TaxIV
• TAxEX0

**9. What is PWM? Provide at least three example applications that use PWM in embedded systems.**

**10. How many Timer_A modules are available and how many PWM outputs can each module provide?**

**11. (25 pts) Describe the steps needed to initialize P2.4 as a PWM output driven by Timer_A0 CCR1 (TA0.1).**
**Use the Timer_A2_PWM.c driver provided in Lab 1 (Motor Control) as a reference.
Include C code such that:**
• The P2.4 pin is configured to use its primary module function (Timer_A output)
• SMCLK is selected as the clock source for Timer_A
• The timer clock is divided by 2
• Up/down mode is selected
• The output mode is configured as Toggle / Reset by setting the appropriate bits of the OUTMOD field in the CCTL[1] register
• The PWM signal has a period of 20 ms and a duty cycle of 50%

**12. Describe the steps needed to configure Timer_A0 to generate a periodic interrupt every 2 ms with an interrupt priority level of 2. Note that Timer_A0 has an interrupt number of 8. Use the Timer_A0_Interrupt.c driver provided in Lab 1 (Motor Control) as a reference.**
Include C code such that:
• SMCLK is selected as the clock source for Timer_A with a prescaler value of 1 (which means the ID field will be 00b)
• The TAIDEX field in the TAxEX0 register has a value of 000b (divide by 1)
• Up mode is selected
