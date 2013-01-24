# Packaging / draft

-----


## Package Descriptor File

Each package must provide a top-level package descriptor, "package.json".


### Required Fields

- root
- name
- version


### Optional Fields

- description
- keywords
- author
- repository
- bugs
- license
- scripts

## Extendable Fields


## Sample Code

**A typical sample**

```
{
    "root": "arale",
    "name": "overlay",
    "version": "1.0.0",
    "description": "Overlay is a mask covering.",
    "keywords": ["mask", "dom"],
    "author": "Hsiaoming Yang <lepture@me.com>",
    "repository": {
        "type": "git",
        "url": "https://github.com/arale/overlay.git"
    },
    "bugs": {
        "url": "https://github.com/arale/overlay/issues"
    },
    "license": {
        "type": "BSD",
        "url": "http://opensource.org/licenses/BSD-2-Clause"
    },
    "scripts": {
        "prebuild": "prebuild.js",
        "test": "make test"
    }
}
```

**A mininal sample**

```
{
    "root": "arale",
    "name": "overlay",
    "version": "1.0.0"
}
```
