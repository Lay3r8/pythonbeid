# python-beid - BEID helpers for Python

Those helpers are meant to be used on a RaspberryPi 3 model B v1.2 with Raspbian Buster.

## Prerequesite

Basicaly, the helpers only need pyscard, and the drivers for the reader (libacr38u for the "official" Beid readers).

Btw, for pyscard to install and work correctly with Python 3 (at least in Raspbian Buster), one should compile and install it from git sources:

```bash
sudo apt-get install swig libpcsclite-dev libacr38u python3-setuptools build-essential git
git clone https://github.com/LudovicRousseau/pyscard.git
cd pyscard
python3 setup build_ext install
cd ..
rm -fr pyscard
```

I also had to install the following packages before it could be recognized by the OS:

```bash
sudo apt install pcscd opensc libnss3-tools libccid libasccid1 -y
```

## Installation

```
git clone https://github.com/Lapin-Blanc/pythonbeid.git
cd pythonbeid
python3
```

## Usage

```python
from beid import BeidReader
from pprint import pprint

class MyReader(BeidReader):
    def on_inserted(self, card):
        pprint(card.read_infos())

my_reader = MyReader()

print(my_reader.card.num_carte)
print(my_reader.card.num_nat)
```

## Troubleshooting

Install pcsc-tools and make sure that the OS is able to recognize the e-reader

```bash
# Plug your device
dmesg -T
# You shoud see a product named "Smart Card Reader Interface"

apt install pcsc-tools
pcsc_scan
```
