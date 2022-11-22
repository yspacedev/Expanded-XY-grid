# Expanded-XY-grid
Custom script for AUTOMATIC1111's stable-diffusion-webui that adds more features to the standard xy grid

## Features added:

Multitool

Customizable prompt matrix

Group files in a directory

S/R Placeholder

Add PNGinfo to grid image

## More info

The code may be very confusing and cluttered because I am not a professional programmer. You are free to add a pull request to this repository to clean up my code, add a feature, or squash some bugs. For now, I've tested it enough to say it works in most cases, but if you encounter a case where it errors out or doesn't work properly, put it in the discussions.

This script is very heavily based (I just modified the code) on the original xy_grid.py created by AUTOMATIC1111 for stable-diffusion-webui, so it includes all the same features. And thank you AUTOMATIC1111 and all other contributors for the original script.

I'm calling this an Alpha release because it is by no means complete or bug free, and definitely has some things left over from development.


# Feature usage:


## Multitool:

The Multitool allows you to adjust multiple parameters in one axis. This allows for theoretically unlimited parameters to be adjusted in one xy grid.
You can now have a CFG scale and steps plot that also compares checkpoint name.

### Format:
<Exact name of field (not case sensitive)>: parameter1, parameter2... | <Exact name of field (not case sensitive)>: parameter1, parameter2... | ...

For example: "Steps: 20, 50 | CFG scale: 7, 10" will create an axis with all possible combinations of those values (Steps: 20 | CFG scale: 7; Steps: 20 | CFG scale: 10; Steps: 50 | CFG scale: 7; Steps: 50 | CFG scale: 10)
 
The data parameters can use ranges like any numerical field can in the base xy_grid script.

For example: "Steps: 20-40 (+10) | CFG scale: 7, 10" will create an axis with all possible combinations of those values (Steps: 20 | CFG scale: 7; Steps: 20 | CFG scale: 10; Steps: 30 | CFG scale: 7; Steps: 30 | CFG scale: 10; Steps: 40 | CFG scale: 7; Steps: 40 | CFG scale: 10)

It also works with text parameters with fields like S/R. For example, "Prompt S/R: a bicycle, a skateboard, a motorcycle | Steps: 20, 50"



## Prompt S/R placeholder:

This very small feature allows you to replace a placeholder value (the first value in the list of parameters) with desired values. 

Example: Prompt: darth vader riding a bicycle, modifier

X parameters: modifier, 4k, 8k

The original Prompt S/R would create the prompts [darth vader riding a bicycle, modifier; darth vader riding a bicycle, 4k; darth vader riding a bicycle, 8k] along the axis

Prompt S/R Placeholder will create the prompts [darth vader riding a bicycle, ; darth vader riding a bicycle, 4k; darth vader riding a bicycle, 8k] along that axis



## Prompt matrix:

This feature functions like S/R placeholder, except it replaces the placeholder value with different combinations of other parameters.

For example: modifier, highly detailed, 4k will replace ALL occurrences of the word "modifier" in the prompt and negative prompt with a combination of "highly detailed" and "4k" (4k; highly detailed; 4k, highly detailed).

There is a minor "bug" where if you use Prompt Matrix in both x and y, and the placeholder words share the same order of characters, the parser will throw an error. (Example: on x: modifier, 4k, 8k; on y: modifier2, realistic, photo) This is because Python replaces all instances of a word like "modifier" with the desired words, and it ends up also replacing the other axis's placeholder word, for example "modifier2". A solution to this is to use "modifier1" as the placeholder value for one axis, and "modifier2" as the placeholder for the other axis.


## Example usage:

![Screenshot 2022-11-16 211052](https://user-images.githubusercontent.com/80003301/202345637-a48d8e28-6bd7-4d3e-9539-94d41b4c6d50.png)


# Example images:

Prompt: "darth vader riding a bicycle, modifier"; <br>
X: Multitool: "Prompt S/R: bicycle, motorcycle | CFG scale: 7.5, 10 | Prompt S/R Placeholder: modifier, 4k, artstation"; <br>
Y: Multitool: "Sampler: Euler, Euler a | Steps: 20, 50"
![xy_grid-0000-1775631796-darth vader riding a bicycle, modifier-min](https://user-images.githubusercontent.com/80003301/202277871-a4a3341b-13f7-42f4-a3e6-ca8f8cd8250a.png)

Prompt: "darth vader riding a bicycle"; <br>
X: Steps: "10, 20, 30, 40, 50"; <br>
Y: Multitool: "Checkpoint name: 1.4, 1.5 | Sampler: Euler, Euler a"
![xy_grid-0001-2789616861-darth vader riding a bicycle-min](https://user-images.githubusercontent.com/80003301/202277910-40d72e95-0afe-4a84-821f-d769035e27d1.png)

Prompt: "darth vader riding a bicycle"; <br>
X: Multitool: "Prompt S/R: bicycle, motorcycle, skateboard | CFG scale: 7.5, 10"; <br>
Y: Multitool: "Sampler: Euler, Euler a | Steps: 20, 50"
![xy_grid-0005-3171584222-darth vader riding a bicycle-min](https://user-images.githubusercontent.com/80003301/202277930-33f371b9-e128-44d0-83dc-e0ac632d5b18.png)

Prompt: "darth vader riding a bicycle, modifier"; <br>
X: Multitool: "Prompt matrix: 1, 4k, 8k | steps: 20, 50"; <br>
Y: Multitool: "Checkpoint name: 1.4, 1.5 | Sampler: Euler, Euler a"
![xy_grid-0073-1378890763-darth vader riding a bicycle, 1-min](https://user-images.githubusercontent.com/80003301/202277967-714d7e33-90bf-41f8-a6af-c6cb4594dd79.png)
