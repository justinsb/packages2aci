# Create ACI images from Debian packages

This is a simple tool to create an ACI image using your operating system packages.

It includes an example to build a Java7 base image in [java7](java7).

### Steps to create your ACI image:

1. Create a directory to hold your work (e.g. [java7](java7))
1. Create the [packages](java7/packages) file with a list of packages to be installed, one per line.
1. Create a [manifest](java7/manifest) file which will be your ACI manifest.
1. (Optional) Create a [postbuild](java7/postbuild) script to do any post-processing after the packages are installed.  Here, we set up a convenience symlink.
1. Run `./packages2aci <dirname>` to build your ACI image (e.g. `./packages2aci java7`)

Your ACI image is then in `<dirname>/image.aci`.  Run it using:

```
sudo rkt --insecure-skip-verify=true run java7/image.aci
```

### Limitations:

* You have to specify each package individually; it doesn't do recursive dependency analysis.
* This works using your currently installed operating system, so is OS dependent.  (This could easily be fixed by doing this inside a rkt image!)
