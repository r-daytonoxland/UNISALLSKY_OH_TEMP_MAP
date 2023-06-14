# UNISALLSKY_OH_TEMP_MAP

This software reads in images from UNIS' Allsky Airglow camera and produces a map of mesosphere 87km temperature above Svalbard.

### Author
Rowan Dayton-Oxland
[University of Southampton](https://www.southampton.ac.uk/people/5z2prx/miss-rowan-dayton-oxland)
[Github](https://github.com/r-daytonoxland)

## Installation

Download or pull from Github

## Requirements
- Python >= 3.10
- .ipynb capabilites e.g. Jupyter Notebook, Visual Studio code
- OS independent
- numpy, pandas, matplotlib, pathlib, struct, glob, datetime

## Contributing
Pull requests are welcome, for major changes please open an issue first to discuss what you would like to change.

## Algorithm

- Read in images from UNIS Allsky airglow camera
- Calibrate images against background sky, flat field, darks etc.
- Interpolate images so they're simultaneous
- Calculate the rotational temperature from the P1(2) P1(4) line ratios (Channels 5 and 6 of the camera)
- Project the temperature map from All-Sky to over Svalbard

Temperatures are calculated according to the equation

$$
T_{rot} = \frac{\frac{hc}{k} (F_b - F_a)}{ln(\frac{I_{a} A_{b} (2J_{b} + 1)}{I_{b} A_{a} (2J_{a} + 1)})}
$$

Where $F,A,J_{a, b}$ are known quantum coefficients, and $I_{a,b}$ are the intensities of the lines in each pixel.

## Data for the two emission lines

| Symbol | F(J') (cm)    | Wavelength (A)   | J'   | Einstein A   |Channel|
|:-------|:-----------|:-----|:----|:------|:------|
| P1(2)  | -45.170339 | 8399 | 1.5 | 0.434 |5      |
| P1(4)  | 113.752553 | 8465 | 3.5 | 0.579 |6      |

## Examples
```
# Run the script including all the functions
# Current iteration in .ipynb format so
# open the file and run in Jupyter Notebook
# or another appropriate editor

import glob

# Get the files from the CH5 and CH6 folders (typical format for UNIS Allsky Airglow Camera data)
Channel5files = glob('filepath/CH5/*.img')
Channel6files = glob('filepath/CH6/*.img')

# Use get_image_pairs to match up the images in time
image_pairs = get_image_pairs(Channel5files, Channel6files)

# To get the time from a specific image file as datetime obj
fname = Channel5files[0]  # For example
time = time_fname[fname]

# To read an image file
header, image = read_img_file(fname)

# To get the dark value from the corner of the image
darkvalue = corner_dark(image)

# To get the calibrated image file (using the corner dark)
calibrated_img = calibrated(image)

# To get the cleaned up version an image or map
cleaned = cleanup_map(image)

# To retrieve a list of all the temperature maps for a folder or some of a folder
tempmaps = get_tempmaps(Channel5files, Channel6files, len(Channel5files))
# or
tempmaps = get_tempmaps(Channel5files, Channel6files, 10)
# To get the first 10 temperature maps

# To produce a keogram from a folder or some of a folder (as above)
timestamps, keogram = get_keogram(Channel5files, Channel6files, len(Channel5files))
```

## References and links

[UNIS Allsky Airglow Camera](http://kho.unis.no/Instruments/KeoSentry.html)

https://pypi.org/project/oh-einstein-temp-convert/

[Holmen, S., Trends and variability of polar mesopause region temperatures attributed to atmospheric dynamics and solar activity, PhD Thesis, UiT The Arctic University of Norway, 2016.](https://hdl.handle.net/10037/10740)

[Mark P. J. van der Loo, Gerrit C. Groenenboom (2008) Theoretical transition probabilities for the OH Meinel system. J. Chem. Phys. 21 March 2007; 126 (11): 114314.](https://doi.org/10.1063/1.2646859)

## Acknowledgements

Noora Partamies, Mikko Syrjasuo, James Plank

## License

[GNU GPLv3.0](https://choosealicense.com/licenses/gpl-3.0/)