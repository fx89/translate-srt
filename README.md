# About
This is a vanilla Python script that makes use of the [MarianMTModel](https://huggingface.co/docs/transformers/en/model_doc/marian)
to translate SRT files from one language into another language offline (after downloading the model for the source and target language, which happens only once).

It was created for personal purposes and was only tested on one environment.

This project doesn't use PIP or any onther package manager. It is meant to work as a shell extension. 

# Table of contents
1. [Requirements](#requirements)
2. [Installation](#installation)<br />
   2.1 [Required dependencies](#dependencies)<br />
   2.2 [Setting up the script to work as a shell extension under Linux](#setup)<br />
3. [Usage](#usage)
4. [Extending the script](#extending)<br />
   4.1 [Adding new translation adapters](#adding)<br />
   4.2 [Choosing the translation adapter](#choosing)<br />

# Requirements<a name="requirements"></a>
```
Python 3.7 or higher
```


# Installation<a name="installation"></a>

## Required dependencies<a name="dependencies"></a>
The following lines install the dependencies of the script
```
python3 -m pip install --upgrade pip
python3 -m pip install sentencepiece transformers
```

## Setting up the script to work as a shell extension under Linux<a name="setup"></a>
### Make the script executable
```
chmod +x translate-srt
```

### Add the script to the path by opening the `~/.bashrc` file with your favorite editor and adding the location of the script to the path
```
nano ~/.bashrc
```
```
PATH=$PATH:[location_of_the_script]
```

### Edit the script and update the header to reference the Python executable
```
nano translate-srt
```
```
#!/usr/bin/python3.11
```


# Usage<a name="usage"></a>
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

To translate a specific SRT file in the current directory, type
```
translate-srt -f [source-language] [target-language] [source_file_name]
```

To translate a specified SRT file and output the results into a specified target file, type
```
translate-srt -f [source-language] [target-language] [source_file_name] [target_file_name]
```


# Extending the script<a name="extending"></a>
The script can be extended with multiple so called translation adapters. The term `translation adapter`
stands for a class that handles the translation of a given text from a source language into a target
language. One such adapter is the `MarianMtTranslationAdapter`, which is part of the script.

## Adding new translation adapters<a name="adding"></a>
To add a new translation adapter, perform the following steps.

### Create a new class using this interface:
```
class MyNewTranslationAdapter():
  def __init(self)__
  """
  Nothing to do here but implementation-specific initialization
  """

  def initialize(self, source_language, target_language):
  """
  Registers the source and target language.
  Performs any necessary initialization steps.
  """

  def translate(self, original_content):
  """
  Translates the given original_text (a string).
  Returns the translated text (another string).
  """
```
For a complete example, take a look at the `MarianMtTranslationAdapter` class.


### Add the new class to the translation_adapters object like this:
```
translation_adapters = {
    "MarianMtTranslationAdapter": MarianMtTranslationAdapter(),
    "MyNewTranslationAdapter": MyNewTranslationAdapter()
}
```


## Choosing the translation adapter<a name="choosing"></a>
To switch between translation adapters, use the `TRANSLATION_ADAPTER_IMPLEMENTATION` variable at the top of the script.
This is a string variable whose value has to be set to the key that identifies the transation adapter in the
`translation_adapters` object.

For example, if the `translation_adapters` looks like this:
```
translation_adapters = {
    "MarianMtTranslationAdapter": MarianMtTranslationAdapter(),
    "GoogleApiTranslationAdapter": GoogleApiAdapter(),
    "HardcodedExpressionsTranslationAdapter": HardcodedAdapter()
}
```
Then the `TRANSLATION_ADAPTER_IMPLEMENTATION` can be set to either of the following options:
- MarianMtTranslationAdapter
- GoogleApiTranslationAdapter
- HardcodedExpressionsTranslationAdapter
