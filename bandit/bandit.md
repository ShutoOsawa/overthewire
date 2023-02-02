## Level 0

```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

## Level 1
```
cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```

## Level 2
```
cat -
```
does not work since cat with - is considered as stdin

```
cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```

## Level 3
```
cat "spaces in this filename"
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```

## Level 4
```
cd inhere
ls -al
cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```

## Level 5
```
cat ./-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```

## Level 6
```
find . -size 1033c
cat ./maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```

## Level 7