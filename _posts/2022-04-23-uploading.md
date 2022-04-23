## A whole lil workflow in one screenshot

Having spoken to the appropriate library people and gotten the logins & green lights, I was all set to begin uploading the [newly-disambiguated](https://emdashemma.github.io/2022/04/18/openrefine.html) Mozart recordings to the Internet Archive. (Once the files were hosted somewhere publicly, they could be cataloged as digital resources and linked to the catalog records for the physical items, creating the level of access originally imagined by the digitization grant, despite not getting the money—huzzah!).  

First, I picked a record in my project spreadsheet, "OMC Cataloging and Digitization," and used the filename-to-accession-number mapping to search Google Drive for the filenames and download the files. Then I listened to the file to make sure it was actually a match. (They all were! But this step was still important because often Sides A and B were cross-named in the files vs. the cataloging, which isn't surprising given that the early discs don't label themselves A and B: if the matrix/catalog numbers aren't sequential, there's no real indication of which should be called Side A.)

<img src='https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/main/uploads/omc_screenshot_1' width="400" align="left">

After months in the extremo controlled MARC/RDA/ISBD metadata environment of bibliographic cataloging, here was the Internet Archive with ... no rules at all! I floundered a bit and then came up with what I think is a tolerably complete, semi-structured metadata format for the public access point to these recordings. The UW Libraries' catalog, Primo, lets you download a CSV of the bibliographic record, so, with my hot-of-the-press amateur Python skills, I wrote a little script to take that `file.csv` and restructure it in plaintext with the desired metadata fields prefaced by their element names:

```python
import csv

csvfile = open('file.csv', newline='')
obj = csv.reader(csvfile)

count = 0
for row in obj:
	if count == 0:
		header = row
	else:
		data = row
	count += 1

full_record = dict(zip(header, data))

to_include = ['Title', 'Language','Format', 'Catalog Title', 'Publisher', 'Publication Date', 'Performer or Participant', 'OCLC Number', 'Permalink']

selected_metadata = {}

for term in to_include:
	if term in full_record:
		selected_metadata[term] = full_record[term]

oclc = selected_metadata.get('OCLC Number')

with open("blurb.txt", "r") as f:
	blurb = f.read()

with open(f"{oclc}.txt", "w") as f:
	for key, value in selected_metadata.items():
		f.write('%s: %s\n\n' % (key, value))
	f.write(f"{blurb}")
```

So that's what is happening here, with the output of `mapping.py` the OCLC-number-named txt file at the right:

<img src='https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/main/uploads/omc_screenshot_2' width="400" align="left">

Then I just pasted that text file into the "Description" field of Internet Archive, using my presumptuously-named `data-dictionary.txt` notes to fill the other fields consistently:

<img src='https://raw.githubusercontent.com/emdashemma/emdashemma.github.io/main/uploads/omc_screenshot_3' width="400" align="left">

And look! They're out there on the real Internet! https://archive.org/details/omc-1983-12-01
