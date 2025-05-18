---
tags:
  - y2s2-MA2079
status: Ongoing
---
## Writing the code
The source(code) of our product's intellect. 
### Initial code
by Hankertrix - in micropython
```python
# Code to run the raspberry pi pico

# Imports
from machine import PWM, Pin

# Constants

# The motor frequency.
# The PWM frequency should be roughly 10 times
# this frequency to ensure a smooth change in motor speed.
MOTOR_FREQUENCY = 250

# The maximum number of button presses.
# This variable determines the number
# of different speeds the motor has.
#
# The number of LEDs should also match
# up with this number so each motor speed
# has an indicator.
MAX_BUTTON_PRESSES = 3

# Motor driver pins
MOTOR_DRIVER_PIN_1 = 6
MOTOR_DRIVER_PIN_2 = 5
MOTOR_DRIVER_ENABLE_PIN = 4

# LED pins
LED_1_PIN = 25
LED_2_PIN = 26
LED_3_PIN = 27

# The switch pin
SWITCH_PIN = 29

# The bus pin for the pull up resistor
V_BUS_PIN = 40


def setup() -> dict[int, Pin]:
    "The setup function to setup the Raspberry Pi"

    # The dictionary of pins
    pins = {}

    # Set up all the pins
    for pin_number in (
        MOTOR_DRIVER_PIN_1,
        MOTOR_DRIVER_PIN_2,
        MOTOR_DRIVER_ENABLE_PIN,
        LED_1_PIN,
        LED_2_PIN,
        LED_3_PIN,
        V_BUS_PIN,
        SWITCH_PIN,
    ):
        #

        # Add the pin to the dictionary
        pins[pin_number] = Pin(pin_number)

    for pin_number in (
        MOTOR_DRIVER_ENABLE_PIN,
        LED_1_PIN,
        LED_2_PIN,
        LED_3_PIN,
        V_BUS_PIN,
    ):
        #

        # Set up the pin as an output pin
        pins[pin_number].init(Pin.OUT).value(0)

    # Set up the motor driver pins
    for pin_number in (MOTOR_DRIVER_PIN_1, MOTOR_DRIVER_PIN_2):
        #

        # Get the pwm object
        pwm = PWM(pins[pin_number], freq=MOTOR_FREQUENCY * 10)

        # Add the pwm object to the dictionary
        pins[pin_number] = pwm

    # Add the switch pin to the dictionary
    pins[SWITCH_PIN].init(Pin.IN)

    # Set the V Bus pin to high
    pins[V_BUS_PIN].value(1)

    # Return the dictionary of pins
    return pins


def main() -> None:
    "The main function to run"

    # Initialise the number of button presses
    button_presses = 0

    # Get the pins
    pins = setup()

    # Infinite loop to keep running
    while True:
        #

        # Get whether the switch is pressed
        switch_pressed = pins[SWITCH_PIN].value()

        # If the switch is not pressed, continue the loop
        if switch_pressed != 1:
            continue

        # Otherwise, increment the button presses
        button_presses = (button_presses + 1) % (MAX_BUTTON_PRESSES + 1)

        # Get the duty cycle for the PWM
        duty_cycle = (button_presses * 100) // MAX_BUTTON_PRESSES

        # Get the duty cycle in terms of 0 - 1023,
        # which is what MicroPython supports
        duty_cycle = duty_cycle * 1023 // 100

        # Set the motors to the duty cycle
        for pin_number in (MOTOR_DRIVER_PIN_1, MOTOR_DRIVER_PIN_2):
            #

            # Set the duty cycle
            pins[pin_number].duty(duty_cycle)


# Name safeguard
if __name__ == "__main__":
    main()

```

