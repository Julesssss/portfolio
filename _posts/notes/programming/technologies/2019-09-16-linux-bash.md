---
layout: post
title: Advanced Bash / Zsh
date:   2019-09-16 10:25:00 +0100
categories: programming technologies linux bash zsh
permalink: /notes/technologies/linux-bash-zsh
---
### General, useful things
`curl cheat.sh/command_to_search` shows a cheatsheet with options for this command  

_(move this into another post. I don't use it often enough)_  
`file_or_command | tee filename` It takes an input, outputs it into the console and at the same time saves it into a file.

### Processing files and data
* `find . -iname "*file_to_search*"` search something at current directory  
* `locate file_to_search` search through whole computer
* `rg` general searching through data files. Better than `grep -r`
* `diff -y --suppress-common-lines file1 file2 | grep '^' | wc -l` count number of changes between 2 files
<!--more-->

#### Analyze logs in real time
With `less +F` we can inspect the file, stop to read and resume in real time.
The advantage over `tail -f` is, with the former we can inspect the logs, but if there's an error or something we want to stop and see, we have to exit and `cat` or `vim` the file.  
~~~ bash
less +F file_to_inspect # real time
ctrl + c # stops
shift + F # resumes
~~~

### Discard normal & error output of a command
`> /dev/null` Redirects standard output to /dev/null  
`2>&1` redirects error output to same as standard output
~~~ bash
command_to_execute > /dev/null 2>&1
~~~

### Vim
#### Redirect input into a Vim buffer
`input | vim -` This, run from bash, outputs the result of a command or a file into a vim buffer, where we can do whatever with it, without modifying the original source.     

#### Useful vim commands  
All of this are executed in command mode  

`:w filename` - writes the content into a file with the following name  
`:%! grep -v delete-this` - execute bash commands for our file content. This example will delete all the lines from our file, which contain the String `delete-this`.  
`:%s/originalstring/replacement/gc` - replaces _originalstring_ for _replacement_. `g` is do this for all matches. `c` is interactive.  
`:set rnu` - see relative line numbers. `:set rnu!` turns off.  

##### Delete something  
`:-6-4d` deletes from the relative line `-6` to `-4`

This commands may be run with `c` instead of `d`, and it will do the same, and open `insert mode` directly    
`di"` when run inside two `"` it will delete the content between them.  
`dt.` delete from my position until the next `.`  
`df.` delete from my position until, and including, the next `.`

##### Search for something
`f` - find and travel to next ocurrence. For example `f.` searches for the next `.`

`/whatever` - searches for the string in the documment. Forward search  
`?whatever` - reverse search. `n` will now search back  

`shift + n` `n` - go to previous / next match  
`ggn` `Gn` - go to first / last match  
`*` `#` - searches for next / previous ocurrence of current word  

##### Copy and paste  
`:-6,-4co.` copies from the relative lines `-6` to `-4` into your current position    

`shift + v` select whole lines  
`y` / `d` copy / cut  
`P` / `p` paste before / after the cursor

##### Misc
`:set nu` - see line numbers, `:set nu!` turns them off  


#### Vimdiff  
Useful to compare changes between up to 4 files at once. It uses the same commands as vim.  

`ctrl + w` `direction arrow` moves the cursor in between file windows  
`:qa` quit all windows without saving  
`:wqa` same but saving  

### Awk  
Language processor. Useful to process `.csv` or files which are structured by columns. By default, it separates columns **by whitespaces**.  

#### Change line-separator
`awk -F '\t' '{print}' file.txt` Uses **tabs** instead of spaces as separator.

#### Working with filters  
`awk '$19 == "S"' file.txt` show lines where the column #19 is equal to _S_
`awk -F '\t' '$2 == "18249"' file.txt` uses both a filter and another line separator at the same time

`awk '{print $4}' file.txt | sort | uniq` print duplicates entries only once  
`awk -F '\t' '$2 == "18249" || $2 == "18258"' file.txt` one condition **or** the other

#### Working with columns
`awk '{print $4}' file.txt` Prints only column #4  
`awk '{print NR, $4}' file.txt` Print only column #4 with line number  
`awk 'length($2) > 0' file.txt` print lines, where the second column has a length greater than 0.  

#### Regex
`awk '$2 ~ /^[0-9]+$/' fichero.txt` get columns for which the following regex is true  
`!~` regex negation  

## Reference(s)
[https://github.com/jlevy/the-art-of-command-line?utm_campaign=explore-email&utm_medium=email&utm_source=newsletter&utm_term=weekly](https://github.com/jlevy/the-art-of-command-line?utm_campaign=explore-email&utm_medium=email&utm_source=newsletter&utm_term=weekly)  
[https://www.youtube.com/watch?v=l8iXMgk2nnY](https://www.youtube.com/watch?v=l8iXMgk2nnY)  
[https://www.youtube.com/watch?v=1alWK5ByNMc](https://www.youtube.com/watch?v=1alWK5ByNMc)
