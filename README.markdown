# I2C Barometric Sensor Project - MPL115A2
## Embedded Philly


# Overview

This document outlines the project goals for developing a set of code
resources for easy, platform independent functionality of the MPL115A2
barometric pressure sensor.

# Project Components

This project has three major components. The interface should be
designed first. The barometric sensor protocol & and lower level I2C
driver can be implemented in parallel, provided those working on it have
agreed on the interface ahead of time.

## Design of an I2C Hardware Abstracted Interface

This will be a common interface that can be used across platforms that
support I2C communication. It will likely be in the form of a .h file
that makes use of all the functionality of the communication interface.

To complete this part of the project, you should do some research on I2C
communication standards, and determine the best way to support all the
functionality of the protocol.

I2C can operate in several modes. You will only need to use one of these
modes for this project, but make sure your interface will be able to
support all of the modes of the protocol for any future uses of the
interface in other projects.

## Implementation of the Barometric Pressure Sensor Protocol Using the
I2C Interface

This will be a module that assumes the I2C driver already exists, and,
given the functionality in the interface, creates an easy to use
interface & implementation for the sensor itself. 

For example, Table 5 of the datasheet outlines 6 I2C commands that can
be used to read information from the sensor. Implement an interface that
uses the I2C hardware interface to create this higher-level protocol. 

This is the kind of module that should be implemented using TDD. Since
you have function stubs for all of the hardware abstraction interface
functions, you will be able to fake these functions using Ceedling.

## Implementation of the I2C Hardware Abstracted Interface

This is the module that will use hardware level access functions for the
board you are working on. Implement all the functions in the interface
so that from outside of the interface, you don't need to know anything
about the interiors of the chip.

Many of these functions may already be implemented by the chip
manufacturer, but it is important to abstract them to a common interface
so that the higher-level barometric pressure module can be used
independently of the lower level functions of the chip. This keeps the
sensor platform agnostic

This portion of the project will likely need to be tested using a logic
analyzer and the hardware itself, which we have available.

# End Results & Directory Structure

This project should result in 4 files:

1. `I2C_HAL.h` -> This should be placed in the HALinterfaces repository
2. `[platform]_I2C.c` -> This will implement I2C_HAL.h and will live in
   a repository for a library specific to your platform.
3. (and 4) `BarometricSensor.c` & `BarometricSensor.h` -> These will live in a
   sensor repository.

For the purposes of development, all the files are included in this
repository. We will deprecate this repository once the project has been
completed.

For now, all files can be found in this repository, in the respective
src/ and inc/ folders. 

In the doc/ folder, you can find the datasheet for the chip.
