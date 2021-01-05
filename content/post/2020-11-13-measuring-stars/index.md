---
title: Measuring the Stars
subtitle: How are luminosity, flux, brightness, magnitude, color index and distance modulus related?
date: 2020-11-20
markup: "mmark"
bigimg: [{src: "solar_spectrum_CCD.jpg", 
desc: "Solar spectrum (KPNO 1981)"}]
draft: false
tags: ["astronomy", "astrophysics", "physics"]
---


While trying to plot Hipparcos satellite data into observational and theoretical Hertzsprung-Russel diagrams I got bogged down in a photometric definitions jungle, which I try to untangle in this post. The working astronomer will know all of this by heart, but at least I needed this workout.


<!--more-->


### Luminosity 


Luminosity $$L$$ is an absolute measure of radiated electromagnetic power, or radiant power, emitted by a light-emitting object. In astronomy, luminosity is the total amount of electromagnetic energy emitted per unit of time by a star, galaxy, or other astronomical object. Luminosity is an intrinsic property of the object &mdash; it does not depend in any way on the location or motion of the observer. 

The IAU has defined a [nominal solar luminosity](https://www.iau.org/static/resolutions/IAU2015_English.pdf) of 3.828 × 10<sup>26</sup> W to promote publication of consistent and comparable values in units of the solar luminosity $$L_\odot$$. There are stars that are 1 million times more luminous than the Sun and other stars that are 1 million times less luminous than the Sun. The exceptionally luminous beacons are rare, and the most common stars are not even as luminous as the Sun.


When not qualified, the term luminosity means **bolometric** luminosity, taking into account electromagnetic radiation at all wavelengths. Luminosity is sometimes referred to as the star’s **absolute brightness**. 


### Radiation flux (aka apparent brightness)

When we look at a star, we actually don't see its luminosity, but rather its **apparent brightness** &mdash; the amount of energy striking a unit area of some light-sensitive surface or device (e.g. CCD chip or human eye) per unit time. 

The apparent brightness of a star is actually measured in terms of the **radiation flux** or **radiant flux** $$F$$ received from the star. Flux means the power going through some surface. The flux emitted by a star into a solid angle $$\omega$$ is

$$F = \frac{L}{\omega r^2} \; .$$  



Imagine a star of luminosity $$L$$ surrounded by a huge spherical shell of radius $$r$$. Then, assuming that no light is absorbed during its journey out to the shell, the radiation flux, $$F$$, measured at distance $$r$$ is related to the star’s luminosity by

$$F = \frac{L}{4 \pi r^2} \; .$$  

Instruments aboard satellites have measured the Sun’s apparent brightness, known as the **solar constant** $$f_\odot$$, which is the total amount of radiant solar energy per unit area reaching the top of the Earth’s atmosphere at the Earth’s mean distance from the Sun. The measurements indicate that $$f_\odot$$ = 1,361 W m<sup>-2</sup> (but note: you will not receive this at your solar panel &mdash; the Sun's rays are attenuated as they pass through the atmosphere, leaving maximum normal surface irradiance at approximately 1000 W m<sup>-2</sup> at sea level on a clear day). At a distance of 1 AU = 1.496 x 10<sup>11</sup> m, the luminosity of the sun is thus $$L_\odot$$ = 3.828 × 10<sup>26</sup> W. By extrapolating the Sun’s radiation flux back to its visible disk, we can further derive the disk’s effective temperature, $$T_\text{eff}$$ from the relation 

$$ F_\odot = \frac{L_\odot}{4 \pi R_\odot^2} = \sigma T_\text{eff}^4 \;  .$$

Using the Sun's radius $$R_\odot$$ = 6.955 x 10<sup>8</sup> m and the Stefan-Boltzmann constant $$\sigma$$ = 5.67 x  10<sup>-8</sup> W m<sup>-2</sup> K<sup>-4</sup> yields a surface temperature $$T_\text{eff}$$ = 5780 K for the visible disk.

Note that physics textbooks use slightly different terminology regarding flux:

* Most US textbooks on elementary astronomy (e.g. Arny/Schneider, Bennett et al., Freedman/Kaufmann, Kay et al.) talk about apparent brightness (or simply brightness) while avoiding the term flux, and correspondingly use the symbol $$B$$ instead of $$F$$.

* Astrophysics books such as Carroll/Ostlie (2017), Lang (2013) or Gallaway (2020) tend to talk about radiant flux (or simply flux) $$F$$.

* Unsöld/Baschek (2002) define the radiation flux $$F_\nu$$ per unit frequency range (1 Hz) and call $$F = \int_{0}^{\infty} F_\nu \,d\nu$$ the total radiation flux.

* Karttunen *et al.* (2016), and with them [Wikipedia](https://en.wikipedia.org/wiki/Luminosity#Luminosity_formulae), call $$F$$ the flux density, while describing the flux emitted into a solid angle $$\omega$$ by $$L = \omega r^2 F$$ and reserving total flux (or luminosity) for $$L =  4 \pi r^2 F$$.



### Apparent brightness and apparent magnitude

Apparent brightness is a measure, not of a star’s luminosity, but of the energy flux (energy per unit area per unit time) produced by the star, as seen from Earth. A star’s apparent brightness depends on our distance from the star.

The Greek astronomer Hipparchos (c. 190 BC–c. 120 BC) was one of the first sky watchers to catalog the stars
that he saw. In addition to compiling a list of the positions of some 850 stars, Hipparchos invented a numerical scale to describe how bright each star appeared in the sky. He divided the stars that he could see into six groups to better measure their relative brightness, relative to the eyes. This way of measuring brightness is called the apparent visual magnitude  and is designated by the lowercase letter $$m$$ or to be explicit about the visual aspect, by $$m_\text{v}$$ with the subscript V denoting ‘‘visual’’.

Hipparchos designated the brightest stars, such as Sirius or Rigel, with the first and most important 
magnitude, $$m = 1$$; Polaris and most of the stars in the Big Dipper were designated $$m = 2$$; and the faintest stars visible to the unaided eye received the sixth magnitude, or $$m = 6$$. Note that a smaller apparent magnitude means a brighter-appearing star.

The rather vague classification of Hipparchos was replaced about two millennia later by the British astronomer Sir Norman Pogson (1829–1891). He noted in 1856 that the stars of the first magnitude were about 100 times as bright as stars of the sixth magnitude. Accordingly, Pogson defined the ratio of the brightnesses
of classes $$n$$ and $$n+1$$ as $$100^{1/5} = 2.512$$.


The **brightness class** or **apparent visual magnitude** $$m$$ can now be defined by demanding that a difference of 5 magnitudes between the apparent magnitudes of two stars shall correspond to the smaller-magnitude star being 100 times brighter than the larger-magnitude star, or expressed through their flux ratio

$$ \frac{F_2}{F_1} = 100^{(m_1 - m_2)/5} = 10^{0.4(m_1 - m_2)} \; .$$

Taking the logarithm of both sides leads to the standard relation between the observed magnitudes of two celestial bodies and their corresponding fluxes:


{{% panel theme="note" %}} 
$$m_1 - m_2 = - 2.5 \log_{10} \left( \frac{F_1}{F_2} \right) \; .$$
{{% /panel %}} 

The apparent magnitude relation takes into account the nonlinear, roughly logarithmic response of the human eye to light intensity (which is still actively debated in psychophysics, see the Wikipedia articles on [Weber's law](https://en.wikipedia.org/wiki/Weber%E2%80%93Fechner_law) and [Stevens's power law](https://en.wikipedia.org/wiki/Stevens%27s_power_law)). Perhaps surprisingly, it turned out that for most stars, Hipparchos’s assessments were actually roughly correct. Today, magnitudes extend both ways from the original six values and the  logarithmic scale causes the very brightest stars to climb to negative apparent magnitudes. Sirius is $$m = -1.45$$, Venus can attain a magnitude of $$−4.5$$, the full Moon is around magnitude $$−13$$, and the Sun is so close and bright that it is $$m = -26.7$$. The number of stars increases dramatically with increasing apparent visual magnitude. There are 14 stars brighter than $$m = 1$$ and about 5,600 stars brighter than $$m = 6$$, which are all of the stars detectable by the unaided human eye. There are 335,000 stars brighter than $$m = 10$$ and 4.8 billion stars brighter than $$m = 25$$. A backyard telescope can detect stars of apparent magnitude between 10 and 15; the Hubble Space Telescope can approach apparent magnitude 30. These stars are 4 billion times fainter than the human eye can see without a telescope.  

### Colors and filters

There are reddish stars like Betelgeuse and Antares, yellowish stars like the Sun and Capella, and whitish stars like Vega and Sirius. These colors provide a rough indication of the temperature of a star’s photosphere as the wavelength of maximum starlight intensity varies inversely with temperature. As the temperature rises, the colors change from red (near 3,000 K), to yellow (around 6,000 K), to white (around 10,000 K).

The coloring of a star, however, is very subtle, depending on the relative amount of light seen in different colors. Blue-colored stars, for example, are not just bluer than red stars. For a star of the same radius, a blue star is more luminous than a red one. Exceptionally hot stars emit most of their radiation at invisible ultraviolet wavelengths, and such a star is even more luminous. There is enhanced radiation intensity at adjacent wavelengths, and this ultraviolet spillover produces more blue light than expected for a cooler star. In this case, the temperature of the star is much hotter than that inferred from blue light alone.

In daylight the human eye is most sensitive to radiation with a wavelength of about 550 nm, the sensitivity decreasing towards red (longer wavelengths) and violet (shorter wavelengths). The magnitude corresponding to the sensitivity of the eye is called the **visual magnitude**  $$m_\text{v}$$.

If, in an ideal case, we were able to measure the radiation at all wavelengths, we would get the **bolometric magnitude**  $$m_\text{bol}$$. In practice this is very difficult, since part of the radiation is absorbed by the atmosphere; also, different wavelengths require different detectors. The sensitivity of the detector is different at different wavelengths. Also, different instruments detect different wavelength ranges. 


Astronomers therefore decided to quantify color by comparing the apparent magnitudes measured in different wavelength bands. The most accurate magnitude measurements are made using photoelectric photometers. The color of a star may be precisely determined by using filters that transmit the star’s light only within certain narrow wavelength bands. One of the multicolor magnitude systems used widely in photoeletric photometry is the **UBV system**  developed in the early 1950’s by Harold L. Johnson and William W. Morgan [(see also this post)](/post/2020-11-12-classification-stellar-spectra/). 

In the standard UBV system, a star’s apparent magnitude is measured through three filters, designated by three capital letters:

* $$U = m_\text{U}$$, the star’s ultraviolet magnitude, is measured through a filter centered at 365 nm with an effective bandwidth of 68 nm.
* $$B = m_\text{B}$$, the star’s blue magnitude, is measured through a filter centered at 440 nm with an effective bandwidth of 98 nm.
* $$V = m_\text{V}$$ , the star’s visual magnitude, is measured through a filter centered at 550 nm with an effective bandwidth of 89 nm.

In any multicolor system, we can define color indices; a color index is the difference of two apparent magnitudes measured in different wavelength ranges X and Y, in other words color index $$= m_\text{X} - m_\text{Y}.$$ In the UBV system it is common to give only the $$V$$ magnitude and the color indices $$U−B$$ and $$B−V$$. 

Within photometry there is an important concept, that of the zero point, which is the magnitude of an
object that for the specified instrument setup will produce one count per second. It is represented by a  preselected flux density $$F_0$$ chosen to correspond to the magnitude 0. All other magnitudes are then defined by $$m = -2.5 \log (F/F_0)$$. The three magnitudes $$U$$, $$B$$, and $$V$$ are by definition related to each other in such a way (i.e. the three constants are chosen in such a way) that for A0 V stars (e.g. $$\alpha$$ Lyr = Vega) $$B-V=U-B=0$$.


### Color index and temperature

The color indices give a measure of the energy distribution in the stellar spectra, i.e. of the wavelength dependence of the radiation flux, as first recognized by Karl Schwarzschild; they are thus also a measure
of the temperatures of the stellar atmospheres. 

Various empiricial fits for the relation between temperature $$T$$ and the $$B-V$$ color index can be found in the literature, see e.g. [Ballesteros (2012)](https://arxiv.org/pdf/1201.1809.pdf), [Sekiguchi/Fukugita (2000)](https://iopscience.iop.org/article/10.1086/301490) or [Reed (1998)](http://articles.adsabs.harvard.edu//full/1998JRASC..92...36R/0000036.000.html). As an example we state the formula by Ballesteros (2012) which works well in
the whole spectrum: 

{{% panel theme="note" %}} 
$$T = 4600 \left(\frac{1}{0.92(B-V)+1.7} + \frac{1}{0.92(B-V)+0.62}\right) \; .$$
{{% /panel %}} 

### Abolute magnitude and distance modulus

Apparent magnitudes do not tell us anything about the true brightness of stars, since the distances differ. A quantity measuring the intrinsic brightness of a star is the absolute magnitude $$M$$. It is defined as the apparent magnitude at a distance of 10 parsecs from the star. To derive it we note that the flux density $$F_d$$ at a distance $$d$$ and the flux density $$F_{10}$$ at a distance $$10$$ pc are related by

$$\frac{F_d}{F_{10}} = \left(\frac{10\:\text{pc}}{d}\right)^2 \; .$$

The so-called **distance-modulus** $$m-M$$, i.e. the difference of magnitudes at $$r$$ and 10 pc, is therefore

$$m-M = -2.5\log\left(\frac{F_d}{F_{10}}\right) = -2.5\log\left(\frac{10\:\text{pc}}{d}\right)^2 \; ,$$

or 

{{% panel theme="note" %}} 
$$m-M = 5 \log \left(\frac{d}{10\:\text{pc}}\right) \; .$$
{{% /panel %}} 


The distance modulus of the Sun is obtained from the definition of 1 pc = 3.086 x 10<sup>16</sup> m and the definition of 1 AU = 1.496 x 10<sup>11</sup> m and is $$(m-M)_{\odot} = -31.57$$  mag. The Sun has an apparent visual magnitude of $$m_{\text{V}\odot} = -26.74$$ and therefore an absolute visual magnitude of $$M_{\text{V}\odot} = 4.83$$. 


### Sources and further reading


B. W. Carroll and D. A. Ostlie, *An Introduction to Modern Astrophysics* (Cambridge University Press, 2017), Chapter 3.

M. Gallaway, *An Introduction to Observational Astrophysics* (Springer, 2020), Chapter 2.

H. Karttunen, *Fundamental Astronomy* (Springer-Verlag GmbH, 2016), Chapter 4.

K. R. Lang, *Essential Astrophysics* (Springer Verlag, 2013), Chapters 2 and 10.

A. Unsöld and B. Baschek, *The New Cosmos* (Springer-Verlag, New York, 2002), Chapters 4 and 6.