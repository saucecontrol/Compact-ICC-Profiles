Compact ICC Profiles
====================

The ICC profiles in this collection contain the minimum tags necessary to correctly represent a color space and, in the case of ICC V2 profiles, use custom packing to mimimize file size.  These profiles are intended for embedding in image files where the size of the profile is a consideration.

Profile description and copyright text are minimal.  All profiles in this collection are released to the public domain under the Creative Commons CC0 license.  They are free from restrictions on distribution and use to the extent allowed by law.

Details on the process used for creating these profiles can be found [here](https://photosauce.net/blog/post/making-a-minimal-srgb-icc-profile-part-1-trim-the-fat-abuse-the-spec)

Conventions
-----------

For color spaces that use a constant gamma value, only a single ICC V2 profile is provided.  V4 profiles offer no accuracy advantage in this case, V2 profiles can be made smaller, and V2 has better software support.

For color spaces that have complex tone reproduction curves (TRCs), I have provided multiple options.  These color spaces are best represented using the newer V4 parametric curve type, so if you know the software reading the image is V4 compatible, those are the best choice.  For the V2 profiles, I have created two variants: `-micro` and `-magic`.  The `-micro` version of the profile uses a TRC that is balanced between accuracy and size and should be more than adequate for any 8-bit per channel images (e.g. JPEG).  For more accuracy, the `-magic` version of the profile uses a TRC with a larger number of points while still being significantly smaller than the standard profiles that use 1024 curve points.  These curves have been tuned so that in many cases they will give greater accuracy than the standard TRCs despite the smaller size, hence the name: magic.

Profiles in this Collection
---------------------------

### sRGB/scRGB

These profiles are defined using the true sRGB primaries, as defined in both the sRGB and scRGB standards, using the process defined in the [ICC's extension spec for sRGB profile makers](http://www.color.org/chardata/rgb/sRGB.pdf).  The values in these profiles differ very slightly from those in profiles derived from the Rec. 709 primaries, which are commonly given as sRGB.

In addition to the usual V2 variants, I have created a `-nano` version of the sRGB profile.  This was done partially as an exercise to determine the minimum size for a useable sRGB-compatible profile and partially because sRGB is a special case where an extra-small profile may be useful.

The scRGB color space uses the same primaries as sRGB but with a linear curve.  It defines an expanded gamut by means of encoding pixel values outside the normal range of [0-1].

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [sRGB-v2-nano.icc](profiles/sRGB-v2-nano.icc?raw=true)   | 410 bytes | nRGB | 20-Point Curve |
| [sRGB-v2-micro.icc](profiles/sRGB-v2-micro.icc?raw=true) | 456 bytes | uRGB | 42-Point Curve |
| [sRGB-v2-magic.icc](profiles/sRGB-v2-magic.icc?raw=true) | 736 bytes | sRGB | 182-Point Curve |
| [sRGB-v4.icc](profiles/sRGB-v4.icc?raw=true)             | 480 bytes | sRGB | Parametric Curve |
|||||
| [scRGB-v2.icc](profiles/scRGB-v2.icc?raw=true)           | 372 bytes | cRGB | Linear Curve |

### Greyscale

These are greyscale versions of the sRGB profiles, with the same TRCs and white point.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [sGrey-v2-nano.icc](profiles/sGrey-v2-nano.icc?raw=true)   | 290 bytes | nGry | 20-Point Curve |
| [sGrey-v2-micro.icc](profiles/sGrey-v2-micro.icc?raw=true) | 336 bytes | uGry | 42-Point Curve |
| [sGrey-v2-magic.icc](profiles/sGrey-v2-magic.icc?raw=true) | 616 bytes | sGry | 182-Point Curve |
| [sGrey-v4.icc](profiles/sGrey-v4.icc?raw=true)             | 360 bytes | sGry | Parametric Curve |

### Display P3

The Display P3 color space is based on the [DCI-P3 D65](https://en.wikipedia.org/wiki/DCI-P3) color space but uses an sRGB TRC rather than the standard constant gamma of 2.6.  This color space is [becoming](https://blog.conradchavez.com/2015/10/26/a-look-at-the-p3-color-gamut-of-the-imac-display-retina-late-2015/) [popular](https://www.anandtech.com/show/10265/understanding-the-97-ipad-pros-true-tone-display) as a display profile on newer wide-gamut displays.

Note: The P3 color space requires a negative Z value for the red primary when adapted to the profile illuminant, which is not allowed according the the ICC spec.  While some software will handle the negative value correctly, it may cause issues with software that adheres strictly to the ICC specs, including popular web browsers.  Chrome and Firefox [recently relaxed those restrictions](https://bugzilla.mozilla.org/show_bug.cgi?format=default&id=1250461), but *only on Apple platforms*.

#### Max-Compatibility

These profiles have the red Z value nudged up to 0, with adjustments made to the other colors to compensate and restore balance.  Use these if you're not sure of compatibility or if you are displaying the images in a web browser.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [DisplayP3Compat-v2-micro.icc](profiles/DisplayP3Compat-v2-micro.icc?raw=true) | 456 bytes | uP3C | 42-Point Curve |
| [DisplayP3Compat-v2-magic.icc](profiles/DisplayP3Compat-v2-magic.icc?raw=true) | 736 bytes | sP3C | 182-Point Curve |
| [DisplayP3Compat-v4.icc](profiles/DisplayP3Compat-v4.icc?raw=true)             | 480 bytes | sP3C | Parametric Curve |

#### Max-Correctness

These profiles use the correct negative Z value for the profile-adapted red primary.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [DisplayP3-v2-micro.icc](profiles/DisplayP3-v2-micro.icc?raw=true) | 456 bytes | uP3 | 42-Point Curve |
| [DisplayP3-v2-magic.icc](profiles/DisplayP3-v2-magic.icc?raw=true) | 736 bytes | sP3 | 182-Point Curve |
| [DisplayP3-v4.icc](profiles/DisplayP3-v4.icc?raw=true)             | 480 bytes | sP3 | Parametric Curve |

### ProPhoto RGB (ROMM RGB)

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [ProPhoto-v2-micro.icc](profiles/ProPhoto-v2-micro.icc?raw=true) | 496 bytes | uROM | 62-Point Curve |
| [ProPhoto-v2-magic.icc](profiles/ProPhoto-v2-magic.icc?raw=true) | 756 bytes | ROMM | 192-Point Curve |
| [ProPhoto-v4.icc](profiles/ProPhoto-v4.icc?raw=true)             | 480 bytes | ROMM | Parametric Curve |

### Rec. 709

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [Rec709-v2-micro.icc](profiles/Rec709-v2-micro.icc?raw=true) | 460 bytes | u709 | 44-Point Curve |
| [Rec709-v2-magic.icc](profiles/Rec709-v2-magic.icc?raw=true) | 738 bytes | R709 | 183-Point Curve |
| [Rec709-v4.icc](profiles/Rec709-v4.icc?raw=true)             | 480 bytes | R709 | Parametric Curve |

### Rec. 2020

Note: The [Rec. 2020](https://en.wikipedia.org/wiki/Rec._2020) color space requires a negative Z value for the red primary when adapted to the profile illuminant, which is not allowed according to the ICC spec.  While some software will handle the negative value correctly, it may cause issues with software that adheres strictly to the ICC specs, including popular web browsers.  Chrome and Firefox [recently relaxed those restrictions](https://bugzilla.mozilla.org/show_bug.cgi?format=default&id=1250461), but *only on Apple platforms*.

#### Max-Compatibility

These profiles have the red Z value nudged up to 0, with adjustments made to the other colors to compensate and restore balance.  Use these if you're not sure of compatibility or if you are displaying the images in a web browser.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [Rec2020Compat-v2-micro.icc](profiles/Rec2020Compat-v2-micro.icc?raw=true) | 460 bytes | u20C | 44-Point Curve |
| [Rec2020Compat-v2-magic.icc](profiles/Rec2020Compat-v2-magic.icc?raw=true) | 790 bytes | 202C | 209-Point Curve |
| [Rec2020Compat-v4.icc](profiles/Rec2020Compat-v4.icc?raw=true)             | 480 bytes | 202C | Parametric Curve |

#### Max-Correctness

These profiles use the correct negative Z value for the profile-adapted red primary.

| File Name | File Size | Description String | Notes |
|--|--|--|--|
| [Rec2020-v2-micro.icc](profiles/Rec2020-v2-micro.icc?raw=true) | 460 bytes | u202 | 44-Point Curve |
| [Rec2020-v2-magic.icc](profiles/Rec2020-v2-magic.icc?raw=true) | 790 bytes | 2020 | 209-Point Curve |
| [Rec2020-v4.icc](profiles/Rec2020-v4.icc?raw=true)             | 480 bytes | 2020 | Parametric Curve |

### Adobe Compatible

These profiles are compact versions of commonly used Adobe-created color spaces.  Because these color spaces all use constant gamma values, the Adobe versions of the profiles are quite small.  However, with custom packing and abbreviated text tags, these profiles are almost 200 bytes smaller.  They are also free of the license restrictions that burden Adobe's versions of the profiles.

The primary colorants and whitepoint values in these profiles were adapted from the published x,y chromaticity coordinates and then tested for compatibility with the Adobe profiles.  Most of Adobe's ICC profiles are [well-behaved](https://ninedegreesbelow.com/photography/well-behaved-profile.html), but in cases where they are not, these compatible profiles have very slightly different primaries to bring them into balance.  No values deviate from those in the Adobe profiles by more than 1/2^16^.

| File Name | File Size | Description String | Color Space |
|--|--|--|--|
| [AdobeCompat-v2.icc](profiles/AdobeCompat-v2.icc?raw=true)           | 374 bytes | A98C | [Adobe RGB (1998)](https://en.wikipedia.org/wiki/Adobe_RGB_color_space) |
| [AppleCompat-v2.icc](profiles/AppleCompat-v2.icc?raw=true)           | 374 bytes | APLC | [Apple RGB](http://www.brucelindbloom.com/WorkingSpaceInfo.html) |
| [ColorMatchCompat-v2.icc](profiles/ColorMatchCompat-v2.icc?raw=true) | 374 bytes | ACMC | [ColorMatch RGB](http://www.brucelindbloom.com/WorkingSpaceInfo.html) |
| [WideGamutCompat-v2.icc](profiles/WideGamutCompat-v2.icc?raw=true)   | 374 bytes | AWGC | [Wide Gamut RGB](https://en.wikipedia.org/wiki/Wide-gamut_RGB_color_space) |
