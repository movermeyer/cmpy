# cmpy
[![License](https://pypip.in/license/cmpy/badge.svg)](https://pypi.python.org/pypi/cmpy/)
[![Latest Version](https://pypip.in/version/cmpy/badge.svg)](https://pypi.python.org/pypi/cmpy/)
[![Downloads](https://pypip.in/download/cmpy/badge.svg)](https://pypi.python.org/pypi/cmpy/)

A simple utility for detecting differences in directories and files.

### Installation

You can get cmpy with pip:

```
pip install cmpy
```

### Overview

Comparison of files and directories in `cmpy` is handled with the `FCompare` and `DCompare` classes, respectively. Files
can also be compared using the static `shallow_fcmp()` and `deep_fcmp()` methods. As the names suggest, the former performs 
a shallow comparison (less strict comparison, faster and less resource intensive), while the latter performs a deep comparison
(strict comparison, slower, more resource intensive). 

For additional information on the comparison methods and classes, see the docstring in `cmpy.py`.

### Usage

#### Comparing Files

```python
# Instantiate a file compare object between to files
f = FCompare('foo/bar', 'bar/foo')

# Compare the files (returns True or False)
f.compare()
```

Optional arguments may be provided

```python
# Perform a shallow comparison (default behavior)
f = FCompare('foo/bar', 'bar/foo', shallow=True)

# Perform a deep comparison
f = FCompare('foo/bar', 'bar/foo', shallow=False)

# Change the default buffer size (for deep comparison). Default is 2**10 bytes
f = FCompare('foo/bar', 'bar/foo', buffer_size=2**8)
```

Files can also be compared without instantiating an object

```python
# Shallow comparison
shallow_fcmp('foo/bar', 'bar/foo')

# Deep comparison
deep_fcmp('foo/bar', 'bar/foo')

# Deep comparison specifying buffer size
deep_fcmp('foo/bar', 'bar/foo', 2**8)
```

#### Comparing Directories:

```python
# Instantiate a directory compare object between to directories
d = DCompare('foo/bar/', 'bar/foo/')

# Compare the directories (returns True or False)
d.compare()
```

Optional arguments may be provided

```python
# Perform a shallow comparison (default behavior)
d = DCompare('foo/bar/', 'bar/foo/', shallow=True)

# Perform a deep comparison
d = DCompare('foo/bar/', 'bar/foo/', shallow=False)

# Change the default buffer size (for deep comparison). Default is 2**10 bytes
d = DCompare('foo/bar/', 'bar/foo/', buffer_size=2**8)

# Perform a comparison non-recursively 
d = DCompare('foo/bar/', 'bar/foo/', recursive=False)

# Perform a comparison recursively (default behavior)
d = DCompare('foo/bar/', 'bar/foo/', recursive=True)
```

The `DCompare` class has various properties on it

```python
d = DCompare('foo/bar/', 'bar/foo/')

# The names of files in the first directory
d.dir1_files

# The names of directories in the first directory
d.dir1_directories

# The names of the entries in the first directory
d.dir1_contents

# The names of files in the second directory
d.dir2_files

# The names of directories in the second directory
d.dir2_directories

# The names of the entries in the second directory
d.dir2_contents

# The names of the entries in the first directory which are not in the second directory
d.dir1_unique

# The names of the entries in the second directory which are not in the first directory
d.dir2_unique

# The names of the entries found in both directories
d.common
```
