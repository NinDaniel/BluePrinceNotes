Found here is the timeline as we know it. To write entries into the timeline, we use the following code in the page you'd like to pull from:

`%%[clue:: 1993-10-06 (Date in YYYY-MM-DD) ~ Summary text to use ~ \^1 (optional block reference)]%%`

**TNS!** means the note does not have an exact date. Instead, we are using an approximated value.
``` dataview
TABLE WITHOUT ID
    dateformat(date(split(string(C), " ~ ")[0]), "MMMM dd, yyyy") AS "Date",
    split(string(C), " ~ ")[1] AS "Clue",
    choice(
        length(split(string(C), " ~ ")) = 3, 
        link(file.path + "#" + split(string(C), " ~ ")[2], file.name), 
        link(file.path, file.name)
    ) AS "Room"
FROM ""
WHERE clue
FLATTEN flat(list(clue)) AS C
SORT date(split(string(C), " ~ ")[0]) ASC
```
