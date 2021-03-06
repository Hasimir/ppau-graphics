# ppau-graphics
Graphics for Pirate Party Australia. 
(@ppau on GitHub.)

There are several purposes for this repository:

1. Version control and general ability for collaboration with source documents.
2. Build an infrastructure that allows us to seamlessly update authorisation tags and, if necessary, printing tags.

The system works by having the artist insert placeholder text, such as `PPAU_AUTH_TAG`, in the artworks instead of something like `Authorised by Name, Address`. The script will perform a textual find-and-replace and then render the artwork to a format more suitable for distribution, currently PNG and PDF. 

# Requirements 

The following programs are required by the render script. 

- a working Python 3.5 (or newer) install to run it.
- `inkscape` 
- `find(1)` 
- `sed(1)`
- `grep(1)`

If you do not specify a correct path to `inkscape`, the script will attempt to find it with `which(1)`.


Additionally, most files in this repository are tracked using Git LFS. See the `.gitattributes` file for a detailed list. An example line: 

`*.jpg filter=lfs diff=lfs merge=lfs -text` 

You'll need the various fonts, too; at a minimum Open Sans (including Condensed) and Gehen Sans, although others might have been used. 

# Usage 

To render the SVGs in the source directory, run the script `render.py` from the command line, probably with something like: 

`python3 /path/to/render.py` 

Add the help flag: `python3 /path/to/render.py --help` for a full list of options. 

Replacement tags are specified in `auth_tag.txt` (authoriser) and `print_tag.txt` (printer). 

There will be three variants of each file rendered:

1. with authorisation tag only (`*-auth.*`),
2. with both authorisation and printing tags (`*-both.*`),
3. with no tags (`*-none.*`)

Each variant will be rendered as a PNG and as a PDF. An SVG with text replacement corresponding to each type is also placed alongside. 

So the single source `Artwork/marriage/cmon-aussie.svg` will result in the following files being generated:

- `Renders/marriage/cmon-aussie-auth.pdf`
- `Renders/marriage/cmon-aussie-auth.png`
- `Renders/marriage/cmon-aussie-auth.svg`
- `Renders/marriage/cmon-aussie-both.pdf`
- `Renders/marriage/cmon-aussie-both.png`
- `Renders/marriage/cmon-aussie-both.svg`
- `Renders/marriage/cmon-aussie-none.pdf`
- `Renders/marriage/cmon-aussie-none.png`
- `Renders/marriage/cmon-aussie-none.svg`

## Examples 

To temporarily override the placeholder authorisation tag text: 

`python3 /path/to/render.py --auth_tag AUTHORISED_BY_CTHULHU`

Be careful using the `--auth_tag` and `--print_tag` flags: remember that they define the text that is to be *replaced*. Specifying an empty string, or something that resembles SVG, will cause issues. 

To specify an alternate file containing the authorisation tag:

`python3 /path/to/render.py --auth_tag_file /path/to/file`

# License

Artwork and text created by members of Pirate Party Australia is released under the Creative Commons [Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) license (CC-BY 4.0), unless otherwise specified. 

Code created by members of Pirate Party Australia is released under the [Free Software Foundation General Public License, version 3](https://www.gnu.org/licenses/gpl-3.0.html), unless otherwise specified.
