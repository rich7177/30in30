# Thirty Commands in Thirty Minutes

## Thirty Commands (or more!) in Thirty Minutes (but likely not less!)

Welcome to our talk. This is the agenda, and also a reference for later. Follow along as we build some sample data, then do all sorts of fun searches against that data!

## Section 1 - Generating Commands

"Creating" data
gentimes and makeresults can *directly* create events. The former can generate a sequence of time-stamped events, and the latter can generate either a single stub event, or can be used to generate data from a small inline CSV or JSON data set.

The last of the three is outputlookup which can be used to take some existing search/data and "save it" so that you can pull it up again.

These three commands make up the cornerstone of our test data. Do note there's also a outputcsv that can function much like outputlookup, but it saves the file in a different location which can't actually be used as a lookup.

| Command  | Description |
| --- | --- |
| makeresults  | Can be used to create a single empty event, or used to generate small data sets from CSV or JSON formatted data. |
| gentimes  | Generates a set of timestamped fake events. |
| outputlookup  | Takes any other output and saves it onto disk to be read back in with inputlookup |
| outputcsv  | NOT covered here, but is much like outputlookup except it creates files in a different folder. |

## Section 2 - Reading in [non-indexed] data
What can I do with the data I just wrote using outputlookup?

Now that we have data "created", how might we read that back in to use it again?

inputlookup and lookup to the rescue!

| Command  | Description |
| --- | --- |
| inputlookup  | Directly reads in the contents of CSV files that are stored in the 'lookups' directory. |
| lookup  | Uses the CSV file "dynamically", looking up the matching values from the events into the lookup, and returning other fields from the lookup. |
| inputcsv  | NOT covered here, but is much like inputlookup only reads files created by outputcsv and which live in a different folder. |

## Section 3 - Field Editing
Making new fields, and editing existing

An extremely useful "swiss army knife" command is eval which lets us dynamically create new fields on the fly. This is a lot more powerful than you might think at first.

| Command  | Description |
| --- | --- |
| eval  | Edits existing fields or creates new fields. Can use all sorts of conditional logic. |

## Section 4 - A Brief Aside about 'tables'
Table vs. Fields, which does what?

A pair of commands, fields and table, are often confused but are worlds apart for what they actually do. table is for prettifying things, but can have enormous [negative] performance implications. fields on the other hand doesn't make things much prettier but is the complete opposite with respect to performance and is very useful to optimize searches.

| Command  | Description |
| --- | --- |
| table  | Formats output for "human consumption" into a nice, organized table. |
| fields  | Removes fields from the existing output stream, often for increased performance. |

## Section 5 - Smashing things together, the inefficient way
Appending multiple data together

append, appendcols, and appendpipe all have "append" in their name, but function in totally different ways.

Note that "append" here means something specific. We do NOT generally recommend using any of the append methods to actually combine separate data together, there are better ways you'll learn later.

| Command  | Description |
| --- | --- |
| append  | Appends two data sets together, like if you pasted a second log file to the end of the first. |
| appendcols  | Appends a second data set in as new *columns* in the existing rows, like if you paste new columns to the right side of a spreadsheet. |
| appendpipe  | Kind of like appending in the same data, useful in some niche use cases where you need to do calculations on the data, but also keep the data as raw events too. |

## Section 6 - easy data selectors
The first and easiest of the data analytics commands

head, tail, top, and rare all work in similar ways, and their names are a giveaway.

| Command  | Description |
| --- | --- |
| head  | Trims data to just the first N events (default 10). |
| tail  | Trims data to just the last N events (default 10). |
| top  | Does some simple calculations and shows you the more common of the different values of a field are. (The "top 10" by default). |
| rare  | The inverse of top, rare shows you the least common of the different values of a field. (The "rarest 10" by default). |

## Section 7 - Sorting
Sorting data

sort and reverse both exist to sort data, which Splunk rarely (if ever) needs but people need all the time. Because we're not machines.

