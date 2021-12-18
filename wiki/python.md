# Python

## Profiling
To generate a profile for a python binary at a designated output file:

`python -m cProfile -o {output_prof_file_name.prof} {my_script.py}`

To visualize the profiles with snakeviz:
`snakeviz {output_prof_file_name.prof}`

