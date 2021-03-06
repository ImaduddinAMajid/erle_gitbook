# radio.pde

Link to the code: [radio.pde](https://github.com/diydrones/ardupilot/blob/master/APMrover2/radio.pde).
In this file you can find functions for dealing with the radio signals and channels.

```cpp
// -*- tab-width: 4; Mode: C++; c-basic-offset: 4; indent-tabs-mode: nil -*-

/*
  allow for runtime change of control channel ordering
 */
static void set_control_channels(void)
{
    channel_steer    = RC_Channel::rc_channel(rcmap.roll()-1);
    channel_throttle = RC_Channel::rc_channel(rcmap.throttle()-1);
    channel_learn    = RC_Channel::rc_channel(g.learn_channel-1);

	// set rc channel ranges
	channel_steer->set_angle(SERVO_MAX);
	channel_throttle->set_angle(100);
}
...
```
This slice of code stablish a channel for steer, another for throttle and another for learn.For the first two, also stablish the range.

```cpp

static void init_rc_in()
{
	// set rc dead zones
	channel_steer->set_default_dead_zone(30);
	channel_throttle->set_default_dead_zone(30);

	//set auxiliary ranges
    update_aux();
}
...
```
This function sets the defauld dead zones for the throttle and steer channels. Also set a auxiliar range.
```cpp
static void init_rc_out()
{
    RC_Channel::rc_channel(CH_1)->enable_out();
    RC_Channel::rc_channel(CH_3)->enable_out();
    RC_Channel::output_trim_all();

    // setup PWM values to send if the FMU firmware dies
    RC_Channel::setup_failsafe_trim_all();
}
...
```

This slice of code enablesthe output in the channels 1 and 3. Also sets the failsafe event.

```cpp

static void read_radio()
{
    if (!hal.rcin->new_input()) {
        control_failsafe(channel_throttle->radio_in);
        return;
    }
    ...
    ```
Here we find the `read_radio`function. First of all detects if there is a `new_input()`.
```cpp
    failsafe.last_valid_rc_ms = hal.scheduler->millis();

    RC_Channel::set_pwm_all();

	control_failsafe(channel_throttle->radio_in);

	channel_throttle->servo_out = channel_throttle->control_in;
...
```
This slice of code enables the `set_pwm_all()`function imlemented in [/libraries/RC_Channel/RC_Channel.cpp](https://github.com/diydrones/ardupilot/blob/master/libraries/RC_Channel/RC_Channel.cpp#L169).Also control failsafe evetns.


```cpp
if (abs(channel_throttle->servo_out) > 50) {
        throttle_nudge = (g.throttle_max - g.throttle_cruise) * ((fabsf(channel_throttle->norm_input())-0.5) / 0.5);
	} else {
		throttle_nudge = 0;
	}

    if (g.skid_steer_in) {
        // convert the two radio_in values from skid steering values
        /*
          mixing rule:
          steering = motor1 - motor2
          throttle = 0.5*(motor1 + motor2)
          motor1 = throttle + 0.5*steering
          motor2 = throttle - 0.5*steering
        */

        float motor1 = channel_steer->norm_input();
        float motor2 = channel_throttle->norm_input();
        float steering_scaled = motor1 - motor2;
        float throttle_scaled = 0.5f*(motor1 + motor2);
        int16_t steer = channel_steer->radio_trim;
        int16_t thr   = channel_throttle->radio_trim;
        if (steering_scaled > 0.0f) {
            steer += steering_scaled*(channel_steer->radio_max-channel_steer->radio_trim);
        } else {
            steer += steering_scaled*(channel_steer->radio_trim-channel_steer->radio_min);
        }
        if (throttle_scaled > 0.0f) {
            thr += throttle_scaled*(channel_throttle->radio_max-channel_throttle->radio_trim);
        } else {
            thr += throttle_scaled*(channel_throttle->radio_trim-channel_throttle->radio_min);
        }
        channel_steer->set_pwm(steer);
        channel_throttle->set_pwm(thr);
    }
}
...
```
The functions in this part of the codeare set in order to adapt the inputs to the outputs in the channels defined above.

```cpp

static void control_failsafe(uint16_t pwm)
{
	if (!g.fs_throttle_enabled) {
        // no throttle failsafe
		return;
    }

	// Check for failsafe condition based on loss of GCS control
	if (rc_override_active) {
        failsafe_trigger(FAILSAFE_EVENT_RC, (millis() - failsafe.rc_override_timer) > 1500);
	} else if (g.fs_throttle_enabled) {
        bool failed = pwm < (uint16_t)g.fs_throttle_value;
        if (hal.scheduler->millis() - failsafe.last_valid_rc_ms > 2000) {
            failed = true;
        }
        failsafe_trigger(FAILSAFE_EVENT_THROTTLE, failed);
	}
}
...
```
You may have notice, that this function is called above.This function checks the failsafe events.
First checks if the throttle is enabled.Then checks if there is loss of GCS control.

```cpp
static void trim_control_surfaces()
{
	read_radio();
	// Store control surface trim values
	// ---------------------------------
    if (channel_steer->radio_in > 1400) {
		channel_steer->radio_trim = channel_steer->radio_in;
        // save to eeprom
        channel_steer->save_eeprom();
    }
}
...
```
This function saves in EEPROM memory the values for the `channel_steer`.By calling [save_eeprom()](https://github.com/diydrones/ardupilot/blob/master/libraries/RC_Channel/RC_Channel.cpp#L240).

```cpp
static void trim_radio()
{
	for (int y = 0; y < 30; y++) {
		read_radio();
	}
    trim_control_surfaces();
}
```
This function calls `read_radio()`until y variable reach 30. Then calls `trim_control_surfaces()`for setting them.