| Command  | Description |
| --- | --- |
| sort  | Sorts events ascending, descending, or in complex combinations. |
| reverse  | A special case of sort, just reverses the normal output direction of a search's events. Has negative performance implications, though if that's what you need, you just deal with it. |

## Section 8 - Transpose
Flipping X with Y

transpose is in a class of its own. When used it swaps your X and your Y axes.

| Command  | Description |
| --- | --- |
| transpose  | Swap your X and your Y. |

## Section 9 - Whatever it is xyseries and untable do
Fixing weirdly structured data. Or something like that.

xyseries and untable are almost but not quite inverses of one another, and each modifies the structure of data to either "make it into a table" when it wasn't before, or to undo data that's too tabular. Sorry fore the confusion, just see the examples.

| Command  | Description |
| --- | --- |
| xyseries  | Converts data from a more "tabular" form to one that more closely resembles the output of stats. |
| untable  | Converts data into a more "tabular" form. |

## Section 10 - Filling in the missing or brokenness in our lives
Don't let your data ghost you!

The three commands makecontinuous, filldown, and fillnull all perform variations of "filling in missing values". Makecontinuous just fills in gaps in non-contiguous events by adding events. Fillnull fills in null values with some user-specified value, and filldown uses the previous value to fill in empty values.

| Command  | Description |
| --- | --- |
| makecontinuous  | Fills in gaps in events by just adding empty events into the holes. |
| filldown  | Uses the previous value for a field to fill in gaps/missing values. |
| fillnull  | Replaces null valued fields with some user-specified value instead. |

## Section 11 - Relative Times
So, I'm weird and this is my favorite command.

While it's a fairly niche command, I think reltime is underutilized. Makes times into things like "5 minutes ago".

| Command  | Description |
| --- | --- |
| reltime  | Converts times into a human-readable difference in time from "now", like "2 days ago". |

## Section 12 - Renaming things
Changing field names

rename is a pretty simple command, I think you'll get the hang of it quickly. Also keep in mind that many other commands like timechart, stats and others, all let you rename things during the command itself making rename often unnecessary.

| Command  | Description |
| --- | --- |
| rename  | Renames fields - and remember you can rename ugly/shorthand names to longer ones for readability, or rename long ones (or ones with spaces) temporarily to make it easier to work with it. |

## Section 13 - REGEX, YAY!
Regular Expressions are FUN!

regex and rex both involve regular expressions, but in completely different ways. regex lets you filter events by a regular expression, and rex lets you either create new fields from parsing "things" with regular expressions, or lets you do some simple replacing/substitution (using mode=sed).

| Command  | Description |
| --- | --- |
| regex  | *FILTERS* data by a regular expression. |
| rex  | Uses regular expressions to *CREATE* new fields from existing data. |

## Section 14 - Real "data analytics"
Serious Data analytics commands

There's a lot of meat here. timechart creates time-oriented aggregations, whereas stats is more general purpose and can create aggregations by practically anything, time or other fields as well. Do note that "aggregations" can be mathematical, but they can ALSO be just thought of as "grouping" sometimes.

In addition to those two, there's two even more mind blowing commands. chart is just like stats except it supports an "over" and also a "by" clause. This is mind-boggling the first few times you see or use it, but it's really powerful. Lastly, eventstats lets you do stats-like calculations on the entire data set, *without* replacing that data set. So, for instance, you can calculate a "grand total" for the data (in whole or "by" some criteria), and have that value tacked onto each event so you can do eval math/calculations with it, like find the percentages of totals. 

| Command  | Description |
| --- | --- |
| timechart | Time-series aggregations and groupings.|
| stats | General purpose aggregations and groupings.|
| chart | Add a the ability to both slice and dice the data, *at the same time*.|
| eventstats | Can calculate over the entire data set, appending its results into each event. This sounds weird and dumb, but once you see it you'll see the power.|