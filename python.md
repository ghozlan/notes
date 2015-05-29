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


## line_profiler
### Installation

Using the pip package
```
sudo pip install line_profiler
```

### Usage

1. Insert ```@profiler``` decorator before the functions you want to profile
  ```
  @profile
  def slow_function(a, b, c):
      ...
  ```

2. Run the profiler
  ```
  kernprof -l -v script_to_profile.py
  ```

3. If you want to view the results later
  ```
  python -m line_profiler script_to_profile.py.lprof
  ```
  
  [Reference](https://github.com/rkern/line_profiler)

## memory_profiler
### Installation

Using the pip package
```
pip install -U memory_profiler
pip install psutil
```
psutils improves the performance of memory_profiler

### Usage

1. Insert ```@profiler``` decorator before the functions you want to profile.

2. Run the profiler
  ```
  python -m memory_profiler script_to_profile.py
  ```


[Reference for cProfile, line_profiler and memory_profiler](http://www.huyng.com/posts/python-performance-analysis/)
