# Embeddable Software for Irrigation Control

This software “looks across the river” to explore computer engineering applied within agriculture, particularly precision irrigation. It begins with work by the United Nations Food and Agriculture Organization (FAO). They developed guidelines for estimating a crop’s water requirements. These guidelines describe a set of equations (Penman-Monteith form) drawn from the physics of evapotranspiration. The equations estimate moisture loss based on information specific to the crop, soil type, terrain, and ambient weather conditions. This present work provides a proof-of-concept for an adaptive process that combines an embedded version of FAO’s equations with weather data feeds. The aim is to create a human-supervised fully-automatic approach to irrigation based on estimated crop moisture needs. The author looks forward to collaboration with interested parties in this effort to apply computer engineering to problems in agriculture. With precision irrigation, farmers seek to cope with drought and limited rainy seasons by minimizing water use without devaluing the crop. This present work is another effort in that vein.

# Background

Precision irrigation is a component of precision agriculture (precision farming), a field of work that combines agricultural knowledge with other fields such as computer engineering, geographic information systems, remote sensing, and meteorology. The main point is to improve or, at least maintain, crop value while using fewer resources such as land, pesticides, water, and fertilizers. It does so while retaining nutrition and without resorting to the risks of genetic mutation.

Given the considerable literature in precision agriculture it is clear that computer engineering can help create human-supervised automated-control of irrigation systems for any crop. Such control mechanisms have the potential to aid farmers stricken by drought as they move beyond their dependence on direct-rain for watering crops. This could extend opportunities to grow crops outside the rainy season, while still not over-farming the land. The software in this project makes use of weather data and FAO’s evapotranspiration equations to demonstrate an approach to limiting the amount of water drawn for irrigation.

Besides growing seasons limited by direct-rain irrigation, drought in many nations requires careful use of water. This leads naturally to control over irrigation so that crops are not over-watered or under-watered. Precision irrigation seeks to improve over methods that rely on fixed schedules and fixed volumes. Based on plant, soil, terrain, and ambient weather conditions, measures are taken to estimate a crop’s water needs, and to irrigate on that basis. In the same way that crop health can not always be estimated by visual observation, the same is true of a crop’s water need. By the time the crop or land shows visual signs of dryness, the time when irrigation should have been applied is past.

The general vision combines soil, terrain, plant type, the plant’s moisture needs, actual rainfall, evapotranspiration calculations to give an estimate of water loss and, thus, water needs. From there, a decision is made on activating the irrigator for some length of time at a given volume. An illustration of the vision is shown here:

![Image of Vision](https://github.com/SoothingMist/Embeddable-Software-for-Irrigation-Control/blob/Next-Version/VisionPicture.jpg)

We begin with a calculation of evapotranspiration for a reference crop, ETo. Software will be added as it is developed for modifying ETo to get ETc, evapotransperation for a specific crop, soil, and terrain. Future modules will employ the latest weather readings instead of historical data. A demonstration of embedded computer access will also be added. Scaling the system for large-scale distributed operations is another goal. It is this author's hope that collaborators will have additional ideas for modules and documentation.

# What is in this Version of the Software

This project's software is written in standard-language C++. Microsoft's VisualStudioCommunity, a free integrated development environment (IDE), was used to develop and test the code. This IDE can be downloaded from https://visualstudio.microsoft.com/downloads. If you use an IDE besides VisualStudioCommunity, you may have to respecify the location of sample data files. VisualStudio itself may want to reconfigure the project for the version you happen to be running. Since C++ is used in its standard form (no Microsoft extensions or other dependencies are employed) it should be possible to build the source with any system that supports C++ v11. The uploaded software was built on a 64-bit computer running the Windows-10 operating system. However, it should work just as well with a 32-bit or even 16-bit computer running Windows or Linux. After you build the software, you only need to run it with the sample data.

There are a number of zip files associated with this project:

ETo-UsingWeatherDataFile - Calculates ETo, evapatranspiration for a reference crop. Data input is from a file of historical weather data.

ETc-UsingEToPlustWeatherDataFile - Integrates the ETo calculation with a Kc table for a specific crop under specific conditions. The result is ETc for that crop under those conditions during the specified growing season. Data input is from a file of historical weather data.

# License

This project is licensed under an AGPL-3.0 License, 
https://github.com/SoothingMist/Embeddable-Software-for-Irrigation-Control/blob/master/LICENSE.

Please post bugs, comments, and concerns to https://github.com/SoothingMist/Embeddable-Software-for-Irrigation-Control.

If you use this software please place the following citation in your writings:

Raeth, P.G. (2020) Embeddable Software for Irrigation Control, software and documentation, 
https://github.com/SoothingMist/Embeddable-Software-for-Irrigation-Control.

I am looking forward to your input and participation.
