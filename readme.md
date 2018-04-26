Compact ICC Profiles
====================

These ICC profiles contain the minimum tags necessary to correctly represent a color space and, in the case of ICC V2 profiles, custom packing to mimimize file size.  These profiles are intended for embedding in images where the size of the profile is a consideration.

Profile description and copyright text are minimal.  All profiles in this collection are licensed under the Creative Commons CC0 license.  They are free from restrictions on distribution and use to the extent allowed by law.

Details on the process used for creating these profiles can be found here:
https://photosauce.net/blog/post/making-a-minimal-srgb-icc-profile-part-1-trim-the-fat-abuse-the-spec

More profiles will be added as I have time to evaluate them.

Files in this Collection
------------------------

| File Name | File Size | Color Space | Spec Version | Notes |
|--|--|--|--|--|
| ProPhoto-v4.icc   | 480 bytes | ProPhoto (ROMM) | 4.3 | Parametric Curve |
| sRGB-v2-nano.icc  | 410 bytes | sRGB | 2.1 | 20-Point Curve -- Smallest usable sRGB-compatible profile |
| sRGB-v2-micro.icc | 456 bytes | sRGB | 2.1 | 42-Point Curve -- Good balance of size and accuracy |
| sRGB-v2-magic.icc | 796 bytes | sRGB | 2.1 | 212-Point Curve -- Better accuracy than standard 1024-point curve in most cases |
| sRGB-v4.icc       | 480 bytes | sRGB | 4.3 | Parametric Curve |
