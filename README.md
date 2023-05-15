# FXDSP — A WhateverDSP based guitar pedal

FXDSP is an easily programmable DSP platform in a familiar guitar pedal form factor:

![FXDSP collage](https://github.com/NuclearLighthouseStudios/FXDSP/assets/55932282/bf53b1a2-d097-4020-ba48-dbba893ccc19)

It's based around an STM32F405 microcontroller and runs on the [WhateverDSP framework](https://github.com/NuclearLighthouseStudios/WhateverDSP), offering low latency audio processing and fully class complicant USB audio and MIDI support.

FXDSP has interchangeable user interface PCBs so it can easily be tailored to the needs of each effect produced on the platform.

## Example code

Here is what that a simple volume control that scales the audio level using a potentiometer looks like:

```c
#include <libwdsp.h>

void wdsp_process(float *in_buffer[BLOCK_SIZE], float *out_buffer[BLOCK_SIZE])
{
	float volume = io_analog_in(POT_1);

	for (int i = 0; i < BLOCK_SIZE; i++)
	{
		float l_sample = in_buffer[0][i];
		float r_sample = in_buffer[1][i];

		out_buffer[0][i] = l_sample * volume;
		out_buffer[1][i] = r_sample * volume;
	}
}

```

Check out the [examples repository](https://github.com/NuclearLighthouseStudios/WhateverDSP-Examples) for more, or [come chat with us on Discord or IRC](https://github.com/NuclearLighthouseStudios/FXDSP#chat).

## Chat

- Discord: [Join link](https://discord.gg/UFeqgzfaba) 
- IRC: irc.libera.chat `#wdsp`

For more information, please see the [WhateverDSP repository](https://github.com/NuclearLighthouseStudios/WhateverDSP).
