# action-lambda-pack

Build binary files and pack necessary libraries for AWS Lambda

## What this can do

Have you ever feel you would like to call linux commands on AWS Lambda?
If so, this makes you happy.

This will run a build.sh script to build, and check what kind of libraries the build binaries require.
Finally this will put the binaries and minimum necessary libraries on lambda runtime.

## INPUT

### `src-path`

Source directory which has build script (Default: src)

### `build-sh`

Build script filename (Default: build.sh)

### `output-path`

Output directory of binary files and libraries (Defualt: output)

## Example

### Default Directory Structure
```
.
|-- output
`-- src
    `-- build.sh
```

### src/build.sh
```
#!/bin/sh

yum install -y git
cp -a /usr/bin/git ${OUTPUT_PATH}
```

You can write any shell script in build.sh.
You can use yum command to install or you can also download source codes and compile.

Only what you have to do is to put the necessary binary files (or anything you need) into the directory which is defined as ${OUTPUT_PATH}.

### Workflow
```
- uses: qualitiaco/action-lambda-build-pack@v1
  with:
    src-path: src
    build-sh: build.sh
    output-path: output
```

### Result
```
.
|-- output
|   |-- git
|   `-- lib
|       |-- libpcre2-8.so.0 -> libpcre2-8.so.0.5.0
|       `-- libpcre2-8.so.0.5.0
`-- src
    `-- build.sh
```

## Samples

Sample code is in

    https://github.com/qualitiaco/action-lambda-build-pack-sample