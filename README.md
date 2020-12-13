# Appliance HAT Mini

* [Web GUI Live Demo](https://io.plasmadan.com/appliancehatmini/)
* [Easy Installer](#easy-installer)
* [Arduino Wiring](#arduino-wiring)
* [Setup Guide](https://github.com/plasmadancom/HAT-GUI/#setup-guide)

A Raspberry Pi Zero size I/O automation board with 2 opto-isolated quick connect power relays. Designed for switching high power loads such as industrial equipment or appliances. Ideally suited to automation or industrial control applications.

Unlike similar products, Appliance HAT Mini does not require any screw terminals or PCB wire connections. Instead it uses quick connect power relays with integrated spade terminals, meaning we have more space for relays.

## Features

* 2 opto-isolated quick connect power relays
* Easy to use [interactive web GUI](#interactive-web-gui)
* Based on the MCP23017 16-port [GPIO expander](#built-in-gpio-expander)
* Jumper selectable [I2C address](#i2c-addressing) & [GPIO voltage](#device-compatibility) (3.3V / 5V)
* Up to 16A @ 250V
* Can be used with 3.3V or 5V I2C host devices (eg, [Arduino](#arduino-wiring))

## Interactive Web GUI

Once installed on your Raspberry Pi, this interactive GUI allows quick &amp; easy control of your Appliance HAT Mini without the need for any coding. It is designed to be both a user guide &amp; quick reference to the Appliance HAT Mini pinout. The GUI is fully responsive and adapts to any screen size.

Check-out the [Live Demo.](https://io.plasmadan.com/appliancehatmini/)

## Easy Installer

Our easy installer takes care of the setup process automatically.

```
sudo wget https://git.plasmadan.com/install.sh
sudo sh install.sh
```

This script will automatically enable I2C, install the required packages and setup the Web GUI.

Alternatively, you can install manually. See our [setup guide](https://github.com/plasmadancom/HAT-GUI/#setup-guide).

## Built-in GPIO Expander

Featuring the well-documented MCP23017 16 channel GPIO expander, Appliance HAT Mini is easy to setup and control via I2C. Channels 0-1 (Group A) are utilised for the relays, giving you an extra 14 GPIOs for use with your project.

Easy integration with [Home Assistant](https://www.home-assistant.io/integrations/mcp23017/).

## Arduino Wiring

We built Appliance HAT Mini to work with any device featuring an I2C bus. It can be used with either 3.3V devices (eg, Raspberry Pi) or 5V devices (eg, Arduino); by selecting the appropriate jumper (see [device compatibility](#device-compatibility)).

## Maximum Ratings

* 16A @ 250V AC (ambient temperature)

Exceeding these limits may overload the relays.

See [relay datasheet](https://github.com/plasmadancom/Appliance-HAT-Mini/blob/main/docs/RZF1-1A6-L005-datasheet.pdf) for full details.

## DC Switching

DC is much more difficult to switch compared to AC. Appliance HAT Mini is not rated to switch DC since it uses AC relays, however provided you stick to **low** voltages and keep the current reasonable, you should be fine. However this is entirely at your own risk and will likely reduce the operational life of the relays. We recommend a **maximum** 10A @ 30V DC.

Alternatively try our [CTRL HAT](https://github.com/plasmadancom/CTRL-HAT) boards which work with DC power-MOSFETs.

## Electrical Safety

Mains voltage electricity is extremely dangerous. There is significant risk of death through electrocution, fire or explosion if not wired and fused correctly.

If using with mains voltages Appliance HAT Mini must be installed in an electrically insulated enclosure by a qualified electrician and maintain at-least a 2mm air gap between all conductive parts of the Raspberry Pi ([source](http://www.creepage.com)).

## Isolating the Relays

Removing the LINK jumper from Appliance HAT Mini will disconnect 5V power to the relays. This allows you to power the relays from a dedicated supply if required.

## Back-Powering *

Using a decent power supply, such as the official Raspberry Pi adaptor, you can expect to pull around 1.5A from the 5V pins on a Raspberry Pi. You can use up to 8 Appliance HAT Minis with a single Raspberry Pi. That's up to 16 relays, 16 LEDs and 8 GPIO expanders which all need power. It's easy to see how quickly we can go over the limit, especially if the GPIO expanders are used to drive other devices. Back-powering can solve this.

The relays on Appliance HAT Mini can be back-powered via the 3.5mm pitch screw terminal.

__* Note: Back-powering is for Appliance HAT Mini, not for Raspberry Pi. Remove the LINK jumper when back-powering to avoid damaging your Pi.__

## I2C Addressing

| Address | A2 | A1 | A0 |
| :---: | :---: | :---: | :---: |
| 0x20 | | | |
| 0x21 | | | &#x2B1B; |
| 0x22 | | &#x2B1B; | |
| 0x23 | | &#x2B1B; | &#x2B1B; |
| 0x24 | &#x2B1B; | | |
| 0x25 | &#x2B1B; | | &#x2B1B; |
| 0x26 | &#x2B1B; | &#x2B1B; | |
| 0x27 | &#x2B1B; | &#x2B1B; | &#x2B1B; |

## Device Compatibility

Appliance HAT Mini is fully compatible with all **40-way** Raspberry Pi models and clones.

| Device Model | Compatibility |
| --- | :---: |
| Raspberry Pi 1 Model A+/B/B+ | &#x2714;&#xFE0F; |
| Raspberry Pi 2 Model B | &#x2714;&#xFE0F; |
| Raspberry Pi 3 Model B+ | &#x2714;&#xFE0F; |
| Raspberry Pi 4 | &#x2714;&#xFE0F; |
| Raspberry Pi Zero | &#x2714;&#xFE0F; |
| Asus Tinker Board | &#x2714;&#xFE0F; |
| Orange Pi | &#x2714;&#xFE0F; |
| Odroid | &#x2714;&#xFE0F; |
| ATMegaZero | &#x2714;&#xFE0F; |

To use with Arduino or any other 5V device the 3V3 jumper must be moved to 5V. Use the SDA &amp; SDL breakout pins for I2C communication.

## Dimensions


<p align="center">
    <a href="https://raw.githubusercontent.com/plasmadancom/Appliance-HAT-Mini/master/img/appliance-hat-mini-v1.0-dimensions.svg">
        <img alt="Mechanical Drawing" src="/img/appliance-hat-mini-v1.0-dimensions.svg" width="500">
    </a>
</p>

## Where to Go From Here

Integrating Appliance HAT Mini with your own projects is easy, just follow any guide which uses the MCP23017 expander. We have provided some example Python scripts to get you started (see [here](https://github.com/plasmadancom/Appliance-HAT-Mini/tree/master/python_examples)).

Integration with [Home Assistant](https://www.home-assistant.io/integrations/mcp23017/) is easy thanks to the MCP23017.

## License

MIT © Dan Jones - [PlasmaDan.com](https://plasmadan.com)
