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

### Optional: load the "python" module
Sometimes this is necessary to use certain software modules like Spades:
```bash
module load python
```

### Run `spades.py`
```bash
spades.py --version
```

Note: modules are not loaded automatically when you log in. If you need a particular module, you have to load it every time you log in.
