# Introduction to COINES

COINES ("**CO**mmunication with **IN**ertial and **E**nvironmental **S**ensors") provides a low-level interface to Bosch Sensortec’s Application Board.
The user can access Bosch Sensortec’s MEMS sensors through a C interface.
COINES can be used with SensorAPI of the sensor. SensorAPI is available at [https://github.com/BoschSensortec](https://github.com/BoschSensortec).
The source code of example applications and SensorAPI are provided with the COINES library as a package.
The user can modify, compile and run the sample applications.

COINES can be used to see how to use the SensorAPI in an embedded environment and allows convenient data logging.

The full working environment consists of:

- A Bosch Sensortec MEMS sensor on a shuttle board mounted on the socket of Bosch Sensortec’s application board APP2.0/APP3.0
- Windows or Linux PC to which the Application Board is connected via USB
- COINES software release as found here: (http://www.bosch-sensortec.com)[http://www.bosch-sensortec.com]
- C compiler is also required (details see below)