# Overview
This file will serve as a guide to the development process of the application.

## Application Aim

The aim of this application is to allow users to submit images and get the css grid in bento box size automatically generated based on the dimensions of each image. [Bento Box Design information](https://www.webdesignerdepot.com/what-is-the-bento-ui-trend-and-how-can-you-get-started/).

## Development Requirements

This will be a website where users can upload a number of images and receive the code for a CSS grid in the style of a bento box dynamically, without the need to manually set dimensions and sizes.

For this to be effective, we will need the following features:

- Multiple image upload
- Live Preview
- Dynamic scaling of css grid properties based on image dimensions.
- Option to shuffle the position of items, and lock items in place so they aren't shuffled.

## How will it work!

### The Problem

Given n images, find a css grid solution, such that each image fits in the grid, and the grid resizes automatically, given longer images more height, and wider images more width, without making the grid uneven.

### Image uploading 

Once images are uploaded one at a time, each one will be inserted into the grid display, with the urls for the images being generataed dyncamically on upload.

### Determining Cell Size

The dimensions for each image will be used to calculate the area and determine whether the image is long, wide, if the corresponding dimension is at least 1.5x the size of the other dimension. This will determine the size of the cell the image will have. This will be stored as a 2 element tuple containing integers which will be the size modification of the cell the image will go into.

When styling, these `(x, y)` modifications will then be applied on the respective axes to display the size of each cell.

### Determining cell position

With the dimensions obtained, next is to determine where each of the cells will go in the position on the grid. The total number of cells will be determined by the number of images uploaded (obviously). Longer cells will tend to be clustered on the sides, whereas wider cells will be primarily nestled within the center area.

We will define the cell types as follows:

- Tall bois: Cells that take up more vertical space than horizontal.
- Wide bois: Cells that take up more horitzontal space than vertical.
- Square bois: Cells that take up the same horizontal and vertical space.
- Big Square bois: These are cells that have a scale of 3 or more on both axes.

Cells should adhere to the following rules when determining where they should go.

- If possible, tall bois should not be directly parallel to each other.
- Square bois should be used to fill in spaces to prevent tall and wide bois from being directly next to each other.
- Big square bois should be as centered as possible, ensuring at least one row above and below.
- Tall bois should be primarily filled from the top left of the grid.
- Wide bois should be primarily filled from the bottom right of the grid.
- Square bois should fill in the empty space.
- The order for the insertion should be: Big Square Bois -> Tall Bois -> Wide Bois -> Square bois.