# SED Command Usage
1. sed Command:
Used for search and replace in files or outputs. Example:

 bash
Copy code
sed 's/error/ERROR/g' file.txt
 This replaces all occurrences of error with ERROR in file.txt.



2. vi (or Vim) Editor:
Use :%s/pattern/replacement/g for search and replace. Example:

 vim
Copy code
:%s/error/ERROR/g
 This replaces all occurrences of error with ERROR in the entire file.



3. Targeting Exact Matches:
Use regular expressions to replace only specific words. Example:

 vim
Copy code
:%s/\(^\|\s\)tmpfs\(\s\|$\)/\1mymssg\2/g
 This replaces only standalone tmpfs with mymssg, not devtmpfs.



4. Working with Command Output:
Modify command output with sed. Example:

 bash
Copy code
df -h | sed 's/\(^\|\s\)tmpfs\(\s\|$\)/\1mymssg\2/g'
 This replaces only tmpfs in df -h output.



Key Point:
 Regular expressions help fine-tune search and replace, ensuring precise replacements.


------



# AWK Command 


1. awk Overview
awk is a powerful text processing tool primarily used for:
Column-based data manipulation


Mathematical operations (sum, average, etc.)


Pattern matching and filtering


Text formatting and output


Key Commands:
Extract columns:

 bash
CopyEdit
awk '{print $1, $3}' file.txt


Sum values in a column:

 bash
CopyEdit
awk '{sum += $2} END {print "Total:", sum}' file.txt


Filter lines based on a condition:

 bash
CopyEdit
awk '$3 > 1000' file.txt


Format output nicely:

 bash
CopyEdit
awk '{printf "User: %s, ID: %s\n", $1, $2}' users.txt


Important Notes:
awk works best with line-based, plain text files.


Can be used to process command outputs like df, ps, etc.


Not suitable for binary files or complex formats like JSON/XML (unless converted).



2. Common Linux Command-Line Tools
sed – Stream Editor (text substitution)


Example:

 bash
CopyEdit
sed 's/error/ERROR/g' file.txt


grep – Search for text patterns (supports regex)


Example:

 bash
CopyEdit
grep "failed" /var/log/syslog


cut – Extract specific columns (by delimiter)


Example:

 bash
CopyEdit
cut -d ':' -f1 /etc/passwd


sort – Sort lines (alphabetically or numerically)


Example:

 bash
CopyEdit
sort -n file.txt


uniq – Remove duplicate lines


Example:

 bash
CopyEdit
sort file.txt | uniq


xargs – Build and execute command lines from input


Example:

 bash
CopyEdit
cat files.txt | xargs rm


find – Search for files (by name, type, etc.)


Example:

 bash
CopyEdit
find /var -name "*.log"


tee – Write output to file and stdout


Example:

 bash
CopyEdit
ls -l | tee list.txt


tr – Translate or delete characters


Example:

 bash
CopyEdit
tr -d '\r' < file.txt  # Remove carriage returns


head / tail – View start or end of files


Example:

 bash
CopyEdit
head -n 10 file.txt
tail -f /var/log/syslog



Summary of Useful Linux Text Processing and System Tools:
Text processing: awk, sed, grep, cut, tr, sort, uniq


File and command manipulation: xargs, find, tee, head, tail


Data processing in pipelines: Combine multiple tools together using the pipe (|) for advanced workflows.



Bonus Tip:
Many of these tools can be combined in pipelines for powerful one-liners, e.g., ps aux | awk '$3 > 10 {print $1, $3}'
Kubernetes!


----






AWK Command 


1. awk Overview
awk is a powerful text processing tool primarily used for:
Column-based data manipulation
Mathematical operations (sum, average, etc.)
Pattern matching and filtering
Text formatting and output
Key Commands:
Extract columns: bashCopyEditawk '{print $1, $3}' file.txt

Sum values in a column: bashCopyEditawk '{sum += $2} END {print "Total:", sum}' file.txt

Filter lines based on a condition: bashCopyEditawk '$3 > 1000' file.txt

Format output nicely: bashCopyEditawk '{printf "User: %s, ID: %s\n", $1, $2}' users.txt

Important Notes:
awk works best with line-based, plain text files.
Can be used to process command outputs like df, ps, etc.
Not suitable for binary files or complex formats like JSON/XML (unless converted).

2. Common Linux Command-Line Tools
sed – Stream Editor (text substitution)
Example: bashCopyEditsed 's/error/ERROR/g' file.txt

grep – Search for text patterns (supports regex)
Example: bashCopyEditgrep "failed" /var/log/syslog

cut – Extract specific columns (by delimiter)
Example: bashCopyEditcut -d ':' -f1 /etc/passwd

sort – Sort lines (alphabetically or numerically)
Example: bashCopyEditsort -n file.txt

uniq – Remove duplicate lines
Example: bashCopyEditsort file.txt | uniq

xargs – Build and execute command lines from input
Example: bashCopyEditcat files.txt | xargs rm

find – Search for files (by name, type, etc.)
Example: bashCopyEditfind /var -name "*.log"

tee – Write output to file and stdout
Example: bashCopyEditls -l | tee list.txt

tr – Translate or delete characters
Example: bashCopyEdittr -d '\r' < file.txt  # Remove carriage returns

head / tail – View start or end of files
Example: bashCopyEdithead -n 10 file.txt
tail -f /var/log/syslog


Summary of Useful Linux Text Processing and System Tools:
Text processing: awk, sed, grep, cut, tr, sort, uniq
File and command manipulation: xargs, find, tee, head, tail
Data processing in pipelines: Combine multiple tools together using the pipe (|) for advanced workflows.

Bonus Tip:
Many of these tools can be combined in pipelines for powerful one-liners, e.g., ps aux | awk '$3 > 10 {print $1, $3}'


[[Linux Command at MCX]]