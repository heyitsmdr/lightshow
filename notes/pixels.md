# Pixels

## Smart Pixels

A typical controllable pixel has 3 DMX light channels; one for each primary color. This is known as a "smart pixel". According to DMX standard, there can be 512 channels in a "universe". Since 3 doesn't divide evenly into 512, the channel maximum is considered to be 510 per universe. This means there can be 170 pixels per universe:

```
Universe = (~510 channels) = 170 pixels
```

## Controller

* CPU: **HinksPix Pro V2**
* Max Number of SPI Output Ports: 3x16 (48)
* Max Number of Pixels per Port: 680
* Max Pixels: 32,640

### Local SPI

The local SPI ports can support 680 pixels each (exclusive of power). This is based on the **Max Number of Pixels per Port** stat above, provided by the CPU.

### Long Range

Each long range CAT5 port can connect to one or more (daisy-chained) long range receivers. Each receiver has 4 local SPI ports. For a given chain (off of a single CAT5 port from the controller), all of the ports in a particular position must not exceed the **Max Number of Pixels per Port** stat above, provided by the CPU. For example, if you have two long range receivers daisy-chained together, port 1 on both receivers cannot exceed 680 pixels. If you have five receivers daisy-chained together, the combination of pixels on port 1 across all five receivers cannot exceed 680 pixels.

Long range receivers always have 4 ports. The 8 port model is just two of the 4-port receivers next to each other. The 16 port model is 4 of the 4-port receivers _on a single board_ (but is functionally no different than 4x 4-port receivers). Watch the YouTube video in the reference of this doc for an in-depth explanation of long-range ports and their limitations.

## Power

Now that the data side of the limitations are understood, there's also a consideration for power which will likely affect limitations.

* 5 amps maximum (fused) per output
    * Wattage
        * 5v: 25 watts
        * 12v: 60 watts 

### LEDs

The wattage of a pixel is it's current draw multiplied by the voltage. With WS2811 pixels, they cannot exceed 0.0555 amps at 100% brightness. At 12 volts, that's 0.666 watts at maximum brightness per pixel. This isn't exact though, check the product description for actual power consumption.

Here's a good tool for figuring out voltage drops over a particular distance, as well as total amp load:

http://spikerlights.com/calcpower.aspx

As an example, a 50-pixel string at 12 volts and 0.66 watts per pixel with pixels spaced out 3 inches apart, we get:

```
(50 pixels) * (0.66 watts @ 100% brightness) = 33 watts
33 watts / 12v = 2.75 amps
```

Be sure to use the tool above to also factor in total distance of the strip to ensure voltage drops are nominal. If voltage drops too much (i.e. greater than a 20% reduction in voltage), we'll have to power inject in the middle of the string.

## Reference

* https://www.youtube.com/watch?v=H41tr1gd2Y4&t=50s
* https://www.holidaycoro.com/kb_results.asp?ID=181
* https://auschristmaslighting.com/threads/pixels-per-power-supply.14247