# `modifyPatches`

## NOTE

The master branch contains the (unchanged) code for OpenFOAM-2.1.x written by
[Hisham El Safti](hsafti@gmial.com) in January 2013. The original code is
downloaded from
[openfoamwiki](https://openfoamwiki.net/images/7/75/ModifyPatches-2.1.x.tar.gz)

**For a more recent version of OpenFOAM, check out other branches (at the moment:
`2206`).**

---

## Purpose

`modifyPatches` modifies the `constant/polyMesh/boundary` file on the commandline without the need to manually edit the file. This is especially usefull when using utilites like `splitMesh` or when importing mesh from other third-party softwares. For example, when the utility `gmshToFoam` converts a Gmsh mesh (`.msh`), it has no information about the type of the patches it convert; it only set the type of all patches to `patch` in the `constant/polyMesh/boundary`.

It can:
- Change the type of a non-null patch (of size greater than zero) to:
  - `empty`
  - `wall`
  - `wall`
  - `wedge`
  - `symmetry`
  - `cyclic`
  - `processor`,
- Remove a given null patch,
- Create a null patch of a given name at the end of the
`constant/polyMesh/boundary` file.


## Usage

To get help on all the available options:

```sh
modifyPatches -help
```

Examples of use:

```sh
modifyPatches -empty frontAndBack
modifyPatches -null Master
```


## Build

To build the source:

```sh
# (Optional) create the `applications/utilities` directory in user directory
mkdir -p $WM_PROJECT_USER_DIR/applications/utilites
cd $_

# Clone the repository
git clone https://github.com/reverseila/modifyPatches

# Build using OpenFOAM's built-in build system utility
wmake -j
```


## Notes

- The `constant/polyMesh/boundary` file is overwritten.
- The application can read one value for each option (for two `empty` patches use the utility twice)
- The processor patch is set to `0` processor and `1` neighbour
 processor by default
- The `cyclic` patch does not add a `neighbourPatch` keyword


## History

- First version added for OpenFOAM-2.1.x -- [Hisham El Safti](hsafti@gmail.com) 08:17, 11 January 2013 (CET)
