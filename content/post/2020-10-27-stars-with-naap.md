---
title: Exploring Stars with NAAP
subtitle: Explorations with the Nebraska Astronomy Applet Project
date: 2020-11-27
markup: "mmark"
bigimg: [{src: "/img/2020-04-25-ai-weekly-17-2020.jpg", desc: "Cherry blossom (Berlin 2020)"}]
draft: true
tags: ["astronomy", "astrophysics", "physics"]
---

The University of Nebraska-Lincoln [astronomy education group](https://astro.unl.edu/) (NAAP) consists of a team of artists and programmers, developing a variety of astronomy education materials, among them [simulations and animations](https://astro.unl.edu/animationsLinks.html) and [applet-based online labs](https://astro.unl.edu/naap/)
 


 
<!--more-->


### Black-body Curves and Filters Explorer

All matter with a temperature greater than absolute zero emits thermal radiation. Thermal radiation is electromagnetic radiation generated by the thermal motion of particles in matter &mdash; particle motion results in charge-acceleration or dipole oscillation which produces electromagnetic radiation. 

If the radiating body and its surface are in thermodynamic equilibrium and the surface has perfect absorptivity at all wavelengths, it is characterized as a black-body. A black-body is also a perfect emitter. The radiation of such perfect emitters is called black-body radiation. The radiation is emitted according to Planck's law, meaning that it has a spectrum that is determined by the temperature alone, not by the body's shape or internal composition. By measuring the peak wavelength of an object's blackbody radiation we are, thus, able to deduce the temperature of the object. 

A star is often modeled as a black-body and electromagnetic radiation emitted from these bodies as black-body radiation. The photosphere of the star, where the emitted light is generated, is idealized as a layer within which the photons of light interact with the material in the photosphere and achieve a common temperature $$T$$ that is maintained over a long period of time. Some photons escape and are emitted into space, but the energy they carry away is replaced by energy from within the star, so that the temperature of the photosphere is nearly steady. The outer layer of the star is somewhat analogous to the example of an enclosure with a small hole in it, with the hole replaced by the limited transmission into space at the outside of the photosphere &mdash; the photons are much more likely to interact with the material within the source than to escape. With all these assumptions in place, the star emits black-body radiation at the temperature of the photosphere. 

The [Black-body Curves and Filters Explorer](https://astro.unl.edu/classaction/animations/light/bbexplorer.html) demonstrates how the blackbody spectrum varies with temperature. The left panel shows the plot of intensity vs. wavelength (the spectrum) for one or more blackbodies. The rainbow indicates the visible part of the electromagnetic spectrum. The filters panel lets one see how a star with the same distribution as the selected curve would look through various filters commonly used by astronomers.

As an example, we can use the explorer to plot the spectra for the coolest and the hottest stars whose peak black-body wavelength can be observed with the human eye. Notice that the hotter star has a much narrower peak and a much higher amount of total radiation, represented by the area under the curve.

<center>
{{< figure src="/img/2020-10-27-stars-with-naap/blackbody1.jpg" width="750px">}}
<p style="color:#989898"><small>
Spectra for stars whose peak black-body wavelength can just be observed with the human eye
</small></p>
</center>

The photosphere of our Sun has a temperature of roughly 5780 K. The corresponding spectrum is peaking at 501.3 nm, the wavelength of green light. [That doesn't mean the sun is green](http://solar-center.stanford.edu/SID/activities/GreenSun.html), or yellow or orange or even red. The Sun is essentially all colors mixed together, which appear to our eyes as white.

<center>
{{< figure src="/img/2020-10-27-stars-with-naap/blackbody2.jpg" width="750px">}}
<p style="color:#989898"><small>
Spectrum of black-body with our Sun's temperature</small></p>
</center>


### Stellar Spectra and Luminosity

Almost everything we know about stars comes from observing light, and most of the details come from measuring their spectra. The analysis of stellar spectra began with Joseph von Fraunhofer's observations on which I had written in an [earlier post on Fraunhofer 2020-10-20-fraunhofer-lines](/post/2020-10-20-fraunhofer-lines/). Spectral characteristics are used by astronomers for various schemes of stellar classification. 










We also
discussed the classification of spectral classes and how it nicely divides stars
based on their effective temperature, intrinsic brightness, spectrum, and mass.
What we didn’t discuss is another important classification that can be seen on
the HR diagram, the luminosity class.
Recall that while stars spend most of their time fusing H into He on the
main sequence, there are also periods of time where they are powered by other
reactions (like He fusion powered giant stars, white dwarfs, neutron stars, etc).
But since the stars temperature and brightness depend on its initial mass, many
stars that are of the same luminosity class (ie giant stars) will be spread out a
bit on the HR diagram (see Figure 4). So while stars spend most of their time
on the main sequence (luminosity class V), a sun-like star will become a giant
star (luminosity class IV) while it is burning He and a white dwarf (luminosity
class VII) after it no longer has any gas it can fuse and is supported only by
electron degeneracy pressure.
The exercises for this simulation are mainly geared toward your understanding of stellar blackbody, emission, and absorption spectra.