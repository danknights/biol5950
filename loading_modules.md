# Listing and loading modules

The MSI Staff have installed and maintained an extensive library of external packages, using the `module` system.

### List all available modules
```bash
module avail
```

### List all modules matching "spades" (e.g. for assembly)
```bash
module avail | grep -i spades
```

### Load the "spades" module version 3.15.5
```bash
module load spades/3.15.5
```

### Load the "python" module to use python scripts (like "spades")
```bash
module load python
```

### Run `spades.py`
```bash
spades.py
```
