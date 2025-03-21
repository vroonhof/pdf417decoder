# pdf417decoder

This is a (hopefully temporary) fork of the python
[pdf417decoder](https://github.com/sparkfish/pdf417decoder) that adds
support for MacroPDF, aka the ability to decode files that have been
split over multiple barcodes.

It works for me and as soon as feel it is tested enough and the API is
right I will try and get it merged back into the main repository.

One issue right now is to have a good public test image with multiple
barcodes.

## Original Description
![Image of a PDF417 barcode](https://raw.githubusercontent.com/sparkfish/pdf417decoder/dev/python/images/haiku.png?id=1)

pdf417decoder is a pure Python library for decoding [PDF417 barcodes](https://en.wikipedia.org/wiki/PDF417).

Reader is capable of Error Detection and Correction according to the standards for PDF417 which you can read about here [ISO/IEC 15438:2006](https://www.iso.org/standard/43816.html) or download an older version of the PDF [this website](https://www.expresscorp.com/public/uploads/specifications/44/USS-PDF-417.pdf).

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install pdf417decoder.

```bash
pip install pdf417decoder
```

## Usage

```python
from PIL import Image as PIL
from pdf417decoder import PDF417Decoder

image = PIL.open("barcode.png")
decoder = PDF417Decoder(image)

if (decoder.decode() > 0):
    decoded = decoder.barcode_data_index_to_string(0)
```

## Testing Results

This library was tested using [pdf417gen](https://pypi.org/project/pdf417gen/) to create random barcodes and blurred with [OpenCV](https://pypi.org/project/opencv-python/) to test error correction. PyTest is used with several test images to show the libraries capability to decode barcodes in the following test cases.

* Binary data
* Multiple barcodes
* Upside down barcode
* Rotated barcode
* Error Corrections: Corrupted data due to blurred barcode
* Error Corrections: Missing data due marks concealing barcode
* Character type transitions (Upper, Lower, Mixed and Punctuation)

## Roadmap

- [x] Initial port of C# to Python
- [x] Create tests for functionality
- [x] Create fuzzy testing of decoder
- [x] Decode from PIL.Image
- [ ] Decode from Numpy Array
- [ ] Convert THRESH_OTSU image processing to use original algorithm written in C# or alternative
- [ ] Performance testing and optimizations

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[CPOL](https://www.codeproject.com/info/cpol10.aspx)

This project is a derivative of code licensed under the Code Project Open License (CPOL). The Code Project Open License (CPOL) is intended to provide developers who choose to share their code with a license that protects them and provides users of their code with a clear statement regarding how the code can be used.

## Credits

 Source code is a port of a C# Library created and maintained by [Uzi Granot](https://www.codeproject.com/script/Membership/View.aspx?mid=193217). [PDF417 Barcode Decoder .NET Class Library and Two Demo Apps](https://www.codeproject.com/Articles/4042463/PDF417-Barcode-Decoder-NET-Class-Library-and-Two-D)
