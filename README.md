## Entries
This repository contains original entries and transformed entries form **Bridge_AZ.pdf** dictionary.
Entries from folder **original_entries** were transformed where each word has *< TOKEN >* tags around it.
Transformed entries are located in **tokenized_entries** folder.

Correct entries with *< dictScrap >* and *< re >* tags are located in **dictScrap** folder.
These entries also contain **page** and **text** attributes.
These entries were manually checked for errors.


**Note:**

Entries in **dictScrap** folder might not be the same as entries in **tokenized_entries** folder.
Assume that entries in **dictScrap** are correct and disregard the same entries in **tokenized_entries** folder.
Entries in **correct_entries** folder are from and older version. They have been manually checked for errors but do not
have < dictScrap/re > tags and page/text attributes.

## Dictionary pages
Dictionary pages are located in **dictinary_pages** folder.
Pages range from page 16 to page 884.
Only token lines were kept and **page/text** attributes were added. 

## Logs

Transformation log is in **info.log** file. This log contains info about the transformation for each entry.
Each entry in transformation log, has described with which word each word was replaced.

**Original** -> shows the original words from the entry

**Changed** -> shows the words that were taken from *tokens.xml* file and replaced the original ones.

At the end of each entry, there is also a grade showing the similarity factor of the original and transformed entries given in percentage.

File **grade.log** contains grades for each entry.
**WARNING** in grade.log means, that the entry could not be parsed using lxml library. This usually occurs when a tag (e.g. < form >) is not closed.


### How the grade is calculated:

Each entry is split by empty spaces. The pronunciation is removed from the entry. Split words (e.g. "abet- ting")
are joined together and the "-" character is removed. Then each word from the original entry is compared with
the transformed entry word using the *difflib.SequenceMatcher.ratio()* function. This function gives [0,1] grade based
on the similarity of those two words (the higer, the better). Ratios for all words are then summed up and divided
by the number of words in the entry.

**Note:**
- Entries that failed the transformation, usualy misplace the words. This happens because the original entry contains
a word that is missing from *tokens.xml* file. Consequently this entry has a lower grade.
- If grading failed, a grade of **-1%** is given to the entry.
- Transformed entries with grade > 90% can be assumed they are correct.

## TO DO:
Entries in **tokenized_entries** with grade lower than 90% should be rechecked.
Mark which entries are faulty so I can correct them manually.

- Sometimes an original word might be split with "-" character, as mentioned above. This is not incorrect.
- Some characters (Š, Č, Ž) in original word are different after transformation. This doesn't meant that entry is incorrect.
- As mentioned above, some words might be missing in *tokens.xml* file, which misplaces all the following words. This is an
incorrect entry and should be marked down.
- Sometimes an additional word is placed beside pronunciation. This also misplaces all the following words and makes entry incorrect.

