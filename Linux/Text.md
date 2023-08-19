**cat** outputs the contents of a text file 

**less**  allows to read a text file page by page. 
- `ctrl-b` `ctrl-f` to move through the file. 
- ``/`` to search. `n-N` to move through the results. 
- `v` enters vim/nano,  the exact one is set in the [[bashrc#^ddc998]] config. 
- `F` awaits for the file updates. 


![[Pasted image 20230730102506.png]]



**grep** searches for patterns in files. 

- `i` or `--ignore-case`: Perform a case-insensitive search.
- `-r` or `--recursive`: Recursively search for the pattern in directories and subdirectories.
- `-n` or `--line-number`: Display line numbers along with matching lines.
- `-v` or `--invert-match`: Invert the match, showing lines that do not contain the pattern.
- `-w` or `--word-regexp`: Match whole words only, not substrings.
- `-l` or `--files-with-matches`: Display only the names of files that contain the pattern.
- `-L` or `--files-without-match`: Display only the names of files that do not contain the pattern.
- `-c` or `--count`: Display the count of matching lines for each file.

![[Pasted image 20230730104200.png]]

**find** recursively searches for a file like:
```bash
find / -name "name"
```
Allows for searches almost by all metadata of a [[File]] like owner name, group name, size, inode, type. 
- -exec argument allows for command execution on all found files (caution is advised)

**sed** reads the file line by line and performs operations outputting the results

- -i[suffix] creates a copy of the original file
```bash
sed -n -isuf '/error/n' filename #creates filenamesuf
```

**awk** performs complex operations on the provided text

**cmp** compares files byte by byte

**diff** compares files line by line, creates a diff-file as an output which can be used with **patch** 
- -i ignores the register
- -B ignores the empty lines

**patch** applies the diff-file creating a new file or replacing the existing one
```bash
patch -R  file < diff-file
```

**cp** copies a file

**mv** moves a file (can be used for renaming)

**head** outputs a fixed amount of lines or bytes specified
- -n 10 lines
- -c 10 bytes

**tail** outputs the end of a file 
- -f awaits new data
- -F awaits new data and informs in the case a file was moved