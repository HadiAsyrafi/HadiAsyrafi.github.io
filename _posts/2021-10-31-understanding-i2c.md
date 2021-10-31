---
title: Understanding I2C
author: Hadi Asyrafi
date: 2021-10-31 15:30:00 +0800
categories: [Protocol, Serial]
tags: [sniffing]
image:
    src: /assets/images/I2C-Block-Diagram.jpg
    width: 1000
    height: 400
    alt: I2C Block Diagram 
---

This post is to share about I2C & how it is used for communication. I2C is used in variety of application. In this example we're going to use I2C EEPROM for demonstration.


## Introduction to I2C

I2C is a very popular serial communication protocol which are used a lot in embedded devices. Hence, it is really useful to get familiarize with this protocol is this can be and important tool to "glance" into and "exploit" our target device.

### Architecture

Similar to UART, I2c operates using only 2 wires to transmit data between devices:
![i2c-master-slave](/assets/images/I2C-Single-Master-Single-Slave.png){: width="1086" height="542"}

SDA - Serial Data   : Transmit / receive data  
SCL - Serial Clock  : Carries clock signal

### Inner Working
As I2C is a synchronous protocol, data is interpretated based on the sampling of Serial Data during the toggling of Serial Clock. Hence, it is necessary for both master & slave to operate on similar clock frequency.

Each I2C communication can be thought of as a stream of messages & each messages consist of multiple frames 8-bits each. Each messages starts with a Start condition, and terminated by a Stop condition
![i2c-message](/assets/images/I2C-Message-Frame.png){: width="1086" height="542"}

Start condition : Master pulls SDA low, while SCL is kept high  
Stop condition  : Master pulls SDA high, while SCL is kept high  
Address frame   : Unique address that identifies the slave intended for communication
Read / Write bit: 0 - Write, 1 - Read  
ACK / NACK bit  : Each frame is followed by ACK/NACK to indicate success  


## Sniffing I2C
Described in this section is an exercice to sniff I2C courtesy of Practical Hardware Pentesting by Jean-Georges Valle

