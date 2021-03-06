From: https://leetcode.com/problems/word-frequency/

192. Word Frequency

Write a bash script to calculate the frequency of each word in a text file words.txt.

For simplicity sake, you may assume:

words.txt contains only lowercase characters and space ' ' characters. (Makes it easy to write in one line.)
Each word must consist of lowercase characters only. (Still makes it easier to write in one line.)
Words are separated by one or more whitespace characters. (Makes it easy to slice.)
Example:

Assume that words.txt has the following content:

the day is sunny the the
the sunny is is
Your script should output the following, sorted by descending frequency:

the 4
is 3
sunny 2
day 1

Note:
Don't worry about handling ties, it is guaranteed that each word's frequency count is unique.
Could you write it in one-line using Unix pipes? (Yes, it was setup this way above.)

Solution:
cat words.txt | tr ' ' '\n' | sed '/^[[:space:]]*$/d' | sort | uniq -c | sed 's/^[ \t]*//;s/[ \t]*$//' | sort -n -r | awk '{print $2,$1}'

Explanation (By command) -> 
cat (Concatenate) gets the text from file and is now in your output stream. 

tr (translate) which is used to replace whitespace characters with newlines. This makes it so every word is on it's own line alone.

sed (stream editor), got the filter from Google which strips blank lines. 

sort, now the input is easy to sort which by default puts it in alphabetical order grouped with all of its duplicates.

uniq, strips away duplicates. It also gives you the count of each word with the "-c" flag which is the crux of what the problem wants.

sed(stream editor), again to strip whitespace for the next command.

sort, we want to sort the remaining input by number in reverse order to get the output the way the problem wants.

awk, simple awk program that just gets two input on every line and switches the the first and second field which effectively reverses the order to get the order what we want.