## About The Project

This project can be your starting point of ACES workflow in Blender.

- [x] Default display mappings from Blender are retained. (e.g.,  standard sRGB, filmic, filmic log)
- [x] Default *Looks* are also retained.
- [x] ACES 1.3 ([Release note](https://community.acescentral.com/t/aces-1-3-now-available/3739))
- [x] Blender 3.1



## Getting Started

#### Method 1 - Overwrite color management folder

- Backup default color management folder.

  It depends on your installation location, for example:

  `C:\Program Files\Blender Foundation\Blender 3.1\3.1\datafiles\colormanagement`

- Copy these items into Blender's `colormanagement` folder.
  - `config.ocio`
  - `luts`
  - `filmic`
  - `aces_luts`
- Open Blender and check `Color Management` panel in `Render Properties`.

![color_management_aces_srgb](.\docs\images\color_management_aces_srgb.png)

- Done.



#### Method 2 - Start Blender from a batch file

Here is an Windows batch file example, assuming Blender-ACES-Config has been cloned into `D:\Blender-ACES-Config` and Blender has been installed at `C:\Program Files\Blender Foundation\Blender 3.1\`.

```
set OCIO=D:\Blender-ACES-Config\config.ocio

start "Blender (ACES workflow)" "C:\Program Files\Blender Foundation\Blender 3.1\blender.exe"
```

Copy the script to a text file, edit the paths according to your situation and save the text file with `.bat` extension. Then run Blender using the batch file.

The advantage of this method is that you can use Blender without ACES config by launching from desktop shortcuts or start menu as usual.



