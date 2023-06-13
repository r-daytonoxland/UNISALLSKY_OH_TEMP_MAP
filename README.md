# UNISALLSKY_OH_TEMP_MAP

This software reads in images from UNIS' Allsky Airglow camera and produces a map of mesosphere 87km temperature above Svalbard.

### Author
Rowan Dayton-Oxland

## Algorithm

- Read in images from UNIS Allsky airglow camera
- Calibrate images against background sky, flat field, darks etc.
- Interpolate images so they're simultaneous
- Calculate the rotational temperature from the P1(2) P1(4) line ratios (Channels 5 and 6 of the camera)
- Project the temperature map from All-Sky to over Svalbard

Temperatures are calculated according to the equation

$ T_{rot} = \frac{\frac{hc}{k} (F_b - F_a)}{ln(\frac{I_{a} A_{b} (2J_{b} + 1)}{I_{b} A_{a} (2J_{a} + 1)})}$

Where $F,A,J_{a, b}$ are known quantum coefficients, and $I_{a,b}$ are the intensities of the lines in each pixel.

## Data for the two emission lines

| Symbol | F(J') (cm)    | Wavelength (A)   | J'   | Einstein A   |Channel|
|:-------|:-----------|:-----|:----|:------|:------|
| P1(2)  | -45.170339 | 8399 | 1.5 | 0.434 |5      |
| P1(4)  | 113.752553 | 8465 | 3.5 | 0.579 |6      |

## References and links

[UNIS Allsky Airglow Camera](http://kho.unis.no/Instruments/KeoSentry.html)



https://pypi.org/project/oh-einstein-temp-convert/

[Holmen, S., Trends and variability of polar mesopause region temperatures attributed to atmospheric dynamics and solar activity, PhD Thesis, UiT The Arctic University of Norway, 2016.](https://hdl.handle.net/10037/10740)

[Mark P. J. van der Loo, Gerrit C. Groenenboom (2008) Theoretical transition probabilities for the OH Meinel system. J. Chem. Phys. 21 March 2007; 126 (11): 114314.](https://doi.org/10.1063/1.2646859)

## Acknowledgements

Noora Partamies, Mikko Syrjasuo, James Plank