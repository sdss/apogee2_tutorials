# Examples 
This section has code snippets affiliated with the APOGEE2 DR17 [Examples Web Documentation](https://www.sdss.org/dr17/irspec/catalogs/). 

For each of the following science applications, we try to explain how one would go about investigating using the *Catalog Archive Server* (SQL), *Science Archive WebApp* (Web Application), and *Science Archive Server* (File Server, with examples in IDL and Python). Many instructions for the *Science Archive Server* can also be applied to the [SciServer](https://www.sciserver.org/), which is a server-side computational platform. 
 
For those unfamiliar with how SDSS data is stored, here is a summary: 

| Tool | Description | Link |
-------|-------------|------|
| Catalog Archive Server or CAS | SQL database | [APOGEE2 Data in the CAS](https://testng.sdss.org/dr17/irspec/spectro_data/#cas) & [Basic CAS Tutorial for APOGEE2 Data](https://testng.sdss.org/dr17/irspec/catalogs/#CAS)| 
| Science Archive WebApp or SAW | GUI Web Application | [APOGEE2 Data in the SAW](https://testng.sdss.org/dr17/irspec/spectro_data/#ScienceArchiveWebapp(SAW)) & [Basic SAW Tutorial for APOGEE2 Data](https://testng.sdss.org/dr17/irspec/catalogs/#SAW) |
| Science Archive Server or SAS | Flat File Server |[APOGEE2 Data in the SAS](https://testng.sdss.org/dr17/irspec/spectro_data/#ScienceArchiveServer(SAS)) | 
| SciServer | Server-Side Platform | SciServer provides access to the main APOGEE2 Summary Files and all Python code can be used in SciServer. | 

Users unfamiliar with the CAS (SQL) or SAW (Web Application) should consult the [CAS tutorial](https://testng.sdss.org/dr17/irspec/catalogs/#CAS) and [SAW tutorial](https://testng.sdss.org/dr17/irspec/catalogs/#SAW) sections on the [APOGEE2 DR17 Examples page](https://www.sdss.org/dr17/irspec/catalogs/). For most of these science applications, "Using the SAS" means loading the entire allStar summary file into memory via IDL or Python, and manipulating data to suit the science application.

Spectral data is stored in FITS image files. There are standard packages in IDL and Python for using these files; useful information regarding using these files has been summarised on the [https://testng.sdss.org/dr17/software/fitsfiles/](SDSS Web Documentation). All of the [APOGEE2 data models](https://data.sdss.org/datamodel/index-files.html) and, in consequence, the examples below assume a familiarity with these file formats.

## Get Stellar Parameters and Abundances for the Main Red Star Sample

ASPCAP parameters, element abundances, and uncertainties for all stars in the main red star sample with reliable abundances.

- Following the advice on [Using Stellar Parameters](https://sdss.org/dr17/irspec/parameters) and [Using Stellar Abundances](https://sdss.org/dr17/irspec/abundances), quanitites that are not trustworthy will have a series of bits set in [APOGEE_ASPCAPFLAG](https://sdss.org/dr17/irspec/apogee-bitmasks/#APOGEE_ASPCAPFLAG:ASPCAPstarlevelbitmask) or [APOGEE_STARFLAG](https://sdss.org/dr17/irspec/apogee-bitmasks/#APOGEE_STARFLAG,APOGEE_ANDFLAG:APOGEEstarlevelbitmask).
- Following the advice on [Using Targets/Samples](https://sdss.org/dr17/irspec/targettingbits/), the [APOGEE_EXTRATARG](https://sdss.org/dr17/irspec/apogee-bitmasks/#EXTRATARG:basictargetinginformation) will have no bits set if the star is in the main red star sample.

### Python 3
- A Juypter Notebook provides an example of [how to select this sample](APOGEE_Keil_Diagram.ipynb)
 
## Get element abundances for stars flagged as known cluster members

In addition to selecting the main red star sample targets, you can select other objects according to how they were targeted. For a discussion of the wealth of targeting bits available, see [Using Targets/Samples](https://sdss.org/dr17/irspec/targettingbits/).
Here, we provide an example of selecting objects chosen to be calibrator stars in clusters with known metallicities, which are identified with the APOGEE_CALIB_CLUSTER in either APOGEE_TARGET1 or APOGEE2_TARGET1 bit 9.

## Building the H-R Diagram

The spectroscopic Hertzsprung-Russell Diagram is key figure to generate from the stellar parameters determined from ASPCAP. To select this sample, the user should select stars with reliable stellar parameters following the advice on [Using Stellar Parameters](https://sdss.org/dr17/irspec/parameters). The different tools provide different levels of specificity for defining this sample, but generally one wants to select for stars with good ASPCAP fits using [APOGEE_ASPCAPFLAG](https://sdss.org/dr17/irspec/apogee-bitmasks/#APOGEE_ASPCAPFLAG:ASPCAPstarlevelbitmask) options. Further constraints to the main red star sample or to exclude ancillary targets, for example, can be achieved by merging code from other examples

### Python 3
- A Juypter Notebook provides an example of [how to make a Keil Diagram](APOGEE_Keil_Diagram.ipynb)

## Making an Abundance Plot

Another key plot is to compare the iron abundance, \[Fe/H\] , to an alpha-element like \[Mg/Fe\]. Selecting stars for this application requires two steps. First, selecting stars with reliable ASPCAP fits based on ASPCAPFLAG and also by removing errant values with a set of cuts. Second, it is adviseable to sub-select regions of the galaxy. As in the H-R diagram example, further refinement of this sample can come from merging different examples on this page.

### Python 3
- A Juypter Notebook provides an example of [how to make abundance plots for the inner and outer galaxy](APOGEE_Abundance_Plot.ipynb) using Galactic Latitude and Longitude.

## Investigating a Spectral Feature

Generally, if a scientific investigation requires the visual inspection of a spectrum, then the star or set of stars to be investigated is known a priori from properties discovered while exploring catalogs. Tor this example, we assume that a star of interest has been identified already.
To demonstrate using the spectra, we will look at an Ap star reported in [Chojnowski et al. (2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...873L...5C/abstract). More specifically, we will use the star [2MASS J06010117+3214538](http://simbad.u-strasbg.fr/simbad/sim-basic?Ident=2MASS+J06010117%2B3214538&submit=SIMBAD+search) that is visualized in [Figure 1](http://www.astroexplorer.org/details/apjlab0750f1) of [Chojnowski et al. (2019)](https://ui.adsabs.harvard.edu/abs/2019ApJ...873L...5C/abstract).

The easiest way to visualize a spectrum is to use the SAW tools because it requires no detailed knowledge of the spectral data model (described in detail here). The SAW provides a means to overlay the spectral fitting windows used for ASPCAP, which is more than sufficient to ask if a spectral feature is problematic -- e.g., contaminated by a skyline or redshifted into a chip gap. Moreover, the SAW provides tools to investigate not only the combined spectra but also the visit spectra and the best-fit synthetic spectrum. Equivalent analyses in the SAS require the accumulation of several types of files in different locations as well as familiarity with each of their data models.

The SAW, however, does not provide analysis tools for line fitting or comparison outside of our standard analyses. For these tasks, the user can use the SAW to gather the data needed and then follow the SAS examples to perform additional investigation.

The SAW provides easy data download options for different spectral products that could be in several places within the SAS and may be more straight forward for acquiring spectral data.

No spectral access tools are provided in the CAS.
