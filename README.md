# HDCP Key Generator

A Python tool for generating HDCP (High-bandwidth Digital Content Protection) source and sink keys.

## Original Author

Rich Wareham <richwareham@gmail.com> (2010)

## Python 3.13+ Compatibility Update

This repository contains an updated version of the original HDCP key generator script, modified to work with Python 3.13 and above.

**Update by:** MakinoSeiran (https://github.com/MakinoSeiran)

### What's Changed

- Removed deprecated `string` module usage
- Replaced `string.split()` with modern `str.split()` method
- Replaced `string.join()` with `str.join()` method
- Fixed all string operations for Python 3.13+ compatibility
- Maintained full backward compatibility with original functionality

###How It Works
HDCP uses a master key matrix to generate unique device keys:

Source Key Generation: Selects 20 rows from the master matrix based on the KSV's 1-bits, then adds them together

Sink Key Generation: Same process but uses the transposed master matrix

KSV (Key Selection Vector): A 40-bit number with exactly 20 ones and 20 zeros

The shared secret between source and sink is computed by adding selected key components based on the partner's KSV.

## Prerequisites

- Python 3.13 or higher
- A valid `master-key.txt` file (not included)

##Usage: generate_key.py [options]

Options:
  -h, --help            show this help message and exit
  -m FILE, --master=FILE
                        load master key from FILE
  -k, --sink            generate a sink key rather than a source key
  --ksv=KSV             use a specific KSV expressed in hexadecimal
  -j, --json            output key and KSV as JSON
  -t, --test            generate source and sink keys and test they work
```

##Examples:

```bash
# Generate a sink key with KSV 0x54f0af39a8 and output the result in JSON
./generate_key.py -k --ksv 54f0af39a8 -j

# Generate a source key with a random KSV and output the result in a 
# human-readable form
./generate_key.py

# Run a self-test to make sure the source a sink key generation is consistent
./generate_key.py -t
```

