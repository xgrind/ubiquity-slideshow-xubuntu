*This repository has been archived. Starting with Xubuntu 24.04 "Noble Numbat," the installer slides can be found in [xubuntu-default-settings](https://github.com/Xubuntu/xubuntu-default-settings/tree/master/debian/live/desktop-provision).*

# ubiquity-slideshow-ubuntu

<http://launchpad.net/ubiquity-slideshow-ubuntu>

-----

This project is about slideshows which appear while installing Ubuntu or
its *buntu friends. The one source package provides a number of Debian
packages for Ubuntu, including ubiquity-slideshow-ubuntu,
ubiquity-slideshow-xubuntu and ubiquity-slideshow-kubuntu.

This is associated with the ubiquity-slideshow group on Launchpad at
<https://launchpad.net/~ubiquity-slideshow>.

Constructive feedback on the group mailing list is always appreciated!

Please also note the "COPYING" and "AUTHORS" files in this directory, which
all have cool stuff in them.

## Testing the slideshow

The easiest way to test changes to the slideshow is to run
`./test-slideshow.sh`. (Note: needs zenity, which is probably already
installed). This will quickly build the slideshow with your changes and
play it. Note that the test-slideshow script does not do localization.
Testing localization is currently a more involved process.

## Changing slideshows

Each slideshow is inside the `slideshows` directory. These are created
with HTML, CSS and Javascript. They all share the link-core directory in
common. This directory has some Javascript files which should be used by
every slideshow.

To actually edit a slideshow, simply open it from the slideshows directory.
Each slide will be its own html file, like
`slideshows/ubuntu/slides/welcome.html`. index.html will contain a list of
these slides in the order they will appear.

Just pull open a slide in your favourite text editor and have fun.

Be sure to test out your creations! The quickest way is test-slideshow.sh.

You may notice some HTML comments (`<!-- comment -->`) in existing slides.
These will appear as notes for translators. If you write something that may
be confusing for them, please leave a comment in the same fashion.

## Screenshot guidelines

Screenshots are taken at full size, scaled precisely 60% and cropped to
match the other screenshots for a given slideshow. (Ubuntu's screenshots
are 448x304 pixels). Please use GIMP to scale images and set
interpolation to “Sinc (Lanczos3)”. That algorithm seems to handle thin
lines particularly well, and it's good to stay as consistent as we can.

We try to follow some conventions for screenshot content, too:

 * Do something. Open an example document, draw a pretty picture, chat with
with someone, play music. Do whatever you might normally do.
 * Do not over-do. It can be tempting to stick every feature into view.
However, that can be really overwhelming. Instead, try to focus on a
single cool idea that will make somebody interested. It doesn't even have
to be about features. Maybe something you can make? Pick one thing that
really captures the essence of what you want to show.
 * Stick to defaults. We all love to customise, but make sure your fonts,
themes and applications look the same as people get with their shiny new
systems.
 * Be people. People are awesome. You're awesome! But anonymized
screenshots are jarring. If you're afraid you might frighten a mainstream
audience, consider making a fun persona in a different user account.
 * Personas live short lives. Try to avoid time as much as possible - it's
awkward to show the current date, for example. A popular mistake is where
a photo manager has images all taken on a single day! Where you can, try
to make things look lived in.
 * Do not depend on text in screenshots. Remember that the slideshow's copy
is translated, so that text will be unreadable for a lot of users. Try to
find a way to communicate things visually and avoid emphasizing any text
on the screen.
 * Avoid showing the mouse pointer.
 * Editing your screenshots with an image editor is fine if you need to
remove some cut off text, for example, but do not deviate from what is
actually possible with an application.

So, I just made screenshots a little trickier, but I hope that helps.
Good luck!

## Musing on writing style

* We can assume that the user has chosen to install Ubuntu willingly. That
person is now an Ubuntu user and doesn't need to be sold on it further.
The sales-person voice should not exist here. If you start to hear that
voice, file a bug immediately.
* Avoid the car instruction manual voice where possible. That is, try not
to tell people where specific features are, but what they can expect to
find. This is because the slideshow won't follow our users everywhere,
so we have to answer a different question: "What next?"
If we fixate on pressing buttons, the lessons will not stick :)
* Please try to keep things neat, tidy and short. In a lot of cases we can
trust our viewers to find things on their own as long as we show them
where to start. It is possible for a single slide to do quite a bit.

## Additional musings on writing

 * The slideshow is a temporary resource. When it's finished, it's gone
until you install Ubuntu again (which is hopefully never, because our
upgrade tool is awesome and Ubuntu will breathe +1000 life into a
computer).
 * So, what we want to do here is point a user in some interesting
