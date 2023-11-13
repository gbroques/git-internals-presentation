# Git Internals Presentation

## Part 1 Demo Instructions
1. Make a demo directory and "cd" into it.
  * `mkdir demo && cd demo`
2. Initialize git repository.
  * `git init`
3. Split terminal horizontally (Ctrl + Shift + D in Hyper.js).
4. Execute `watch -d "find .git/objects -type f -printf \"%Tr %p\n\"| sort -n | cat --number"` in 2nd terminal to the right.
   * If the `watch` command is unavailable, here's a custom bash script which can serve the same purpose: 
   ```bash
   #!/bin/bash
   # https://gist.github.com/espaciomore/    28e24ce4f91177c0964f4f67bb5c5fda
   # https://gist.github.com/gbroques/    6ab813236b5e7490b552465196afd5d7
   ARGS="${@}"
   clear; 
   while(true); do 
   OUTPUT=$(find .git/objects -type f -printf "%T@   %Tr   %p\n" | sort -n | awk '{print $2 " " $3 " "   $4}' |   cat --number)
   clear
   printf "\n"
   echo -e "${OUTPUT[@]}"
   sleep 2
   done
   ```

5. Make a file `1.txt` with `"one text"` content.
  * `echo "one text" > 1.txt`
6. Add `1.txt` to the staging area.
  * `g add .`
7. Show `echo "one text" | git hash-object --stdin`
8. Make an "Initial commit".
  * `git commit -m "Initial commit"`
9. Make a change to `1.txt`
  * `echo "a change" >> 1.txt`
10. Make a 2nd commit.
  * `git add . && git commit -m "Second commit"`.
11. Create a new `2.txt` inside a directory `dir/`, then make a 3rd commit:
    1. `mkdir dir`
    2. `echo "two text" > dir/2.txt`
    . `git add . && git commit -m "Third commit"`

## Part 2 Demo Instructions

watch git HEAD bash script:
```bash
#!/bin/bash
# https://gist.github.com/espaciomore/28e24ce4f91177c0964f4f67bb5c5fda
# https://gist.github.com/gbroques/109615d7304bfea189c09c2709d77e96
ARGS="${@}"
clear; 
while(true); do 
  OUTPUT=$(cat .git/HEAD)
  ref=$(echo $OUTPUT | awk '{print $2}' | xargs -I {} cat .git/{})
  commit_message=$(git log --format=%B -n 1 $ref)
  clear
  printf "\n    HEAD\n"
  echo -e "        ${OUTPUT[@]}"
  printf "\n    ref:\n"
  echo -e "        ${ref}"
  printf "\n"
  echo -e "        ${commit_message}"
  sleep 2
done
```

## Generating Slides

Navigate to:

    http://localhost:8000/?print-pdf

Ctrl + P to print and save.

Alternatively `decktape`, but this doesn't render images well:

    decktape http://localhost:8000/ slides.pdf
