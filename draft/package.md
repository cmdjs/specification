# Packaging / draft

-----


## Package Descriptor File

Each package must provide a top-level package descriptor, "package.json".


### Required Fields

- root
- name
- version


### Optional Fields


## Package Distribution


## Sample Code

**A typical sample**

```
{
    "root": "arale",
    "name": "overlay",
    "version": "1.0.0",
    "description": "Overlay is a mask covering.",
    "author": "Hsiaoming Yang <lepture@me.com>",
    "repository": {
        "type": "git",
        "url": "https://github.com/arale/overlay.git"
    },
    "bugs": {
        "url": "https://github.com/arale/overlay/issues"
    },
    "dependencies": {
        "arale/widget": "1.0.x",
        "arale/position": "1.0.0",
        "arale/iframe-shim": ">=1.0.0"
    },
    "engines": {
        "seajs": ">2.0.0"
    }
}
```
