# Kaldi Active Grammar

> **Python Kaldi speech recognition with grammars that can be set active/inactive dynamically at decode-time**

[![PyPI - Version](https://img.shields.io/pypi/v/kaldi-active-grammar.svg)](https://pypi.python.org/pypi/kaldi-active-grammar/)
[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/kaldi-active-grammar.svg)](https://pypi.python.org/pypi/kaldi-active-grammar/)
[![PyPI - Wheel](https://img.shields.io/pypi/wheel/kaldi-active-grammar.svg)](https://pypi.python.org/pypi/kaldi-active-grammar/)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/kaldi-active-grammar.svg?logo=python)](https://pypi.python.org/pypi/kaldi-active-grammar/)
[![GitHub - Downloads](https://img.shields.io/github/downloads/daanzu/kaldi-active-grammar/total?logo=github)](https://github.com/daanzu/kaldi-active-grammar/releases)
<!-- [![GitHub - Downloads](https://img.shields.io/github/downloads/daanzu/kaldi-active-grammar/latest/total?logo=github)](https://github.com/daanzu/kaldi-active-grammar/releases/latest) -->
[![Batteries-Included](https://img.shields.io/badge/batteries-included-green.svg)](https://github.com/daanzu/kaldi-active-grammar/releases)
[![Gitter](https://badges.gitter.im/kaldi-active-grammar/community.svg)](https://gitter.im/kaldi-active-grammar/community)

[![Donate](https://img.shields.io/badge/donate-GitHub-pink.svg)](https://github.com/sponsors/daanzu)
[![Donate](https://img.shields.io/badge/donate-Patreon-orange.svg)](https://www.patreon.com/daanzu)
[![Donate](https://img.shields.io/badge/donate-PayPal-green.svg)](https://paypal.me/daanzu)
[![Donate](https://img.shields.io/badge/preferred-GitHub-black.svg)](https://github.com/sponsors/daanzu)
[**GitHub** is matching (only) my **GitHub Sponsors** donations.]

> Python package developed to enable context-based command & control of computer applications, as in the [Dragonfly](https://github.com/dictation-toolbox/dragonfly) speech recognition framework, using the [Kaldi](https://github.com/kaldi-asr/kaldi) automatic speech recognition engine.

Normally, Kaldi decoding graphs are **monolithic**, require **expensive up-front off-line** compilation, and are **static during decoding**. Kaldi's new grammar framework allows **multiple independent** grammars with nonterminals, to be compiled separately and **stitched together dynamically** at decode-time, but all the grammars are **always active** and capable of being recognized.

This project extends that to allow each grammar/rule to be **independently marked** as active/inactive **dynamically** on a **per-utterance** basis (set at the beginning of each utterance). Dragonfly is then capable of activating **only the appropriate grammars for the current environment**, resulting in increased accuracy due to fewer possible recognitions. Furthermore, the dictation grammar can be **shared** between all the command grammars, which can be **compiled quickly** without needing to include large-vocabulary dictation directly.

### Features

* **Binaries:** The Python package **includes all necessary binaries** for decoding on **Windows/Linux/MacOS**. Available on [PyPI](https://pypi.org/project/kaldi-active-grammar/#files).
    * Binaries are generated from my [fork of Kaldi](https://github.com/daanzu/kaldi-fork-active-grammar), which is only intended to be used by kaldi-active-grammar directly, and not as a stand-alone library.
* **Pre-trained model:** A compatible **general English Kaldi nnet3 chain model** is trained on **~3000** hours of open audio. Available under [project releases](https://github.com/daanzu/kaldi-active-grammar/releases).
    * [**Model info and comparison**](docs/models.md)
    * Improved models are under development.
* **Plain dictation:** Do you just want to recognize plain dictation? Seems kind of boring, but okay! There is an [**interface for plain dictation** (see below)](#plain-dictation-interface), using either your specified `HCLG.fst` file, or KaldiAG's included pre-trained dictation model.
* **Dragonfly/Caster:** A compatible [**backend for Dragonfly**](https://github.com/daanzu/dragonfly/tree/kaldi/dragonfly/engines/backend_kaldi) is under development in the `kaldi` branch of my fork, and has been merged as of Dragonfly **v0.15.0**.
    * See its [documentation](https://dragonfly2.readthedocs.io/en/latest/kaldi_engine.html), try out a [demo](https://github.com/dictation-toolbox/dragonfly/blob/master/dragonfly/examples/kaldi_demo.py), or use the [loader](https://github.com/dictation-toolbox/dragonfly/blob/master/dragonfly/examples/kaldi_module_loader_plus.py) to run all normal dragonfly scripts.
    * You can try it out easily on Windows using a **simple no-install package**: see [Getting Started](#getting-started) below.
    * [Caster](https://github.com/dictation-toolbox/Caster) is supported as of KaldiAG **v0.6.0** and Dragonfly **v0.16.1**.
    * Support for KaldiAG **v1.2.0** has been merged as of Dragonfly **v0.20.0**! Improvements include **Improved Recognition**, **Weights on Any Elements**, **Pluggable Alternative Dictation**, **Stand-alone Plain Dictation Interface**, and various bug fixes & optimizations. For details and previous versions' improvements, see [project releases](https://github.com/daanzu/kaldi-active-grammar/releases).

### Demo Video

[![Demo Video](docs/demo_video.png)](https://youtu.be/Qk1mGbIJx3s)

### Donations are appreciated to encourage development.

[![Donate](https://img.shields.io/badge/donate-GitHub-pink.svg)](https://github.com/sponsors/daanzu)
[![Donate](https://img.shields.io/badge/donate-Patreon-orange.svg)](https://www.patreon.com/daanzu)
[![Donate](https://img.shields.io/badge/donate-PayPal-green.svg)](https://paypal.me/daanzu)
[![Donate](https://img.shields.io/badge/preferred-GitHub-black.svg)](https://github.com/sponsors/daanzu)
[**GitHub** is currently matching all my donations $-for-$.]

### Related Repositories

* [daanzu/kaldi-grammar-simple](https://github.com/daanzu/kaldi-grammar-simple)
* [daanzu/speech-training-recorder](https://github.com/daanzu/speech-training-recorder)
* [daanzu/dragonfly_daanzu_tools](https://github.com/daanzu/dragonfly_daanzu_tools)

## Getting Started

Want to get started **quickly & easily on Windows**?
Available under [project releases](https://github.com/daanzu/kaldi-active-grammar/releases):

* **`kaldi-dragonfly-winpython`**: A self-contained, portable, batteries-included (python & libraries & model) distribution of kaldi-active-grammar + dragonfly2. Just unzip and run!
* **`kaldi-dragonfly-winpython-dev`**: [*more recent development version*] A self-contained, portable, batteries-included (python & libraries & model) distribution of kaldi-active-grammar + dragonfly2. Just unzip and run!
* **`kaldi-caster-winpython-dev`**: [*more recent development version*] A self-contained, portable, batteries-included (python & libraries & model) distribution of kaldi-active-grammar + dragonfly2 + caster. Just unzip and run!

Otherwise...

### Setup

**Requirements**:
* Python 2.7 or 3.6+; *64-bit required!*
* OS: *Windows/Linux/MacOS*
* Only supports Kaldi left-biphone models, specifically *nnet3 chain* models, with specific modifications
* ~1GB+ disk space for model plus temporary storage and cache, depending on your grammar complexity
* ~1GB+ RAM for model and grammars, depending on your model and grammar complexity

Install Python package, which includes necessary Kaldi binaries:

```
pip install kaldi-active-grammar
```

Download compatible generic English Kaldi nnet3 chain model from [project releases](https://github.com/daanzu/kaldi-active-grammar/releases). Unzip the model and pass the directory path to kaldi-active-grammar constructor.

Or use your own model. Standard Kaldi models must be converted to be usable. Conversion can be performed automatically, but this hasn't been fully implemented yet.

### Troubleshooting

* Errors installing
    * Make sure you're using a 64-bit Python.
    * You must install via `pip install kaldi-active-grammar` (directly or indirectly), *not* `python setup.py install`, in order to get the required binaries.
    * Update your `pip` (to at least `19.0+`) by executing `python -m pip install --upgrade pip`, to support the required python binary wheel package.
* Try deleting the Kaldi model `*.tmp` directory and rerunning.
* For reporting issues, try running with `import logging; logging.basicConfig(level=1)` at the top of your main file to enable full debugging logging.

## Documentation

Documentation is sorely lacking currently. To see example usage, examine the [**backend for Dragonfly**](https://github.com/daanzu/dragonfly/tree/kaldi/dragonfly/engines/backend_kaldi).

The KaldiAG API is pretty low level, but basically: you define a set of rules, and send in audio data, along with a bit mask of which rules are active at the beginning of each utterance, and receive back the recognized rule and text. The easy way is to go through Dragonfly, which makes it easy to define the rules, contexts, and actions.

### Plain dictation interface

```python
import sys, wave
from kaldi_active_grammar import PlainDictationRecognizer
recognizer = PlainDictationRecognizer()  # Or supply non-default model_dir, tmp_dir, or fst_file
filename = sys.argv[1] if len(sys.argv) > 1 else 'test.wav'
wave_file = wave.open(filename, 'rb')
data = wave_file.readframes(wave_file.getnframes())
output_str, likelihood = recognizer.decode_utterance(data)
print(repr(output_str), likelihood)  # -> 'it depends on the context' 2.1386399269104004
```

## Contributing

Issues, suggestions, and feature requests are welcome & encouraged. Pull requests are considered, but project structure is in flux.

Building:

* Linux/MacOS: `python setup.py bdist_wheel` (see `CMakeLists.txt` for details)
* Windows: currently quite complicated (see [my fork of Kaldi](https://github.com/daanzu/kaldi-fork-active-grammar), then similar to Linux/MacOS)

Donations are appreciated to encourage development.

[![Donate](https://img.shields.io/badge/donate-GitHub-pink.svg)](https://github.com/sponsors/daanzu)
[![Donate](https://img.shields.io/badge/donate-Patreon-orange.svg)](https://www.patreon.com/daanzu)
[![Donate](https://img.shields.io/badge/donate-PayPal-green.svg)](https://paypal.me/daanzu)
[![Donate](https://img.shields.io/badge/preferred-GitHub-black.svg)](https://github.com/sponsors/daanzu)
[**GitHub** is currently matching all my donations $-for-$.]

## Author

* David Zurow ([@daanzu](https://github.com/daanzu))

## License

This project is licensed under the GNU Affero General Public License v3 (AGPL-3.0-or-later). See the LICENSE.txt file for details. If this license is problematic for you, please contact me.

## Acknowledgments

* Based on and including code from [Kaldi ASR](https://github.com/kaldi-asr/kaldi), under the Apache-2.0 license.
* Code from [OpenFST](http://www.openfst.org/) and [OpenFST port for Windows](https://github.com/kkm000/openfst), under the Apache-2.0 license.
* [Intel Math Kernel Library](https://software.intel.com/en-us/mkl), copyright (c) 2018 Intel Corporation, under the [Intel Simplified Software License](https://software.intel.com/en-us/license/intel-simplified-software-license).
* Modified generic English Kaldi nnet3 chain model from [Zamia Speech](https://github.com/gooofy/zamia-speech), under the LGPL-3.0 license.
