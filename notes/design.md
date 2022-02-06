# Figma/Design

coolers.co for picking color palettes

unsplash for photos

add min-height on col debug and padding on row debug until done with layout

inspect color for hexcode, add hexcode from mock up

:root{
--ocean: #...;
--wasabi: #...;
--cake-batter: #...;
}

.bg-ocean{
background-color: var(--ocean)
}

background-image for gradients or more than one color

make header, main and footer as your different containers and build at rows and cols from there put in 6 col-4s will break it up into 2 rows of 3.

The row organizes the columns if wanting to move column or all columns put text center on the row so it will move the whole column rather than just the text within the column into the center of the column

add in mobile response after laying out basic wireframe for desktop response

d-md-block to make content disappear on mobile response

margin pushes out of container, apply margin to column to cheat the 12 rule of bootstrap

using col without number will make the cols share the row evenly

inspect and look for row, flexbox button

To change image on screen size- create a media rule in css using a media query, go to mdn and copy media query, replace article with what you want to target i.e. bg-image, replace pixels with screen size breakpoint where you want it to change. change to max-width or swap images

@media screen and (max-width: ?px) {
? {
background image: url("")

    }

}

.some-class{
backdrop-filter: ?% or blur(?px) will apply filter or blur to everything underneath it
}

if image is bigger than column, add class to image tag called image-fluid. Use text-center for buttons. Buttons are considered text as well as a tags and i tags

To move button over image- transform: use -? to move up on y-axis, use positive number to move it down

to scale image down or up so they are all of the same size-
make class for all images add heighth and width to the class for all images. Add object-fit: cover so they don't squish when changing height and width. Add class to your media rule. Leave img fluid so img doesnt break out when changing to mobile

i tag for icons add class to i tag
