# Git Internals Presentation

## Demo Instructions
1. Make a demo directory and "cd" into it.
  * `mkdir demo && cd demo`
2. Initialize git repository.
  * `git init`
3. Split terminal horizontally (Ctrl + Shift + D in Hyper.js).
4. Execute `watch -d "find .git/objects -type f -printf \"%Tr %p\n\"| sort -n | cat --number"` in 2nd terminal to the right.
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

## Generating Slides

    decktape http://localhost:8000/ slides.pdf
