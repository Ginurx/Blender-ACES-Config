# ACES Config for Blender



## About The Project

This project can be your starting point of ACES workflow in Blender.

- [x] Default display mappings from Blender are retained. (e.g.,  standard sRGB, filmic, filmic log)
- [x] Default *Looks* are also retained.
- [x] ACES 1.3 ([Release note](https://community.acescentral.com/t/aces-1-3-now-available/3739))
- [x] Blender 3.2



**IMPORTANT**

Some configurations you can find online also contains Blender default transforms. **But most of them are totally wrong.** 

Since scene linear in Blender's default config is Rec.709+Linear while scene linear in ACES is defined as ACEScg (AP1+Linear), simply copying & pasting won't work as you expect. Additional color transform is required. Otherwise,  the color would be slightly darker than it was supposed to be.



## Getting Started

#### Method 1 - Overwrite color management folder

- Backup default color management folder.

  It depends on your installation location, for example:

  `C:\Program Files\Blender Foundation\Blender 3.2\3.2\datafiles\colormanagement`

- Copy these items into Blender's `colormanagement` folder.
  - `config.ocio`
  - `luts`
  - `filmic`
  - `aces_luts`
- Open Blender and check `Color Management` panel in `Render Properties`.

<img src="./docs/images/color_management_aces_srgb.png" alt="color_management_aces_srgb" style="zoom:67%;" />

- Done.



#### Method 2 - Start Blender from a batch file

Here is an Windows batch file example, assuming Blender-ACES-Config has been cloned into `D:\Blender-ACES-Config` and Blender has been installed at `C:\Program Files\Blender Foundation\Blender 3.2\`.

```
set OCIO=D:\Blender-ACES-Config\config.ocio

start "Blender (ACES workflow)" "C:\Program Files\Blender Foundation\Blender 3.2\blender.exe"
```

Copy the script to a text file, edit the paths according to your situation and save the text file with `.bat` extension. Then run Blender using the batch file.

The advantage of this method is that you can use Blender without ACES config by launching from desktop shortcuts or the Start menu as usual.



#### Method 3 - Set environment variable

Blender uses the [OCIO](https://opencolorio.org/) standard environment variable - `OCIO` -  to read an OCIO configuration. So you can set the `OCIO` environment variable to the path of your configuration.

**But this is a highly discouraged method.** It can mess up other software which uses OCIO as color management backend. Blender should provide an alternative environment variable, for example `BLENDER_OCIO`???to avoid this problem.



## Showcase

*Left*: original filmic sRGB display transform (in which scene linear color space uses sRGB color primaries).

*Right*: ACES workflow filmic sRGB display transform (in which scene linear color space uses [AP1](https://en.wikipedia.org/wiki/Academy_Color_Encoding_System#ACEScg))

![the_cornell_box_rec709_filmic_vs_ap1_filmic](./docs/images/the_cornell_box_rec709_filmic_vs_ap1_filmic.png)

----

*Left*: standard sRGB display:

- Blender built-in workflow (in which scene linear uses sRGB color primaries)

*Right*: ACES sRGB display:

- ACES workflow (in which scene linear uses AP1 color primaries)
- sRGB display ([RRT](https://en.wikipedia.org/wiki/Academy_Color_Encoding_System#System_overview) + sRGB output)



![the_cornell_box_standard_srgb_vs_aces_srgb](./docs/images/the_cornell_box_standard_srgb_vs_aces_srgb.png)



## Customization

| Entry               | Comment                                                      |
| ------------------- | ------------------------------------------------------------ |
| `default_byte`      | Default color space for byte images such as JPEG, PNG, etc. <br>Since sRGB color space prevail, the default value had been set to `Utility - sRGB - Texture`.<br>Change this config entry to your most used source image color space. |
| `default_float`     | Default color space for HDR image such as EXR, HDR, etc.<br>The default value is `Utility - Linear - sRGB` which means a color space with sRGB primaries and linear encoding (without gamma). |
| `default_sequencer` | Default color space sequencer is working in.<br>Alpha blending can be quite different with different color space.<br>Pick a color space of which the color primaries either be ACES AP1 or the one in which your contents are to be delivered.<br>This option can be changed in Blender's color management panel per project. |
| `color_picking`     | This is the most tricky part of the configuration. The RGB color numbers you see in color picker panel are always in scene linear space which is ACEScg in ACES workflow.<br>But a wide gamut color space can't be displayed on a typical sRGB monitor.<br>In order to pick a color by our eyes, a transform had to be introduced, i.e. the `color_picking` role. <br>Typically, this shall match your output transform such as `Output - sRGB`, `Output - P3D65`. <br>The default value is `Utility - sRGB - Texture` which is a "standard" sRGB transform without ACES RRT. This will give you traditional look.<br>Remember, in Blender, the RGB color numbers in color picker are always in scene linear color space. It can be different with what you see. Maybe blender should provide a way to pick color in user specified color space. |

You should leave the other entries intact.



## Related Projects

[ACES v1.3 config and LUTs](https://github.com/Ginurx/OpenColorIO-Configs)

[Blender](https://www.blender.org/)

[OpenColorIO](https://opencolorio.org/)

[ACES](https://acescentral.com/)
