---
title: "Magspoof – Wirelessly Spoof Magnetic Stripereaders"
date: "2020-8-9"
image: assets/images/magspoof.jpg
author: name
layout: post
tags: [ magspoof, wireless, spoof, magnetic, stripreaders ]
categories: [ magspoof ]
---


<![endif]-->

MagSpoof, the credit card and magstripe spoofer.

MagSpoof is a device that can spoof or emulate any magnetic stripe or credit card and it can work wirelessly even on standard magstripe credit card readers by generating a strong electromagnetic field that emulates a traditional magnetic stripe card.

Keep in mind that MagSpoof does not enable you to use credit cards that you are not legally authorized to use.

The chip-and-pin and Amex information is not implemented, and using MagSpoof requires you to both have and own the magstirpes which you want to emulate.

Having a credit card number and expiration date is not enough to perform transactions.

MagSpoof does allow you to perform research in other areas of the field, such as microcontrollers and electromagnetism.

You can store all of your credit cards and magstripes in one device and it even works on traditional magstripe readers wirelessly without the need for NFC and RFID.

You can disable chip-and-pin and it can even correctly predict Amex credit card numbers and expirations from previous card numbers.

IT supports all three magnetic stripe tracks and even supports track 1+2 simultaneously.

It can be easily be built using Arduino or other common parts.

## Use Case

MagSpoof can be used as a traditional credit card and store all of your credit cards in various form factors.

It can also be used to conduct security research in any area that would require a magstripe such as credit card readers, drivers’ licenses, hotel room keys and automated parking lot tickets.

## How Do They Work: Magnetic Stripes

Magnetic stripes, otherwise known as magstripes are magnetic.

While the magnetic strips inside are weak, they are still strong enough to attract small ferrous particles and are wide enough to fully extract all of the data from a magstripe or credit card.

MegaSpoof emulates a magnetic stripe by quickly changing the polarization of an electromagnet, producing a magnetic field similar to that of a normal magnetic stripe, emulating it as if it is being swiped.

The magstripe reader requires no form of wireless receiver, NFC or RFID, and as such, MagSpoof can work wirelessly, even with standard magstripe readers.

The length at which it can be used is dependent on the strength of the electromagnet.

MagSpoof can also use inexpensive and off the shelf parts and can be built with an Arduino, a wire and a battery.

Electromagnets typically have an iron core; however, the core is lost in this case to provide more space and portability.

The iron core does make an electromagnet more efficient, however, without it, we can still get a level of power enough for everything to work.

By emulating a card with MagSpoof, if you send track 1 one way and track 2 reversed, every card reader will assume that you swiped a card back and forth, and the data from both tracks can be used and properly read.

Due to this, it is an extremely efficient process which requires only a single coil and works for both tracks simultaneously.

MagSpoof can also work on track 3 because of this.

## Security Level

A primary issue of the new forms of security is the fact that they are set on the “Service code” portion of the magstripe, the Chip-and-Pin part.

The service code in a credit card magstripe defines certain attributes of a card, such as if the card can dispense cash, where it can work, nationally or internationally, and if the card as a built in IC chip and if it has a pin.

If a card has a chip inside and you go to any retailer that supports chip but swipe just your magstripe, the point of sale system will ask you to dip your card for additional security.

The bits stating the card has Chip-and-Pin can be turned off from the magstripe however.

If you take a card that would normally request you to dip it, you can get away with not dipping your chip at all and perform a successful transaction, which evades the security measure.

## Card Number Prediction

The CID or CVV2 on Visa, printed on a card is protected by a secret 3DES key.

This key encrypts the Primary Account Number service code and expiration.

The service code can be determined as most cards will contain a similar service code.

CSC behaves like a CID or CVV2 on a magstripe, and continues to work for a newer predited card.

An attacker can use a stolen card’s CSC with the predicted card number and expiration date to make purchases.

To perform the transaction without gaining suspicion, the attacker can use a magswipe writer or a device like MagSpoof to load a newly devised card information onto a card.

## The Hardware

This hardware was used for the experiments, however you are free to test out and use similar hardware.

The Microcontroller is an Atmel ATtiny85 which drives the entire system by storing all of the magnetic stripe and credit card data.

The Motor Driver is a L293D H-bridge which drives the electromagnet.

Most motor drivers are driven by the electromagnets and magnets inside of them, and any standard driver should be able to get the job done.

As for the coil, you need around 24AWG magnet wire to act as the coil to produce the electromagnetic field.

This piece of wire produces an electromagnetic field which makes the card reader believe a card is being swiped.

A small 100mAh 3.7v lip battery to power the entire thing.

A 100 µF Capacitor to keep enough energy and provide the electromagnetic field with power when it needs it.

A LED to signal you when the information is transmitted.

A 100Ω Resistor to not burn out the LED and a momentary switch to indicate the electromagnet.

Finally, to solder everything together use a mini-protoboard.

## The Firmware

The source code for MegSpoof can be found from here:

[https://github.com/samyk/magspoof](https://github.com/samyk/magspoof)

It is compatible with the Arduino framework and can work on both Arduinos and ATtiny chips.

## References

- Gizmodo (https://gizmodo.com/this-tiny-device-can-wirelessly-spoof-magnetic-stripe-r-1744584039){:target="_blank"}