"Freeze" the appearance of a PDF file and (ideally) compress its file size.

Below are the sections [Implementation](#implementation), [Usage](#usage), and [Background](#background).

This script has only quite specific use cases, as it effectively converts the content of each page of a PDF into an image and replaces the original page with that image. As a result, it reduces available options to interact with the file, for example it disables text selection. In most cases turning a PDF page from vector-based content into an image is **not** a desirable outcome.
More about the reason why I wrote this script can be found below in the section [Background](#background). Respective use cases might be derived from the reasoning there.


## Implementation

This script depends on:
 - pdftoppm
 - convert (imagemagick/ghostscript)  
Depending on your system, these packages might be installed by default.

As I did not come around (yet) to build a proper option for verbosity via toggling of a flag, there are two versions included here, `pdfcompr` and `pdfcomprverbose`. The difference is that the latter prints some information at each step to tell the user what is happening at the moment.

The following instructions are essentially valid for both versions. However, for simplicity I mostly refer to `pdfcompr` only.

 1. Download the file `pdfcompr` (optional: and/or `pdfcomprverbose`) and save it to your preferred location. (Hint: depending on the location you might need to use `sudo`, e.g., for access to `/opt/bin`. However, as recommendations where to save such files vary, choose any location at your own risk.)
 2. Make the file executable using `chmod +x`. (Hint: if you chose `/opt/bin` to store the script, navigate there and type `chmod +x pdfcompr`. You might need to use `sudo` again.)
 3. (optional) If not done yet, export the path of the script's location to be able to use it from anywhere. In case of bash, open the file `~/.bashrc` for editing and export the respective path. Using the previous example location `/opt/bin`, add this line `export PATH="/opt/bin:$PATH"`. This allows access to all executable scripts in `/opt/bin` from any location.

 
## Usage

The usage is also decribed in the help text of the script. When using `pdfcomprverbose` instead of `pdfcompr` simply replace the latter with the former at the respective places.

General usage:  
cmd `pdfcompr input.pdf [0-100]`

Example 1:  
The input file is 'test.pdf' and the quality level is the default option (80).  
cmd `pdfcompr test.pdf`  
output file: 'test_compr80.pdf'

Example 2:  
The input file is 'test.pdf' and the quality level is 50.  
cmd `pdfcompr test.pdf 50`  
output file: 'test_compr50.pdf.'


## Background

For a while I was involved in grading handwritten reports from students. Due to a change of the rules that allowed students to submit scanned versions of these reports, I received numerous different PDF files. Some of these were simply photographed reports, some were properly scanned, and others were produced on tablets of different manufacturers using a multitude of software.  
As a result, file sizes varied greatly with some cases reaching > 50 MB per file. Additionally, some software that created these PDF files used optical character recognition (OCR). In some cases multiple PDF viewers I used struggled with a proper display of these files, as the added text was not in the background of the document, i.e., it was visible and made large parts of these files unrecognizable.  
Adding my comments and annotations to these files would have resulted in an incomprehensible mess.

This script helped immensely in these cases. The output PDF files that I got never displayed any hidden texts nor had formatting issues, which enabled easy commenting for me.  
Depending on the input PDF file the output might have only a small fraction of the input's size. In each case I was able to shrink the initial file's size to some degree, albeit only a few percent in some cases.  
Intriguingly, even some PDF files with about 30 pages were compressed to about 4 MB, while maintaining a high degree of readability.