directions, but we can't go all the way. We have to avoid the case where
somebody feels they need to go back to the slideshow for information. It's
fine if someone will miss your slideshow (people love pretty things!), but
it's frustrating when a complex product has all its critical information on
the outer packaging.
 * Avoid writing links that people will need to click, because they won't
always be able to. They probably won't want to, either, because there is an
entire operating system being installed. Our user's 1 GHz netbook sounds
like a washing machine as it is. Instead, we want people to see a simple
link they can write down or remember for later. So, contrary to modern web
writing conventions,
<a href="http://www.ubuntu.com/community">ubuntu.com/community</a>
is a better link than…
<a href="http://www.ubuntu.com/community">the Ubuntu community website</a>
 * This also goes back to the second point: if you have to copy and paste a
URL, try to find something less specific and more memorable.

## Embedding a slideshow

(For example, in an installer)

Slideshows are simple HTML documents and can be embedded with WebKit or
any other browser widget that supports Javascript and CSS.
`Slideshow.py` contains an example implementation with GTK+ 3 and Python.

The slideshow can be given some information through its URL. Append "#"
and add attributes as key=value pairs, separated by "?". The following are
recognized:

    ?controls          Enables debugging controls
    ?locale=LANG       Sets the locale. For example, locale=en_CA.
    ?rtl               Specifies whether to display text right-to-left.

The slideshow expects to be passed a locale parameter, based on the
current locale. It may fall back to English if the requested locale is not
available.

The rtl parameter should be added if that is the current text direction,
since the slideshow will not do this automatically based on the locale.

There is also an ini-style file (see ConfigParser) for each slideshow,
called slideshow.conf. This contains two important variables inside the
Slideshow section: width and height. This way, your implementation can
find the specific size for its web widget and can choose whether to
display a slideshow based on the available screen space.

## Editing slideshow design

For each slideshow, the visual design can be customized. First of all,
notice that each slideshow inside the ./slideshows directory has a file
called slideshow.conf. If you change the dimensions of the slideshow, make
sure to edit this.

Each slideshow also (usually) has a slides/link directory with a CSS file
and some graphics that can be customized.

Of course, the entire thing can be completely redone, too! For more in
depth tinkering, you can edit index.html. Just make sure the general
structure of the document is the same.

In the <head>, we need a link to directory.js and every js file in
link-core.

index.html also needs a block called container, containing another block
named slideshow, which lists all the slides as
<div><a href="slide" class="load"></a></div>

A block with id="debug-controls", and widgets with id="prev-slide" and
id="next-slide" will be handled automatically to produce the debugging
controls that appear when #?controls is added to the url.

Outside of those requirements, this should be fairly flexible. Have fun!

## Adding / editing images

Adding images is something that individual slideshows have a lot of
freedom with; the underlying system doesn't mind how this happens. There
are a few things to note, though:

 * It is nice to have the source of each image (eg: SVG file) in the
images-source directory if we are making any changes.
 * If an image comes from an external source, please attribute its author
and specify its license in debian/copyright.
 * If a common effect is being applied to multiple images, consider
creating an automated script and placing it under the images-source
directory. For example, with the Ubuntu slideshow we have a script called
generate-reflected-pngs.sh which, with a GIMP script, adds a fuzzy
reflection to some SVG images and exports them as PNGs. This will help
people working on the project in the future.

## Localization

A .pot file is generated for each slideshow. One .pot file contains
the strings from every slide in the slideshow.
We routinely gather the translations (in the form of .po files) and add
them to the ./po directory. The build script in ./generate-local-slides.sh
automatically generates slides for each translation using po2html.

The underlying structure is a bit convoluted, but the good news is this:
Actually making translations for this project is very conventional. You
can simply head over to the Ubuntu source package on Launchpad and submit
new strings.
<http://translations.launchpad.net/ubuntu/+source/ubiquity-slideshow-ubuntu>
We will gather the results and merge them back into the project for
releases.

## Other handy scripts

First of all, the slideshow can be built by running make. This uses the
Makefile, which in our case is a fairly straight-forward shell script.
Each slideshow gets its own rule in the Makefile which runs the
appropriate other scripts for the final output to ./build.

 * `make test.ubuntu`: Test the specified slideshow in an example GUI.
 * `make test.ubuntu.fr_CA`: Test the specified slideshow, with the
specified locale, in an example GUI.
 * `make pot`: When slideshow content has been edited, this may be run to
 create new .pot files (for translators) reflecting that content.
 * `./images-source/*.sh`: As mentioned in the "Adding / editing images"
section, scripts are placed here that apply common effects to source images.
This makes it easier to add images to some slideshows.
