Compact ICC Profiles
====================

The ICC profiles in this collection contain the minimum tags necessary to correctly represent a color space and, in the case of ICC V2 profiles, use custom packing to minimize file size.  These profiles are intended for embedding in image files or software where the size of the profile is a consideration.

Profile description and copyright text are minimal.  All profiles in this collection are released to the public domain under the Creative Commons CC0 license.  They are free from restrictions on distribution and use to the extent allowed by law.

Details on the process used for creating these profiles can be found [here](https://photosauce.net/blog/post/making-a-minimal-srgb-icc-profile-part-1-trim-the-fat-abuse-the-spec)

Conventions
-----------

For color spaces that use a constant gamma value, profiles are provided in both ICC V2 and V4 versions (with the exception of HDR video color spaces, which are V4 only).  V2 profiles can be made smaller, and V2 has better software support, but V4 allows for a slight increase in the gamma precision.

For color spaces that have complex tone reproduction curves (TRCs), I have provided multiple options.  These color spaces are best represented using the newer V4 parametric curve type, so if you know the software reading the image is V4 compatible, those are the best choice.  For the V2 profiles, I have created two variants: `-micro` and `-magic`.

The `-micro` version of the profile uses a TRC that is balanced between accuracy and size and should be more than adequate for any 8-bit per channel images (e.g. JPEG).  For more accuracy, the `-magic` version of the profile uses a TRC with a larger number of points while still being significantly smaller than the standard profiles that use 1024 curve points.  These curves have been tuned so that in many cases they will give greater accuracy than the standard TRCs despite the smaller size, hence the name: magic.

Profiles in this Collection
---------------------------

### sRGB/scRGB

These profiles are defined using the true sRGB primaries, as defined in both the sRGB and scRGB standards, using the process defined in the [ICC's extension spec for sRGB profile makers](https://www.color.org/chardata/rgb/sRGB.pdf).  The values in these profiles differ very slightly from those in profiles derived from the Rec. 709 primaries, which are commonly given as sRGB.

In addition to the usual V2 variants, I have created a `-nano` version of the sRGB profile.  This was done partially as an exercise to determine the minimum size for a useable sRGB-compatible profile and partially because sRGB is a special case where an extra-small profile may be useful.

The scRGB color space uses the same primaries as sRGB but with a linear curve.  It defines an expanded gamut by means of encoding pixel values outside the normal range of [0-1].  It should be used only with images that are encoded in linear RGB with at least 16 bits per channel.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [sRGB-v2-nano.icc](profiles/sRGB-v2-nano.icc?raw=true)   | 410 bytes | nRGB | 20-Point Curve |
| [sRGB-v2-micro.icc](profiles/sRGB-v2-micro.icc?raw=true) | 456 bytes | uRGB | 42-Point Curve |
| [sRGB-v2-magic.icc](profiles/sRGB-v2-magic.icc?raw=true) | 736 bytes | sRGB | 182-Point Curve |
| [sRGB-v4.icc](profiles/sRGB-v4.icc?raw=true)             | 480 bytes | sRGB | Parametric Curve |
|  |  |  |  |
| [scRGB-v2.icc](profiles/scRGB-v2.icc?raw=true)           | 372 bytes | cRGB | Linear Curve |

---
### Greyscale

These are greyscale versions of the sRGB profiles, with the same TRC and white point.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [sGrey-v2-nano.icc](profiles/sGrey-v2-nano.icc?raw=true)   | 290 bytes | nGry | 20-Point Curve |
| [sGrey-v2-micro.icc](profiles/sGrey-v2-micro.icc?raw=true) | 336 bytes | uGry | 42-Point Curve |
| [sGrey-v2-magic.icc](profiles/sGrey-v2-magic.icc?raw=true) | 616 bytes | sGry | 182-Point Curve |
| [sGrey-v4.icc](profiles/sGrey-v4.icc?raw=true)             | 360 bytes | sGry | Parametric Curve |

---
### Display P3

The Display P3 color space is based on the [DCI-P3 D65](https://en.wikipedia.org/wiki/DCI-P3) color space but uses the sRGB transfer function rather than a constant gamma of 2.6.  This color space is [becoming](https://blog.conradchavez.com/2015/10/26/a-look-at-the-p3-color-gamut-of-the-imac-display-retina-late-2015/) [popular](https://developer.android.com/training/wide-color-gamut) as a display profile on newer wide-gamut displays.

Note: Apple has shipped at least two versions of their Display P3 profile.  The newer one, dated 2017, uses the sRGB TRC.  The older one, dated 2015, has slightly different values for the linear segment of the curve.  The profiles in this collection use the true sRGB curves as [documented by Apple](https://developer.apple.com/documentation/coregraphics/cgcolorspace/1408916-displayp3) and used by other vendors, such as Adobe.

**Warning**: The P3 color space requires a negative Z value for the red primary when adapted to the profile illuminant, which is not allowed according the ICC spec.  While some software will handle the negative value correctly, it may cause issues with software that adheres strictly to the ICC specs.

#### Max-Correctness

These profiles use the correct negative Z value for the profile-adapted red primary.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [DisplayP3-v2-micro.icc](profiles/DisplayP3-v2-micro.icc?raw=true) | 456 bytes | uP3 | 42-Point Curve |
| [DisplayP3-v2-magic.icc](profiles/DisplayP3-v2-magic.icc?raw=true) | 736 bytes | sP3 | 182-Point Curve |
| [DisplayP3-v4.icc](profiles/DisplayP3-v4.icc?raw=true)             | 480 bytes | sP3 | Parametric Curve |

#### Max-Compatibility

These profiles have the red Z value nudged up to 0, with adjustments made to the other colors and chromatic adaptation tags to compensate and restore balance.  Use these if you're not sure of software compatibility.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [DisplayP3Compat-v2-micro.icc](profiles/DisplayP3Compat-v2-micro.icc?raw=true) | 456 bytes | uP3C | 42-Point Curve |
| [DisplayP3Compat-v2-magic.icc](profiles/DisplayP3Compat-v2-magic.icc?raw=true) | 736 bytes | sP3C | 182-Point Curve |
| [DisplayP3Compat-v4.icc](profiles/DisplayP3Compat-v4.icc?raw=true)             | 480 bytes | sP3C | Parametric Curve |

#### DCI-P3

This profile defines a constant gamma of 2.6 and the P3 Theater whitepoint (x=0.314,y=0.351).  It is intended only for video use at high bit depths (HDR).

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [DCI-P3-v4.icc](profiles/DCI-P3-v4.icc?raw=true) | 464 bytes | TP3 | Gamma 2.6 |

---
### ProPhoto RGB (ROMM RGB)

[ProPhoto](https://en.wikipedia.org/wiki/ProPhoto_RGB_color_space) is an extremely wide gamut color space and should be used only for images encoded with at least 16 bits per channel.  The `-micro` curve for this color space is larger than others to ensure greater accuracy in these higher bit depth files.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [ProPhoto-v2-micro.icc](profiles/ProPhoto-v2-micro.icc?raw=true) | 496 bytes | uROM | 62-Point Curve |
| [ProPhoto-v2-magic.icc](profiles/ProPhoto-v2-magic.icc?raw=true) | 756 bytes | ROMM | 192-Point Curve |
| [ProPhoto-v4.icc](profiles/ProPhoto-v4.icc?raw=true)             | 480 bytes | ROMM | Parametric Curve |

---
### Rec. 601 (BT.601)

[Rec. 601](https://en.wikipedia.org/wiki/Rec._601) is a color space created for video but occasionally appears in image files.  Rec. 601 defines different color primaries for NTSC (525 line) and PAL (625 line) video formats.  Profiles are included for both color spaces.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [Rec601NTSC-v2-micro.icc](profiles/Rec601NTSC-v2-micro.icc?raw=true) | 460 bytes | u601 | 44-Point Curve |
| [Rec601NTSC-v2-magic.icc](profiles/Rec601NTSC-v2-magic.icc?raw=true) | 738 bytes | R601 | 183-Point Curve |
| [Rec601NTSC-v4.icc](profiles/Rec601NTSC-v4.icc?raw=true)             | 480 bytes | R601 | Parametric Curve |
|  |  |  |  |
| [Rec601PAL-v2-micro.icc](profiles/Rec601PAL-v2-micro.icc?raw=true) | 460 bytes | u60P | 44-Point Curve |
| [Rec601PAL-v2-magic.icc](profiles/Rec601PAL-v2-magic.icc?raw=true) | 738 bytes | R60P | 183-Point Curve |
| [Rec601PAL-v4.icc](profiles/Rec601PAL-v4.icc?raw=true)             | 480 bytes | R60P | Parametric Curve |

---
### Rec. 709 (BT.709)

[Rec. 709](https://en.wikipedia.org/wiki/Rec._709) is a color space created for video but occasionally appears in image files.  Note that although the color primaries are nearly identical to sRGB, Rec. 709 uses a different transfer curve, so these color spaces are not interchangeable.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [Rec709-v2-micro.icc](profiles/Rec709-v2-micro.icc?raw=true) | 460 bytes | u709 | 44-Point Curve |
| [Rec709-v2-magic.icc](profiles/Rec709-v2-magic.icc?raw=true) | 738 bytes | R709 | 183-Point Curve |
| [Rec709-v4.icc](profiles/Rec709-v4.icc?raw=true)             | 480 bytes | R709 | Parametric Curve |

---
### Rec. 2020

**Warning**: The [Rec. 2020](https://en.wikipedia.org/wiki/Rec._2020) color space requires a negative Z value for the red primary when adapted to the profile illuminant, which is not allowed according to the ICC spec.  While some software will handle the negative value correctly, it may cause issues with software that adheres strictly to the ICC specs.

#### Max-Correctness

These profiles use the correct negative Z value for the profile-adapted red primary.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [Rec2020-v2-micro.icc](profiles/Rec2020-v2-micro.icc?raw=true) | 460 bytes | u202 | 44-Point Curve |
| [Rec2020-v2-magic.icc](profiles/Rec2020-v2-magic.icc?raw=true) | 790 bytes | 2020 | 209-Point Curve |
| [Rec2020-v4.icc](profiles/Rec2020-v4.icc?raw=true)             | 480 bytes | 2020 | Parametric Curve |

#### Max-Compatibility

These profiles have the red Z value nudged up to 0, with adjustments made to the other colors and chromatic adaptation tags to compensate and restore balance.  Use these if you're not sure of software compatibility.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [Rec2020Compat-v2-micro.icc](profiles/Rec2020Compat-v2-micro.icc?raw=true) | 460 bytes | u20C | 44-Point Curve |
| [Rec2020Compat-v2-magic.icc](profiles/Rec2020Compat-v2-magic.icc?raw=true) | 790 bytes | 202C | 209-Point Curve |
| [Rec2020Compat-v4.icc](profiles/Rec2020Compat-v4.icc?raw=true)             | 480 bytes | 202C | Parametric Curve |

#### Gamma 2.4

This profile uses a constant gamma of 2.4 instead of the transfer function given by the standard, which matches that of Rec. 709.  The standard defines a gamma of 2.4 for the reference display device, so some applications use gamma 2.4 encoding to match.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [Rec2020-g24-v4.icc](profiles/Rec2020-g24-v4.icc?raw=true) | 464 bytes | 2024 | Gamma 2.4 |

---
### Adobe Compatible

These profiles are compact versions of commonly used Adobe-created color spaces.  Because these color spaces all use constant gamma values, the Adobe versions of the profiles are quite small.  However, with custom packing and abbreviated text tags, these profiles are almost 200 bytes smaller.  They are also free of the license restrictions that burden Adobe's versions of the profiles.

The primary colorants and whitepoint values in these profiles were adapted from the published x,y chromaticity coordinates and then tested for compatibility with the Adobe profiles.  Most of Adobe's ICC profiles are [well-behaved](https://ninedegreesbelow.com/photography/well-behaved-profile.html), but in cases where they are not, these compatible profiles have very slightly different primaries to bring them into balance.  No values deviate from those in the Adobe profiles by more than 1/2<sup>16</sup>.

The V4 profiles in this section encode the gamma value using the newer parametric curve tag, allowing for a slight increase in precision.  For example, the [Adobe RGB (1998) color space specification](https://www.adobe.com/digitalimag/pdfs/AdobeRGB1998.pdf) defines a gamma of precisely 2.19921875 (2+51/256), which is the nearest value to an ideal gamma of 2.2 that could be represented in a V2 profile.  V4 profiles allow encoding 2.2 gamma as 2.19999695 (2+13107/65536).  These profiles also include the slope limiting function recommended by Adobe (see Adobe RGB spec, Annex C) and implemented in the Adobe Color Engine.  The V4 profiles may give better conversion results when used with software that does not implement slope limiting internally.

| File Name | File Size | Description String | Color Space |
|--|--|--|--|
| [AdobeCompat-v2.icc](profiles/AdobeCompat-v2.icc?raw=true)           | 374 bytes | A98C | [Adobe RGB (1998)](https://en.wikipedia.org/wiki/Adobe_RGB_color_space) |
| [AdobeCompat-v4.icc](profiles/AdobeCompat-v4.icc?raw=true)           | 480 bytes | A98C |  |
|  |  |  |  |
| [AppleCompat-v2.icc](profiles/AppleCompat-v2.icc?raw=true)           | 374 bytes | APLC | [Apple RGB](http://www.brucelindbloom.com/WorkingSpaceInfo.html) |
| [AppleCompat-v4.icc](profiles/AppleCompat-v4.icc?raw=true)           | 480 bytes | APLC |  |
|  |  |  |  |
| [ColorMatchCompat-v2.icc](profiles/ColorMatchCompat-v2.icc?raw=true) | 374 bytes | ACMC | [ColorMatch RGB](http://www.brucelindbloom.com/WorkingSpaceInfo.html) |
| [ColorMatchCompat-v4.icc](profiles/ColorMatchCompat-v4.icc?raw=true) | 480 bytes | ACMC |  |
|  |  |  |  |
| [WideGamutCompat-v2.icc](profiles/WideGamutCompat-v2.icc?raw=true)   | 374 bytes | AWGC | [Wide Gamut RGB](https://en.wikipedia.org/wiki/Wide-gamut_RGB_color_space) |
| [WideGamutCompat-v4.icc](profiles/WideGamutCompat-v4.icc?raw=true)   | 480 bytes | AWGC |  |

---
### CMYK

Unlike RGB profiles, which need only define 3 primary colorant triplets and a single shared curve, CMYK profiles typically contain multiple complex transforms -- each of which consists of a 3x3 matrix, a set of distinct input curves per channel, an N-dimensional mapping table, and separate output curves per channel.  It is not uncommon for CMYK ICC profiles to be in the range of 500KB to 4MB, or more.

While the different structure of CMYK profiles makes it impossible to achieve the same small file sizes as we can for RGB profiles, it is possible to trim a CMYK profile down to the minimum required for a specific use.  Since the main purpose of the profiles in this collection is to enable correct display of images on a screen, I have included one such CMYK profile for that purpose.

This profile contains only the `A2B0` mapping tag, which defines a perceptual intent mapping from the source CMYK space.  The mapping is based on the [CGATS TR 001-1995](https://www.color.org/chardata/CGATS_TR_001.xalter) characterization data, with the gamut stretched to D50 white and black.  The primary purpose of this profile is to serve as a default for image viewing or conversion software to use when a CMYK image does not contain an embedded profile.  It cannot be used for conversion *to* CMYK or for other rendering intents.

The perceptual mapping is modeled on the appearance of Adobe's `U.S. Web Coated (SWOP) v2` profile, which is the long-time Photoshop default for North American users -- though it is not intended to be a direct replacement for the Adobe profile.  Due to the small size of the 4D LUT, this profile will not match the Adobe profile's output exactly, but it should give a correct overall appearance to an image when converted for display.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [CGATS001Compat-v2-micro.icc](profiles/CGATS001Compat-v2-micro.icc?raw=true) | 8464 bytes | uCMY | 48-Point Input Curves, 6-Point 4D LUT |
