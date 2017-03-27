# GYB-Template
Xcode template for GYB (Generate Your Boilerplate) tool.

This template is composed of 2 files:
* `___FILEBASENAMEASIDENTIFIER___.swift` — The swift file wich will contain the generated code. This file **must** be created by the template to add it in the compile sources list. This file should not be modified manually, it will be overridden at each build.
* `___FILEBASENAMEASIDENTIFIER___.swift.gyb` — The boilerplate file. Write your boilerplate code here.


> **Note:** The file names are important. The gyb boilerplate must have the same name as the pure swift file, with the `.gyb` extension. If you rename one of the file , you must rename the other one accordingly.

# Installation

## Template
* Download [GYB Template](https://github.com/RaphaelRO/GYB-Template/archive/master.zip).
* Copy the `Generate Your Boilerplate` folder into `~/Library/Developer/Xcode/Templates/File Templates/`.

## GYB Tool

Download the GYB tool from the apple Swift repository, and add execution permissions:
```bash
$ curl -O https://raw.githubusercontent.com/apple/swift/master/utils/gyb.py
$ chmod +x gyb.py
```

In project's **Build Phases**, add a new `Run script phase`:

```bash
find . -name '*.gyb' | while read file; do <path/to/gyb.py> --line-directive '' -o "${file%.gyb}" "$file"; done
```

> **Note:** The script must be executed **before** the `Compile Sources` phase.

> How it works: During the build phase, the script will search all `*.gyb` files, and run the GYB tool to genereate the final `.swift` file.


## Python 3

Apparently, the GYB tool is only compatiable with **Python 2**. The Swift repository contain a wrapper that force GYB execution on Pyhton 2. You can install this wrapper using the following command:

```bash
$ curl -O https://raw.githubusercontent.com/apple/swift/master/utils/gyb
```

To enable the wrapper, simply replace the `<path/to/gyb.py>` in the **Build Phases** section with the wrapper path.
