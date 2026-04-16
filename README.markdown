Browse : [AWK](https://github.com/michel-leonard/ciede2000-awk) · [BC](https://github.com/michel-leonard/ciede2000-basic-calculator) · [C#](https://github.com/michel-leonard/ciede2000-csharp) · [C++](https://github.com/michel-leonard/ciede2000-cpp) · [C99](https://github.com/michel-leonard/ciede2000-c) · **Dart** · [Go](https://github.com/michel-leonard/ciede2000-go) · [JavaScript](https://github.com/michel-leonard/ciede2000-javascript) · [Java](https://github.com/michel-leonard/ciede2000-java) · [Julia](https://github.com/michel-leonard/ciede2000-julia) · [Kotlin](https://github.com/michel-leonard/ciede2000-kotlin)

# CIEDE2000 color difference formula in Dart

This page presents the CIEDE2000 color difference, implemented in the Dart programming language.

![Logo for CIEDE2000 in Dart/Flutter](https://raw.githubusercontent.com/michel-leonard/ciede2000-color-matching/refs/heads/main/docs/assets/images/logo.jpg)

## About

Here you’ll find the first rigorously correct implementation of CIEDE2000 that doesn’t use any conversion between degrees and radians. Set parameter `canonical` to obtain results in line with your existing pipeline.

`canonical`|The algorithm operates...|
|:--:|-|
`false`|in accordance with the CIEDE2000 values currently used by many industry players|
`true`|in accordance with the CIEDE2000 values provided by [this](https://hajim.rochester.edu/ece/sites/gsharma/ciede2000/) academic MATLAB function|

## Our CIEDE2000 offer

This production-ready file, released in 2026, contain the CIEDE2000 algorithm.

Source File|Type|Bits|Purpose|Advantage|
|:--:|:--:|:--:|:--:|:--:|
[ciede2000.dart](./ciede2000.dart)|`double`|64|General|Interoperability|

### Software Versions

- Dart 3.11.5

### Example Usage

We calculate the CIEDE2000 distance between two colors, first without and then with parametric factors.

```dart
void main() {
	// Example of two L*a*b* colors
	final double l1 = 76.8, a1 = 103.9, b1 = 6.6;
	final double l2 = 73.6, a2 = 116.1, b2 = -3.9;

	double delta_e = ciede2000(l1, a1, b1, l2, a2, b2);
	print('CIEDE2000 = ${delta_e}'); // ΔE2000 = 4.575648907164364

	// Example of parametric factors used in the textile industry
	final double kl = 2.0, kc = 1.0, kh = 1.0;

	// Perform a CIEDE2000 calculation compliant with that of Gaurav Sharma
	final bool canonical = true;

	delta_e = ciede2000(l1, a1, b1, l2, a2, b2, kl, kc, kh, canonical);
	print('CIEDE2000 = ${delta_e}'); // ΔE2000 = 4.1058032084100855
}
```

### Test Results

LEONARD’s tests are based on well-chosen L\*a\*b\* colors, with various parametric factors `kL`, `kC` and `kH`.

```
 CIEDE2000 Verification Summary :
          Compliance : [ ] CANONICAL [X] SIMPLIFIED
  First Checked Line : 60.0,-0.0,32.0,68.0,0.00008,-127.9995,1.0,1.0,1.0,54.15960745600092
           Precision : 11 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 227.48 seconds
     Average Delta E : 67.12
   Average Deviation : 4.2e-15
   Maximum Deviation : 1.7e-13
```

```
CIEDE2000 Verification Summary :
          Compliance : [X] CANONICAL [ ] SIMPLIFIED
  First Checked Line : 60.0,-0.0,32.0,68.0,0.00008,-127.9995,1.0,1.0,1.0,54.15941680953167
           Precision : 11 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 223.21 seconds
     Average Delta E : 67.12
   Average Deviation : 4.7e-15
   Maximum Deviation : 1.7e-13
```

## Public Domain Licence

You are free to use these files, even for commercial purposes.
