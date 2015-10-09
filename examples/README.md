## Examples

### Parsing the log

Example of parsing a Java GC log with [R](https://www.r-project.org/). To do this, we will use the `stringr` package.

```r
# Including stringr package for regex
library(stringr)

# Read the GC log file in
gc <- readLines("gc.log")

# Regex the matches
matches <- str_match(gc, "(\\d+)K->(\\d+)K\\((\\d+)K\\),\\s(\\d+.\\d+)\\ssecs.*\\[Times\\: user=(\\d+.\\d+) sys=(\\d+.\\d+), real=(\\d+.\\d+) secs")

# Look at what matches, now we want to filter out the NA
matches

# Filter content out and convert to a data frame
gc.df <- data.frame(na.omit(matches[,-1]), stringsAsFactors=FALSE)

# Add a column header to describe fields
colnames(gc.df) <- c("HeapUsedBeforeGC_KB","HeapUsedAfterGC_KB", "HeapCapacity_KB", "GCPauseTime_Sec", "GCUserTime_Sec", "GCSysTime_Sec", "GCRealTime_Sec")

# List out the contents of the data frame
gc.df
```