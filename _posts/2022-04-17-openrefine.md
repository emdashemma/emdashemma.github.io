## The magic of OpenRefine

In the course of cataloging the 78rpm recordings for my Capstone project—working toward vendor digitization with a grant that didn't come through—I learned that the Music Library had a "mystery hard drive" with a couple of folders, "Mozart 10" and "Mozart 12", among these large sets of more-or-less unidentified files. These had not been considered viable access copies for the collection because they were origin- and nomenclature-unknown. 

With the grant off the table, though, maybe it was worth another look. I had access to the Google Drive version of the mystery drive, and I'd spent two months mapping the different numbers across these materials: tracking spreadsheet vs. database, call number vs. accession number, label on actual container vs. list of... Maybe the filenames would map.

Why is there no Google directory print? Nineteen ZIPs and 19x `ls > list.txt` later (the internet said this is not best practice but... it worked?), I had a CSV of filenames to drop into an OpenRefine project. I copied the internal database of disc metadata into another OpenRefine project—this has accession number and some work/performer/label/matrix info—and then set about mapping the accession numbers onto the filenames.

The goal was to massage these into identical text strings so that a `cell.cross` function could pull the original filename into the project with metadata. Then, reuinted with their metadata, these files could potentially serve as our access copies for the collection!

OpenRefine is the perfect tool for this kind of data manipulation: the logic behind the filenames was clearly identifiable to someone familiar with the collection, but they had been formulated inconsistently and with quite different grammar than the accession numbers. Accession numbers were structured **omc-1980-12-02**, with **omc** standing for "Offenbacher Mozart Collection," **1980** the year of acquisition, **12** the disc diameter, and **02** indicating the acquisition number of that size in that year. Filenames looked something like **801202.wav**, with the same elements represented: **80** = 1980, **12** = 12" disc, **02** = second disc. Or they looked something like **ES(10)8a.wav**, because an entire half(?) of the collection was identified by two-letter abbreviation of the opera (here, ES = _Entführung_) instead of year... okay.

From the accession number side, the most stripped-down string that captured the semantic information would look like this:

<img src="https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/blob/main/uploads/accession_trim.png" width="500">

Then, simple transformations of "Filename" in the other project, aiming toward the same thing (chomp the end off, remove punctuation):

<img src="https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/blob/main/uploads/filename_transformations.png" width="500">

But then... a bunch of the filenames were more like **001235a.wav**. I had learned from handling the original discs—which were labeled with \*different\* accession numbers, no hyphens, whatever—that the original accession, in 1978, had originally been labeled with leading zeros rather than years. So the "modern" accession number **omc-1978-xx-xx** actually refers to a disc in a sleeve with a label "00xxxx". 

There was some padding nonsense as well. I faceted by filename string length and noticed that some just seemed to have a few extra zeros, so I replaced any "000" with "00", then used a regular expression `/^00/` to convert those leading 00s into 78s.

The sweet, sweet moment of truth: 

<img src="https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/blob/main/uploads/cell_cross.png" width="500">

After reviewing the filenames that got left behind, I reiterated some of the transformations to catch other weirdnesses—for example, the filenames didn't pad the final unit the way the accession numbers did, so I manually added in some penultimate zeros, and got a few hundred more matches—and tada! after about 90 minutes of fiddling, I had 1037 matches. 

Next up: since we know what they are now, can we upload them?? 
  
