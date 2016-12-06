# labuino
Graphical arduino lab.

It's my perception that many Arduino projects are fairly simple. A few
input devices, a few output devices and some code to hold it all
togehter.

It's also my perception that the code part is the tricky bit for many
newcomers.

My intention with labuino is to explore a graphical representation of
devices and events that drives such arduino projects and see if it may
in fact be a useful way of expressing simple projects.

There is a second motivating force behind this. And that is teaching
kids to code. I feel that there is a gap between scratch that is used
successfully to introduce kids to programing. But the step towards
programing in other environments is large. I hope to incorporate
scratch-like programing into labuino to give a real world, tangible
use for someone already versed in scratch.

Finally, a byproduct of a labuino project should be a readable working
sketch so that the "real" code behind it can be studied.

# Interface

The main tool of labuino will be a workspace where you can place
modules. The modules can either be representation of hardware
components, such as a button or a LED, or they can be interconnecting
logic functions driven by the arduino processor, such as a timer,
sequencer or memory.

Each module will have one or more input nodes or output nodes. The
nodes can be connected to eachother showing a route for a signal.

A signal is either a momentary on or off or something more complex
such as a numerical value, text or complex object.

Example:

    Button --> Timer --> LED    Light Sensor --> Beeper

## Proposed modules

* Button

  A momentary or maintained switch with one output, either on or off.

* LED

  A light emitting diode, one input. Could be simple such as on or off
  but variants that accept a value for brightness or even RGB is
  conceivable.
   
* Knob (potentiometer) / Stepwise knob

  A rotary switch, one output. Either a continous output within a
  range or a stepwise switch with a given number of positions.

* Sequencer

  A programmable set of steps with values with programmable delays
  between. Can either be defined with fixed values or programmable via
  some input pins. Could act as a pure shift register or have input
  for each step in the sequence.

* Multiplexer (Mux)

  Accepts several input but only one is chosen for output at a given
  time. Selecting input could be done in sequence or with a value.

* Demux

  Accepts one input and has multiple outputs, but only one is active
  at a given time. Output is select as with the Mux.

* Memory Cell

  Stores a value that can be read on an output ping.

* Timer

  Accepts one input pin

* Counter

  One input pin, counts the number of time the input pin is on. Can be
  read like a memory cell.

* Segment display

  Accepts one input value and displays it. Could optionally be read.

* Motor

  Could be a servo, stepper motor or continous motor. Various input
  control speed and/or distance traveled.

* Sensors

  Any type of sensor that can give a value. Light, Sound, Moisture,
  Current.

* Code block

  The icing on the cake. Some form of code must be possible to handle
  cases to complex for simple wiring. Perhaps the code could emit to
  given "output" pins. Perhaps manipulate other modules by name. This
  certainly needs further thought.

## Signals or pulses

The system overall is event driven. Something will happen that triggers a pulse. Consider the following simple diagram

    Button --> Memory Cell --> Segment display

In this case, the button will trigger memory cell to ouput it's value
in a pulse to a segment display which will be visibly updated.

Extend this to:

             Rotary Switch
                   |
                   v
    Button --> Memory Cell --> Segment display

In this example the Rotary Switch will puls it's value each time it
changes and update the Memory Cell. The Memory Cell however will not
update segment display unless triggered by the button. It could
perhaps be convenient to configure the Memory Cell to be "pass
through" that is it will both be updated and trigger an update of the
Segment Display.