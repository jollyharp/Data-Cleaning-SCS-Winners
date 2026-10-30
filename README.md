# Data-Cleaning-SCS-Winners
A data cleaning project using the table from the Wikipedia page for the Supreme Cat Show.

More concise log of operations on the "Supreme Cat Show winners" table from Wikipedia. My goal was to get this table from the web into a workable format, bring cramped data into its own columns, and fix some inconsistent formatting.

- Scraped from page using rvest

- Separated "Breed" column into three new columns: breed, sex, and coat (color/pattern) mostly using regular expressions/brute force
	To organize by coat color or pattern, you would need to filter by what the string contains. Color and sex typically have nothing to do with the breed of the cat unless it has a color in its name or only comes in a specific color, so I'm not sure why these were grouped up in the first place. Male vs female is also a common thing to compare and I thought it would benefit the data for it to be separated.

- Separated "Pedigree Name" column into two new columns: name and title using similar methods to the previous step
	"title" includes all titles. To organize by titles in a graph, you would need to filter by what the string contains. I don't know in what order these ranks go or how to quantify them; if I did, I probably would have separated them further for better analysis. 

- Separated owners and breeders' names when there were multiple
	In the case of couples, names were typically formatted "Mr & Mrs (surname or initials)" or "Name & Name (Surname)", so I split at " & " and concatenated the first person's name or title with everything except the name or title of the second person.

- Added a new column "breeder_owner_match" to show if one or more of its owners were also its breeder(s)
	The "empty" cells were originally filled with "placeholder" rather than "none" for the breeder_2 column to prevent false positives by comparing "none" to "none".

- Modified "Section" column to match number formatting across all years
	Significantly easier to sort. In 2018, the formatting was changed from the name of the section to the number.

- Plotted wins by section, sex (excluding unknowns), & "self-bred" status (owners and breeders being the same)
	Used several of my separated values to be able to make these plots. They are not very complex, though, just simple bar charts with slightly nicer labels.

- Plotted cumulative wins of Persian cats over time
	Persian (section 1) was the most prevalent by a large margin, so I was curious if trends in preference changed over time.

There are a lot of for loops with if statements in them in this program because I couldn't remember if there was a better way to edit individual elements in a table on a condition rather than the entire column at once. Many of them were for fixing outputs from string-related functions, because they would come out as lists, which I could not easily work with. I had to check whether the list was empty, in which case I would replace it with "unknown" or "none" or something of the sort, or if it had a certain other number of elements, or something else along those lines. 

I could have probably just used filter() to filter by whatever condition I was modifying values on and then modify them all at once, but I was always assigning my edits back to the original table, and I wanted the modification to be permanent and the filter to not be. As I'm writing this I'm realizing I could have just made it a new table and then joined them using the year or the name or something like an ID, but what I have now works, so I'll try that out some other time.