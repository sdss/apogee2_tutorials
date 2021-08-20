# Examples 
This section has code snippets affiliated with the [Examples Web Documentation](https://www.sdss.org/dr16/irspec/catalogs/). 

For each of the following science applications, we try to explain how one would go about investigating using the CAS (SQL), SAW (Web Application), and SAS (File Server, both IDL and Python). Where applicable, a "*" marks the preferred method for a given science application.

Users unfamiliar with the CAS (SQL) or SAW (Web Application) should consult the CAS tutorial and SAW tutorial sections on this page. For most of these science applications, "Using the SAS" means loading the entire allStar summary file into memory via IDL or Python, and manipulating data to suit the application.

Spectral data is stored in FITS image files. There are standard packages in IDL and Python for using these files; useful information regarding using these files can be found here. All of our data models and, in consequence, the examples below assume a familiarity with these file formats.

## Get Stellar Parameters and Abundances for the Main Red Star Sample

ASPCAP parameters, element abundances, and uncertainties for all stars in the main red star sample with reliable abundances.

- Following the advice on [Using Stellar Parameters](https://sdss.org/dr17/irspec/parameters) and [Using Stellar Abundances](https://sdss.org/dr17/irspec/abundances), quanitites that are not trustworthy will have a series of bits set in [APOGEE_ASPCAPFLAG](https://sdss.org/dr17/irspec/apogee-bitmasks/#APOGEE_ASPCAPFLAG:ASPCAPstarlevelbitmask) or [APOGEE_STARFLAG](https://sdss.org/dr17/irspec/apogee-bitmasks/#APOGEE_STARFLAG,APOGEE_ANDFLAG:APOGEEstarlevelbitmask).
- Following the advice on Using [Targets/Samples](https://sdss.org/dr17/irspec/targettingbits/), the [APOGEE_EXTRATARG](https://sdss.org/dr17/irspec/apogee-bitmasks/#EXTRATARG:basictargetinginformation) will have no bits set if the star is in the main red star sample.
 
## Get element abundances for stars flagged as known cluster members

## Building the H-R Diagram

## Making an Abundance Plot

## Investigating a Spectral Feature
