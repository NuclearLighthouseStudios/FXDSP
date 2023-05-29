# FXDSP — A WhateverDSP based guitar pedal

FXDSP is an easily programmable DSP platform in a familiar guitar pedal form factor:

![FXDSP collage](https://github.com/NuclearLighthouseStudios/FXDSP/assets/55932282/bf53b1a2-d097-4020-ba48-dbba893ccc19)

It's based around an STM32F405 microcontroller and runs on the [WhateverDSP framework](https://github.com/NuclearLighthouseStudios/WhateverDSP),
offering low latency audio processing and fully class complicant USB audio and MIDI support.

FXDSP has interchangeable user interface PCBs so it can easily be tailored to the needs of each effect produced on the platform.

For more information about WhateverDSP, [please see the WhateverDSP repository](https://github.com/NuclearLighthouseStudios/WhateverDSP).

## Example code

Here is a full example showing a simple volume control that scales the audio level using a potentiometer:

```c
#include <libwdsp.h>

void wdsp_init(void)
{
	io_digital_out(BYPASS_L, true);
	io_digital_out(BYPASS_R, true);
}

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

Check out the [examples repository](https://github.com/NuclearLighthouseStudios/WhateverDSP-Examples) for more,
or [come chat with us on Discord](https://github.com/NuclearLighthouseStudios/FXDSP#chat).

## Chat

[You can chat with us on Discord.](https://discord.gg/WDsFnartXb)

## License

FXDSP hardware is licensed under CC-BY-NC-SA.

The WhateverDSP library is licensed under GNU Lesser General Public License.
