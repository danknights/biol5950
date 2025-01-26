# Listing and loading modules

The MSI Staff have installed and maintained an extensive library of external packages, using the `module` system.

### List all available modules
```bash
module avail
```

### List all modules matching "spades" (e.g. for assembly)
```bash
module avail spades
```

### Load the "spades" module version 3.15.5
```bash
module load spades/3.15.5
```

### Run `spades.py`
```bash
spades.py --version
```

### Optional: load the "python" module
If `spades.py` did not run, it may be necessary to load the `python` module and then run `spades.py` again.
```bash
module load python
```

Note: modules are not loaded automatically when you log in. If you need a particular module, you have to load it every time you log in.
