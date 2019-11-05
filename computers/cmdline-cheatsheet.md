
* **Intersection** of two sorted files: `comm -1 -2 file1 file2`.  
  `-1` and `-2` are there to discard columns which are the diff between the sets
* **Regexp** match and print: `gawk '{ if (match($0,/regexp-with-()/,m)) print m[1] }`  
* **Json** parse and print: `jq -r .<field>.<field>`  
  `-r` means that no quotes are printed
