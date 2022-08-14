# Raspberry Pi Pico Polyphonic DCO and DAC

This board was modified from the original Pico DCO to act as a secondary DCO board to provide 2 DCO's per voice, as the first DCO board has gate outputs these were not deemed necessary on the second DCO board. This board does not have a MIDI input and takes its MIDI signal from the first board via a buffer, stacking controls are also shared between the 2 boards. Detune and FM inputs are currently seperate, but I think the FM inputs can be linked.

This repository contains source code, schematics for a digitally controlled oscillator (DCO) with up to 6 voices which are driven by a Raspberry Pi Pico. It uses PIO to generate a highly accurate frequency which is controlled by USB or serial MIDI. The analog oscillator part is based on the Juno 106 and generates sawtooth and square wave signal with a 10Vpp amplitude. Amplitude compensation is done by a smoothed PWM signal coming from the Pico. Additionally I have removed the gate signals and added an 8 channel DAC to provide the 6 CV's that would normally be available for filter tracking etc. This also makes the board into a 6 note polyphonic MIDI to CV converter. Additionally with the help of Freddie Renyard an FM input is now available. Also an octave select switch allowing a 3 octave adjustment of the DCO's range.

## Key features

- Digitally controlled analog oscillator using a Raspberry Pi Pico
- Up to six voices
- Voice stacking
- Detuning of voices
- USB MIDI input
- MIDI pitch bend
- Portamento with adjustable speed
- FM input
- V/oct outputs for each note
- Octave switching

## The source of the inspiration for these modifications and acknowledgements

Pico DCO also known as Jan Knipper

https://github.com/polykit/pico-dco

This is how it sounds: [Ramp sample](https://soundcloud.com/polykit/pico-dco-ramp) [Pulse sample](https://soundcloud.com/polykit/pico-dco-pulse) [Polyphonic sample](https://soundcloud.com/polykit/pico-dco-polyphonic)

Freddie Renyard for his coding of the FM inputs and patience with me whilst I debugged the voice sync of two boards together.

https://github.com/freddie-renyard

## Installation (simple)

Press `BOOTSEL` button on the Pico while powering it with USB. Copy file `build/pico-dco-dac.uf2` onto the USB mass storage device.

## Usage

After installing the Pico should register as USB MIDI device. Alternatively serial MIDI input is available. The DCO listens to note on/note off messages on MIDI channel 1. Pitch bend is also supported. Portamento can be enabled by MIDI CC message #65, portamento time can be adjusted by CC message #5.

## References

https://blog.thea.codes/the-design-of-the-juno-dco/

https://electricdruid.net/roland-juno-dcos/

https://www.youtube.com/watch?v=yYnQYF_Xa8g

https://github.com/raspberrypi/pico-examples/tree/master/pio/pwm

https://github.com/raspberrypi/pico-examples/tree/master/pio/pio_blink

https://github.com/raspberrypi/pico-examples/tree/master/pwm/hello_pwm

https://qiita.com/jamjam/items/f2fdd5c072ff348fd809

https://github.com/infovore/pico-example-midi

https://learn.sparkfun.com/tutorials/midi-tutorial/all

http://www.music-software-development.com/midi-tutorial.html

http://midi.teragonaudio.com/tech/midispec/run.htm
