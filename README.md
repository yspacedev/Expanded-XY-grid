# Expanded-XY-grid
Custom script for AUTOMATIC1111's stable-diffusion-webui that adds more features to the standard xy grid

Features added:

Multitool (still working on getting the step count to be correct)

Customizable prompt matrix

S/R Placeholder

Group files in a directory (still working on)

Add PNGinfo to grid image



The code may be very confusing and cluttered because I am not a professional programmer. You are free to add a pull request to this repository to clean up my code, add a feature, or squash some bugs. For now, I've tested it enough to say it works in most cases, but if you encounter a case where it errors out or doesn't work properly, put it in the discussions.

This script is very heavily based (I just modified the code) on the original xy_grid.py created by AUTOMATIC1111 for stable-diffusion-webui, so it includes all the same features.

I'm calling this an Alpha release because it is by no means complete or bug free, and definitely has some things left over from development.


Feature usage:

Multitool:

The Multitool allows you to adjust multiple parameters in one axis. This allows for theoretically unlimited parameters to be adjusted in one xy grid.
You can now have a CFG scale and steps plot that also compares checkpoint name.

Format:
<Exact name of field (not case sensitive)>: parameter1, parameter2... | <Exact name of field (not case sensitive)>: parameter1, parameter2... | ...

For example: Steps: 20, 50 | CFG scale: 7, 10 will create an axis with all possible combinations of those values (Steps: 20 | CFG scale: 7; Steps: 20 | CFG scale: 10; Steps: 50 | CFG scale: 7; Steps: 50 | CFG scale: 10)
 
