# Version Management

---

## Versioning

Use _semantic versioning_ as follows.

```
Major Version . Minor Version . Patches
```

```
4.7.6
```

- Major Version
	+ Major Changes
	+ breaks the API
- Minor Version
	+ does not break the API
- Patches
	+ Bug Fixes

or in Embedded Terms

- Major Version
	+ Major Changes
	+ New Features / Functionalities
	+ HAL Upgrades
- Minor Version
	+ Introduction of new Libraries
- Patches
	+ Bug Fixes

Without a proper production release (while debuging) the Major Release should be `0` with the Version being `0.x.x`

---

## Git

### Branching strategy

For each hardware revision there is a separate branch with a name that can be uniquely assigned to the hardware.

Local branches can also be a good strategy to experiment with new code features / libraries without breaking the `main` branch.

### Commit Messages

Commit messages are subject to general due diligence at the discretion of the developer. 
These can be helpful. 
Important for the production are however the tags / releases.

### Tagging

Tags can be used at important milestones to mark a point in time in the project e.g. a new hardware driver finally works. 
In case of a not-working release, the tag quickly tells you at which point it was still working.

### Gitignore

Gitignores are optional. 
However, it is good practice if the binaries (`.hex` `.o` `.bin` `.a`) do not end up on Github. 
However, careful configuration of the `.gitignore` and `.gitkeep` files can be extensive work. 
There are many gitignore templates on the internet. 
For STM32 the standard `C` gitignore template is fair and works good even with CI/CD.
The later chapter about CI/CD describes which files must not be excluded by the gitignore.
Makefiles inside the `./Debug` directory are important for building, so this directory should not be excluded.




