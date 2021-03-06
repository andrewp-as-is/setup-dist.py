<!--
https://readme42.com
-->


[![](https://img.shields.io/pypi/v/setup-dist.svg?maxAge=3600)](https://pypi.org/project/setup-dist/)
[![](https://img.shields.io/badge/License-Unlicense-blue.svg?longCache=True)](https://unlicense.org/)
[![](https://github.com/andrewp-as-is/setup-dist.py/workflows/tests42/badge.svg)](https://github.com/andrewp-as-is/setup-dist.py/actions)

### Installation
```bash
$ [sudo] pip install setup-dist
```

### Concept
pypi/prod `setup.py` without unnecessary metadata (`keywords`, `description`, `long_description`, `classifiers`, `url`, etc)

#### Pros
+   less production code and commits

#### How it works
project metadata is stored in the distribution `PKG-INFO` file

#### Usage
```bash
$ usage: python -m setup_dist ...
```

#### Features
key|default value|environment variable
-|-|-
`name`|`os.path.basename(os.getcwd()).split(".")[0].lower()`|`SETUP_NAME`
`version`|`None`|`SETUP_VERSION`
`packages`|`setuptools.find_packages()`|`SETUP_PACKAGES`
`install_requires`|`requirements.txt` lines|`SETUP_INSTALL_REQUIRES` or `SETUP_INSTALL_REQUIRES_FILE`
`classifiers`|`classifiers.txt` lines|`SETUP_CLASSIFIERS` or `SETUP_CLASSIFIERS_FILE`
`scripts`|`scripts/` files|`SETUP_SCRIPTS`
`keywords`|`None`|`SETUP_KEYWORDS` or `SETUP_KEYWORDS_FILE`
`description`|`None`|`SETUP_DESCRIPTION`
`long_description`|`README.md` or `README.rst` content|`SETUP_LONG_DESCRIPTION` or `SETUP_LONG_DESCRIPTION_FILE`
`license`|`None`|`SETUP_LICENSE`
`url`|`None`|`SETUP_URL`

#### Examples
```bash
dist_dir="$(mktemp -d)"
export SETUP_VERSION="42"
export SETUP_DESCRIPTION="Answer to the Ultimate Question of Life, the Universe, and Everything"
python -m setup_dist sdist --dist-dir="$dist_dir"  1> /dev/null
```

twine upload
```bash
sdist="$(find "$dist_dir" -type f -name "*.tar.gz")"
twine upload --config-file=~/.pypirc "$sdist"
```

pypi/prod `setup.py`
```python
import setuptools

setuptools.setup(
    name='NAME',
    install_requires=open('requirements.txt').read().splitlines(),
    packages=setuptools.find_packages()
)
```

<p align="center">
    <a href="https://readme42.com/">readme42.com</a>
</p>