### Revised code
by Hankertrix - in micropython
```python
# Code to run the raspberry pi pico

# Imports
import time

from machine import PWM, Pin

# Constants

# The maximum value for an unsigned 16 bit integer
U16_MAX = 65535

# The motor frequency.
# The PWM frequency should be roughly 10 times
# this frequency to ensure a smooth change in motor speed.
MOTOR_FREQUENCY = 250

# The maximum number of button presses.
# This variable determines the number
# of different speeds the motor has.
#
# The number of LEDs should also match
# up with this number so each motor speed
# has an indicator.
MAX_BUTTON_PRESSES = 3

# Pins on the Raspberry Pi Pico.
#
# Note that all the pins are the GPIO pin numbers,
# not the physical pin numbers on the Raspberry Pi Pico.

# Motor driver pins
MOTOR_DRIVER_PIN_1 = 4
MOTOR_DRIVER_PIN_2 = 3

# LED pins
LED_1_PIN = 19
LED_2_PIN = 21
LED_3_PIN = 20

# The switch pin
SWITCH_PIN = 22


def setup() -> dict[int, Pin | PWM]:
    "The setup function to setup the Raspberry Pi"

    # The dictionary of pins
    pins = {}

    # Set up all the pins
    for pin_number in (
        MOTOR_DRIVER_PIN_1,
        MOTOR_DRIVER_PIN_2,
        LED_1_PIN,
        LED_2_PIN,
        LED_3_PIN,
        SWITCH_PIN,
    ):
        #

        # Add the pin to the dictionary
        pins[pin_number] = Pin(pin_number)

    for pin_number in (
        LED_1_PIN,
        LED_2_PIN,
        LED_3_PIN,
    ):
        #

        # Get the pin
        pin = pins[pin_number]

        # Set up the pin as an output pin
        pin.init(Pin.OUT)

        # Set the value to be low
        pin.value(0)

    # Set up the motor driver pins
    for pin_number in (MOTOR_DRIVER_PIN_1, MOTOR_DRIVER_PIN_2):
        #

        # Get the pwm object
        pwm = PWM(pins[pin_number], freq=MOTOR_FREQUENCY * 10)

        # Initialise the PWM to 0
        pwm.duty_u16(0)

        # Add the pwm object to the dictionary
        pins[pin_number] = pwm

    # Initialise the switch pin to be an input
    pins[SWITCH_PIN].init(Pin.IN)

    # Return the dictionary of pins
    return pins


def main() -> None:
    "The main function to run"

    # Initialise the number of button presses
    button_presses = 0

    # Get the pins
    pins = setup()

    # Infinite loop to keep running
    while True:
        #

        # Sleep for a bit to make the switch easier to control
        time.sleep(0.2)

        # Get whether the switch is pressed
        switch_pressed = pins[SWITCH_PIN].value()

        # If the switch is not pressed, continue the loop
        if switch_pressed != 0:
            continue

        # Otherwise, increment the button presses
        button_presses = (button_presses + 1) % (MAX_BUTTON_PRESSES + 1)

        # If the number of button presses is 0, turn off all the LEDs
        if button_presses < 1:
            #

            # Turn off the motors
            for pin_number in (MOTOR_DRIVER_PIN_1, MOTOR_DRIVER_PIN_2):
                #

                # Set the duty cycle
                pins[pin_number].duty_u16(0)

            # Iterate over all the LEDs
            for pin_number in (LED_1_PIN, LED_2_PIN, LED_3_PIN):
                #

                # Turn off the LED
                pins[pin_number].value(0)

            # Continue the loop
            continue

        # Light up the LEDs
        for pin_number in (LED_1_PIN, LED_2_PIN, LED_3_PIN)[:button_presses]:
            #

            # Light up the LED
            pins[pin_number].value(1)

        # Get the duty cycle for the PWM
        duty_cycle = (button_presses * 100) // MAX_BUTTON_PRESSES

        # Get the duty cycle in terms of 0 - U16_MAX,
        # which is what MicroPython supports
        duty_cycle = duty_cycle * U16_MAX // 100

        # Set the motors to the duty cycle
        for pin_number in (MOTOR_DRIVER_PIN_1, MOTOR_DRIVER_PIN_2):
            #

            # Set the duty cycle
            pins[pin_number].duty_u16(duty_cycle)


# Name safeguard
if __name__ == "__main__":
    main()

```