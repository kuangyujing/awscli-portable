![awscli](assets/logo.png)

## TL;DR

You can download pre-built single binary at `downloads` directory or [release](https://github.com/kuangyujing/awscli-portable/releases). It runs on Apple Silicon Macs.

[The latest version](https://github.com/kuangyujing/awscli-portable/releases/download/2.22.7/awscli-portable-2.22.7.zip) .

## Build Instruction

Install Homebrew

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Download and extract awscli source package

```sh
curl -o awscli.tar.gz https://awscli.amazonaws.com/awscli.tar.gz
tar xzf awscli.tar.gz
```

Install build tool

```sh
brew install autoconf automake libtool make
```

Set environment variable

```sh
export PATH="/opt/homebrew/opt/libtool/libexec/gnubin:$PATH"
```

Run configure script

```sh
./configure --with-install-type=portable-exe --with-download-deps
```

Build awscli

```sh
make
```

If `make` exit with errors like this:

> ERROR: Ignored the following versions that require a different python version: 4.10 Requires-Python <3.11,>=3.6; 4.6 Requires-Python <3.11,>=3.6; 4.7 Requires-Python <3.11,>=3.6; 4.8 Requires-Python <3.11,>=3.6; 4.9 Requires-Python <3.11,>=3.6; 5.0 Requires-Python <3.11,>=3.7; 5.0.1 Requires-Python <3.11,>=3.7; 5.1 Requires-Python <3.11,>=3.7; 5.10.0 Requires-Python <3.12,>=3.7; 5.10.1 Requires-Python <3.12,>=3.7; 5.11.0 Requires-Python <3.12,>=3.7; 5.12.0 Requires-Python <3.12,>=3.7; 5.13.0 Requires-Python <3.13,>=3.7; 5.13.1 Requires-Python <3.13,>=3.7; 5.13.2 Requires-Python <3.13,>=3.7; 5.2 Requires-Python <3.11,>=3.7; 5.3 Requires-Python <3.11,>=3.7; 5.4 Requires-Python <3.11,>=3.7; 5.4.1 Requires-Python <3.11,>=3.7; 5.5 Requires-Python <3.12,>=3.7; 5.6 Requires-Python <3.12,>=3.7; 5.6.1 Requires-Python <3.12,>=3.7; 5.6.2 Requires-Python <3.12,>=3.7; 5.7.0 Requires-Python <3.12,>=3.7; 5.8.0 Requires-Python <3.12,>=3.7; 5.9.0 Requires-Python <3.12,>=3.7; 6.0.0 Requires-Python <3.13,>=3.8; 6.1.0 Requires-Python <3.13,>=3.8; 6.2.0 Requires-Python <3.13,>=3.8; 6.3.0 Requires-Python <3.13,>=3.8; 6.4.0 Requires-Python <3.13,>=3.8; 6.5.0 Requires-Python <3.13,>=3.8; 6.6.0 Requires-Python <3.13,>=3.8; 6.7.0 Requires-Python <3.13,>=3.8; 6.8.0 Requires-Python <3.13,>=3.8; 6.9.0 Requires-Python <3.13,>=3.8
> ERROR: Could not find a version that satisfies the requirement pyinstaller==5.13.2 (from versions: 2.0, 2.1, 3.0, 3.1, 3.1.1, 3.2, 3.2.1, 3.3, 3.3.1, 3.4, 3.5, 3.6, 4.0, 4.1, 4.2, 4.3, 4.4, 4.5, 4.5.1, 6.10.0, 6.11.0, 6.11.1)
> ERROR: No matching distribution found for pyinstaller==5.13.2

De-grade python to 3.9

```sh
brew install python@3.9
```

And force Homebrew use 3.9

brew unlink python@3.12
brew unlink python@3.13
brew link --force python@3.9
```

Then `make` again.

If success, you can see these logs:

> 15712 INFO: Re-signing the EXE
> 15733 INFO: Building EXE from EXE-00.toc completed successfully.
> 15769 INFO: checking COLLECT
> 15769 INFO: Building COLLECT because COLLECT-00.toc is non existent
> 15769 INFO: Building COLLECT COLLECT-00.toc
> 19786 INFO: Building COLLECT COLLECT-00.toc completed successfully.
> Copying contents of build/exe/dist/aws_completer into build/exe/aws/dist
> Copying contents of exe/assets into build/exe/aws
> Update metadata values {'distribution_source': 'source-exe'}
> Deleted build directory: build/exe/build
> Deleted build directory: build/exe/dist
> Built exe at ./build/exe/aws

Now, point to `build/exe/aws/dist`.

Congraturations! `aws` and `aws_completer` is the executable single binaries.
