# About
This is a vanilla Python script that makes use of the [MarianMTModel]([https://www.genome.gov/](https://huggingface.co/docs/transformers/en/model_doc/marian))
to translate SRT files from one language into another language offline (after downloading the model for the source and target language, which happens only once).

It was created for personal purposes and was only tested on one environment. However, it does not use any non-vanilla dependencies, other than the MarianMTModel.

This project doesn't use PIP or any onther package manager. It is meant to work as a shell extension. 

# Requirements
```
Python 3.7 or higher
```


# Installation

## Required dependencies
The following lines install the MarianMTModel and its dependencies
```
python3 -m pip install --upgrade pip
python3 -m pip install sentencepiece transformers
```

## Setting up the script to work as a shell extension under Linux
Make the script executable
```
chmod +x translate-srt
```

Add the script to the path by opening the `~/.bashrc` file with your favorite editor and adding the location of the script to the path
```
nano ~/.bashrc
```
```
PATH=$PATH:[location_of_the_script]
```

Edit the script and update the header to reference the Python executable
```
nano translate-srt
```
```
#!/usr/bin/python3.11
```


# Usage
To print the help, just type
```
translate-srt --help
```
or
```
translate-srt
```

To translate all the SRT files in the current directory and output the results into a target directory, type
```
translate-srt [source-language] [target-language] [target_dir]
```

To translate all the SRT files from a given source directory into a given target directory, type
```
translate-srt [source-language] [target-language] [source_dir] [target_dir]
```

To rtranslate a specific SRT file in the current directory, type
```
translate-srt -f [source-language] [target-language] [source_file_name]
```

To translate a specified SRT file and output the results into a specified target file, type
```
translate-srt -f [source-language] [target-language] [source_file_name] [target_file_name]
```


# Extending the script

