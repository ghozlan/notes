# Python

## Profiler

To profile a python script ```myscript.py```, use
```
python -m cProfile myscript.py
```

To save the command line output to file, use
```
python -m cProfile myscript.py > profiler.txt
```

To write the profile results to a file instead of to stdout
```
python -m cProfile -o output_file myscript.py
```

How to read profile results in the output file?

[Reference](https://docs.python.org/2/library/profile.html)
