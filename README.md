# Embeddable Software for Irrigation Control

This software “looks across the river” to explore computer engineering applied within agriculture, particularly precision irrigation. It begins with work by the United Nations Food and Agriculture Organization (FAO). They developed guidelines for estimating a crop’s water requirements. These guidelines describe a set of equations (Penman-Monteith form) drawn from the physics of evapotranspiration. The equations estimate moisture loss based on information specific to the crop, soil type, terrain, and ambient weather conditions. This present work provides a proof-of-concept for an adaptive process that combines an embedded version of FAO’s equations with weather data feeds. The aim is to create a human-supervised fully-automatic approach to irrigation based on estimated crop moisture needs. The author looks forward to collaboration with interested parties in this effort to apply computer engineering to problems in agriculture. With precision irrigation, farmers seek to cope with drought and limited rainy seasons by minimizing water use without devaluing the crop and without resorting to genetic mutation. This present work is another effort in that vein.

Two papers have been published on this topic:

1) https://academicjournals.org/journal/AJAR/article-abstract/74E637865285

2) https://academicjournals.org/journal/JECI/article-abstract/EED46CD66537

The second stage of this effort is available: https://github.com/SoothingMist/Remote-Soil-Moisture-Sensing.

# Background

Precision irrigation is a component of precision agriculture (precision farming), a field of work that combines agricultural knowledge with other fields such as computer engineering, geographic information systems, remote sensing, and meteorology. The main point is to improve or, at least maintain, crop value while using fewer resources such as land, pesticides, water, and fertilizers. It does so while retaining nutrition and without resorting to the risks of genetic mutation.

Given the considerable literature in precision agriculture it is clear that computer engineering can help create human-supervised automated-control of irrigation systems for any crop. Such control mechanisms have the potential to aid farmers stricken by drought as they move beyond their dependence on direct-rain for watering crops. This could extend opportunities to grow crops outside the rainy season, while still not over-farming the land. The software in this project makes use of weather data and FAO’s evapotranspiration equations to demonstrate an approach to limiting the amount of water drawn for irrigation.

Besides growing seasons limited by direct-rain, drought in many nations requires careful use of water. This leads naturally to control over irrigation so that crops are not over-watered or under-watered. Precision irrigation seeks to improve over methods that rely on fixed schedules and fixed volumes. Based on plant, soil, terrain, and ambient weather conditions, measures are taken to estimate a crop’s water needs, and to irrigate on that basis. In the same way that crop health cannot always be estimated by visual observation, the same is true of a crop’s water need. By the time the crop or land shows visual signs of dryness, the time when irrigation should have been applied is past.

The general vision combines soil, terrain, plant type, the plant’s moisture needs, actual rainfall, evapotranspiration calculations to give an estimate of water loss and, thus, water needs. From there, a decision is made on activating the irrigator for some length of time at a given volume. An illustration of the vision is shown here:

![Image of Vision](https://github.com/SoothingMist/Embeddable-Software-for-Irrigation-Control/blob/master/VisionPicture.jpg)

We begin with a calculation of evapotranspiration for a reference crop, ETo. ETc is a modification of ETo for a specific crop, soil, and terrain. Weather data feeds the calculation of ETo and Kc, a parameter for modifying ETo (ETc = ETo * Kc). ETc estimates the amount of moisture lost. Subtracting that from previous moisture content and comparing to moisture needs estimates the amount of water to add.

# What is in this Version of the Software

This project's software is written in standard-language C++. Microsoft's VisualStudioCommunity, a free integrated development environment (IDE), was used to write and test the code. This IDE can be downloaded from https://visualstudio.microsoft.com/downloads. If you use an IDE besides VisualStudioCommunity, you may have to respecify the location of sample data files. VisualStudio itself may want to reconfigure the project for the version you happen to be running. Since C++ is used in its standard form (no Microsoft extensions or other dependencies are employed) it should be possible to build the source with any system that supports C++ v11. The uploaded software was built on a 64-bit computer running the Windows-10 operating system. However, it should work just as well with a 32-bit or even 16-bit computer running Windows or Linux. After you build the software, you only need to run it with the sample data.

There are a number of stand-alone zip files associated with this project. Each comes with a file AboutThisSoftware that gives more details. Please post a message if you find some detail is missing.

WeatherData - Contains sample weather data downloaded from the US National Centers for Environmental Information, Global Summary of the Day (GSOD), repository. This directory goes in the same directory as each of the code directories.

ETo-UsingWeatherDataFile - Calculates ETo, evapatranspiration for a reference crop. Data input is from a file of historical weather data. If you only need ETo, this is the program to use.

ETc-UsingEToPlusWeatherDataFile - Integrates the ETo calculation with a Kc table for a single crop under normal conditions. The result is ETc for that crop under those conditions during the specified growing season. Data input is from a file of historical weather data. If you have a specific Kc table, this is the program to use.


========================

These are old codes that are being improved. They read a different version of the weather data.


ETc-CalculatedFromGeneralTable - Calculates ETc using FAO's general Kc and crop-growth-phase tables and associated equations for single-parameter/normal-conditions. This is the program to use if you use the general Kc tables.

ETc-GeneralTable-NetworkedIrrigator - The same calculation for ETc as in ETc-CalculatedFromGeneralTable is applied, combined with software moldules to create a rudimentary client/server system. The server, software written for the BeagleBoneBlack (https://beagleboard.org/black), an embeddable computer, receives messages from the client indicating how much water is needed. The server turns an LED on and off during the period of "irrigator" operation. The client uses VisualStudio-specific networking modules. However, those are in their own class and could be replaced by Linux-oriented modules. The server is written specifically for the BeagleBone but here too the modular nature makes that easy to modify. It is a matter of which irrigator controller one is using.

ETc-GeneralTable-NetworkedIrrigator-WeatherFeed - Replaced the reading of historical weather data with a REST query to the US Weather Service for readings over the last 24 hours. The resulting JSON response is reformatted into a record compatible with all other software modules. No changes to the calculation of ETo and ETc were made. Sweet Corn is used as the crop of interest since that is grown in Dayton Ohio USA, where the weather station is located. A generic windows server is provided for those without a BeagleBoneBlack.


The software above uses a data format for weather data that is different from what now is delivered by the US National Oceanic and Atmospheric Administration, National Centers for Environmental Information. Still, sample data is there for your use. (JSON deliveries remain the same.)


RainPrediction - Conducts an experiment in statistical classification of weather conditions under which next-day precipitation may occur. See the document ApplyingC5.pdf in the root directory.


WaterUse - Evolves earlier software so that it uses the new US weather data format. That software is integrated with RainPrediciton to study the impact of rain prediction on water volume consumed by irrigation. There are three sub-directories:

  1. WeatherData: Contains all weather data used to drive the software during testing.
  2. WaterUseTesting-SansPrediction: ETo and ETc without rain prediction. This is a VisualStudio project.
  3. WaterUseTesting-WithPrediction: ETo and ETc with rain prediction. See Notes.txt to build and run. Builds but will not run in VisualStudio.

# License

This project is licensed under an AGPL-3.0 License, 
https://github.com/SoothingMist/Embeddable-Software-for-Irrigation-Control/blob/master/LICENSE.

Please post bugs, comments, and concerns to https://github.com/SoothingMist/Embeddable-Software-for-Irrigation-Control.

If you use this software please place the following citation in your writings:

Raeth, P.G. (2020, September) Embeddable Software for Irrigation Control, software and documentation, 
https://github.com/SoothingMist/Embeddable-Software-for-Irrigation-Control.

I am looking forward to your input and participation.
