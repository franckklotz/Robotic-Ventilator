# Project overview

Hello,

with key people in robotics design and Software development, a MD, and a MD Student, we decided to work on a Ventilator since the Covid-19 crisis.

Since we worked together in multiple indutrial robotic project, we called it Robotic repirator team.

We also participate to the https://www.agorize.com/en/challenges/code-life-challenge?lang=en as Robotic Team. this was a challenge to design a ventilator in a few days .

After few idea, we decided tu use an existing Manual Ventilator, AMBU ( see web site ) and control the flow using a stepper motor to precisely control air flow, volume, cylce per minute. The design can be adapted to similar AMBU compatible manual ventilator to "automate" the process of ventilating.

Thanks to Paulo Arruda and Patrick Schmitt to have "worked" some late night on brainstorming this idea / concept.

unfortunately, we could not get all parts to have a working prototype as per 31 march 2020, so we decided to share openly our idea so we can continu to build and improve around the community.

The Store Closed aroud us ( Montreal, Canada ), and delivery was jumping out of range for us to have a prototype for the 31 march 2020.

So please feel free to get inspired from this proposal and do not hesitate to improve.

do not hesitate to contact us via email for any specific questions.

# Specification

the specification are the folowing :

Pressure control up to 40 cmH2O, expiration pressure up to 25 cmH2O
Respiration ratio from 6 to 40 breath per minute
Adjustable inspiratiory time I:E ration
FiO2 from 21 to 100 % in 10 % increase 
Trigger time and or patient 
Connect to standard mask 
Dual Circuit with non rebreathing valve ( Y patient ) 

humidity and temperature not controlled in our design
O2 read out not in our design 
O2 sensor are very expensive and "impossible to find " @ end of march 2020

# Mechanical parts

The complete 3D parts and assembly is available in the specific folder. The different Ambu clone may have different dimentions but our intent is to design the claws in such way it will fit the different models destinated to support adults.
It was designed with Solidworks.

you can download a free viewer, edrawing to see the design.

the free viewer will allow you to hide parts ( like cover ) or make some parts transparent, and of course zoom in out, rotate and basic navigation around the mechanical design.

please open the AUTOMATIC AMBU ACTUATOR SYSTEM.SLDASM file to see the assembly.

PARTS :

All parts starting with a number, are https://www.mcmaster.com/ parts. You can oder parts directly from them or find equivalent parts.

Part 3D printed start with a 3D-xxxx. We have access to a 3D printer using ONYX plastic.

the main component is the stepper motor from https://www.pololu.com/product/2689 , this one is provided with the screw ( selected in design for speed of delivery reason ) but you could buy the same motor and adapt your own screw with this motor https://www.pololu.com/product/2267

the motor is sized for 60 respiration per minute, see the calculation excel for sizing.

# Electronic parts

the electronic is designed to have a main microprocessor, based on arduino or particle.io.

Arduino is well available, but the particle board have the capacity to update remotely. ( a plus during development, but a risk once running with real patient ).

the arduino selected was https://www.pololu.com/product/2188

The microprocessor board drives a 4988 stepper motor driver https://www.pololu.com/product/1182 that is controlled usind 2 pin, direction, and pulse for "speed" . This pulse needs to be managed to reach setup speed from medic team, and can also be managed to have "S" curve for inspiration and expiration.

of course, stepper motor needs to have a "zero" this could be achieved by "returning" the motor to zero and have it "mechanically" stopped, or adding a sensor for position zero and monitor this position "zero" for each positive pressure to patient. The flexibility can only by achieved using a Stepper motor.

To improve a little bit more the system, and to have the pressure setup, we wanted to use Athmospheric pressure monitor based on the bosch 280 https://www.adafruit.com/product/2652 . this will allow us to compare ambiant pressure with pressure to AMBU exhaust and manage the stepper motor accordingly, using a PID loop . ( also, with bypass to ensure minimum respiration setup by DRs )

These sensors would have beed used in the output of AMBU, the return from patient to monitor the PEEP pressure ( from 5 to 20 as standard PEEP pressure ), even if we wanted to use existing PEEP valve from AMBU.

This Pressure sensor was also used to monitor patient respiration, in order to do "Assisted Ventilation", and of course have a software to ensure minimum respiration per minute as per standard ventilator.

The precison expected using BOSCH 280 athmospherique sensor was, based on th position in the curve , from 5 to 10 %, that was the acceptable precision range fir the challenge.

Once we will get all sensor, we will also test and validate theorie.

Off course, these sensor do not meet the "cleaning" requirement, but this could be changed, and we will mount them in a remote small chanber connected to the main "chambers" to avoid contamination, but this is not ideal.



# UI / UX interface 

to have a User Experience, User Interface able to replicate what the medical team is used, we selected 2 option. 

1 - using a 7.00 inch touch screen
2 - using a smaller 3.2 inch touch screen to save cost and have more availability 

the 7.00 screen is https://www.robotshop.com/ca/fr/affichage-lcd-tactile-7-nextion-hmi.html from Nextion

the 3.20 screen is https://www.robotshop.com/ca/fr/affichage-lcd-tactile-hmi-32-nextion.html also from Nextion

this system is for rapid deveolpement and provide a free "HMI" intreface, and also all code to interface to Arduino and other microprocessor board.

you can download the software to design HMI from nextion at https://nextion.tech/

there is also a cheaper version from China, but not available outside of China.

The 7.00 inch screen is able to draw curve, so we will be able to replicate UI used in actual Ventilator.


# Software 

Software wa in a few steps, of course we started with a POC, proof of concept, and evolve to a pre-releae.

- POC : control motor based on "parameter from console" Volume is controlled by Servo 
- STEP 01 : ensure sensor "zero" is activated and create alarm 
- STEP 02 : change cycle per minute based on "parameter from console :
- STEP 03 : change ratio push, release air ( ratio 1/4 to 3/4 ) based on parameter fom console
- STEP 04 : read pressure from multiple sensor and determine pressure from 0 - to - 60 mm
- STEP 05 : add PID control loop based on Pressure sensor 
- STEP 06 : add alarm for multiple alarms as per specification
- STEP 07 : start HMI screen with +/- for Fio2 VT F ration 
- STEP 08 : test functions and integration of HMI 




