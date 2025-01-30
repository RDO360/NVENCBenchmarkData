# NVENC Benchmark Data

This repository contains the data produced during our NVENC benchmark.

To reproduce the following results, first [install, run and learn about the use of our benchmarking tools](https://github.com/RDO360/PerformanceBenchmarks).

If you use any part of this dataset, please [cite our work](#citation).

## 360° videos

The video material used in our benchmark consists of the following 360° videos that we filmed using an [Insta Pro 2 camera](https://www.insta360.com/product/insta360-pro2).

| Name      | Duration (s) | Download Links |
|:----------|:------------:|:-----|
| Fireplace | 227          | [Unstitched](TODO) <br> [Stitched Monoscopic (2D)](TODO) <br> [Stitched Stereoscopic (3D)](TODO) |
| Suburb    | 245          | [Unstitched](TODO) <br> [Stitched Monoscopic (2D)](TODO) <br> [Stitched Stereoscopic (3D)](TODO) |

For the benchmark, we stitched the 360° videos in equirectangular projection using the [Insta360 Stitcher 3.1.3 software](https://www.mantis-sub.com/support/) and the following parameters.

| Parameter                   | Value                            |
|:----------------------------|:--------------------------------:|
| Content Type                | Monoscopic                       |
| Stitching Mode              | New Optical Flow                 |
| Sampling Type               | Fast                             |
| Blender Type                | Cuda                             |
| Opticalflow stitching range | 20                               |
| Template stitching range    | 0.5                              |
| Use Original Offset         | Enabled                          |
| Smooth Stitch               | Enabled                          |
| Flowstate Stabilization     | Disabled                         |
| Use Hardware Decoding       | 8                                |
| Use Hardware Encoding       | Enabled                          |
| Use nadir logo              | Disabled                         |
| Resolution                  | 8K (7680 $\times$ 3840 pixels) |
| Output Format               | MP4                              |
| Codec Type                  | H265 codec                       |
| Bitrate                     | 144 Mibps*                       |
| Frame Rate                  | 29.97                            |
| Audio Type                  | None                             |

\* Even though Insta360 Stitcher shows the bitrate in Mbps, Mibps are used during encoding.
A bitrate of 144 Mibps is approximately 151 Mbps.

## Tiles

The 360° videos were cut into 6 by 6 tiles (from left to right, then top to bottom) using the following FFmpeg command.

```bash
ffmpeg -y -hide_banner -i video.mp4 -vf "crop=1280:640:0:0" -pix_fmt yuv420p tile1.y4m -vf "crop=1280:640:1280:0" -pix_fmt yuv420p tile2.y4m -vf "crop=1280:640:2560:0" -pix_fmt yuv420p tile3.y4m -vf "crop=1280:640:3840:0" -pix_fmt yuv420p tile4.y4m -vf "crop=1280:640:5120:0" -pix_fmt yuv420p tile5.y4m -vf "crop=1280:640:6400:0" -pix_fmt yuv420p tile6.y4m -vf "crop=1280:640:0:640" -pix_fmt yuv420p tile7.y4m -vf "crop=1280:640:1280:640" -pix_fmt yuv420p tile8.y4m -vf "crop=1280:640:2560:640" -pix_fmt yuv420p tile9.y4m -vf "crop=1280:640:3840:640" -pix_fmt yuv420p tile10.y4m -vf "crop=1280:640:5120:640" -pix_fmt yuv420p tile11.y4m -vf "crop=1280:640:6400:640" -pix_fmt yuv420p tile12.y4m -vf "crop=1280:640:0:1280" -pix_fmt yuv420p tile13.y4m -vf "crop=1280:640:1280:1280" -pix_fmt yuv420p tile14.y4m -vf "crop=1280:640:2560:1280" -pix_fmt yuv420p tile15.y4m -vf "crop=1280:640:3840:1280" -pix_fmt yuv420p tile16.y4m -vf "crop=1280:640:5120:1280" -pix_fmt yuv420p tile17.y4m -vf "crop=1280:640:6400:1280" -pix_fmt yuv420p tile18.y4m -vf "crop=1280:640:0:1920" -pix_fmt yuv420p tile19.y4m -vf "crop=1280:640:1280:1920" -pix_fmt yuv420p tile20.y4m -vf "crop=1280:640:2560:1920" -pix_fmt yuv420p tile21.y4m -vf "crop=1280:640:3840:1920" -pix_fmt yuv420p tile22.y4m -vf "crop=1280:640:5120:1920" -pix_fmt yuv420p tile23.y4m -vf "crop=1280:640:6400:1920" -pix_fmt yuv420p tile24.y4m -vf "crop=1280:640:0:2560" -pix_fmt yuv420p tile25.y4m -vf "crop=1280:640:1280:2560" -pix_fmt yuv420p tile26.y4m -vf "crop=1280:640:2560:2560" -pix_fmt yuv420p tile27.y4m -vf "crop=1280:640:3840:2560" -pix_fmt yuv420p tile28.y4m -vf "crop=1280:640:5120:2560" -pix_fmt yuv420p tile29.y4m -vf "crop=1280:640:6400:2560" -pix_fmt yuv420p tile30.y4m -vf "crop=1280:640:0:3200" -pix_fmt yuv420p tile31.y4m -vf "crop=1280:640:1280:3200" -pix_fmt yuv420p tile32.y4m -vf "crop=1280:640:2560:3200" -pix_fmt yuv420p tile33.y4m -vf "crop=1280:640:3840:3200" -pix_fmt yuv420p tile34.y4m -vf "crop=1280:640:5120:3200" -pix_fmt yuv420p tile35.y4m -vf "crop=1280:640:6400:3200" -pix_fmt yuv420p tile36.y4m
```

## Spatial and Temporal Information

We evaluated the spatial information (SI) and temporal information (TI) of the tiles using the following command.

```powershell
siTi.ps1 -tiles "tile1.y4m", "tile2.y4m", "tile3.y4m", "tile4.y4m", "tile5.y4m", "tile6.y4m", "tile7.y4m", "tile8.y4m", "tile9.y4m", "tile10.y4m", "tile11.y4m", "tile12.y4m", "tile13.y4m", "tile14.y4m", "tile15.y4m", "tile16.y4m", "tile17.y4m", "tile18.y4m", "tile19.y4m", "tile20.y4m", "tile21.y4m", "tile22.y4m", "tile23.y4m", "tile24.y4m", "tile25.y4m", "tile26.y4m", "tile27.y4m", "tile28.y4m", "tile29.y4m", "tile30.y4m", "tile31.y4m", "tile32.y4m", "tile33.y4m", "tile34.y4m", "tile35.y4m", "tile36.y4m" -resultsFile siti_tiles.csv
```

The result files for `Fireplace` (`siTiFireplace.csv`) and `Suburb` (`siTiSuburb.csv`) are available in this repository.
The files follow this format.

| Column Name | Description                            |
|:------------|:---------------------------------------|
| input_file  | The file name of the tile.             |
| n           | The index of the frame (starts at 1).  |
| si          | The spatial information of the frame.  |
| ti          | The temporal information of the frame. |

## Bitrate and Visual Quality Benchmark

We evaluate the bitrate and visual quality of the tiles' segments according to their encoding parameters using the following command.

```powershell
bitrateVmafBenchmark.ps1 -tiles "suburb5.y4m", "suburb13.y4m", "suburb19.y4m", "fireplace3.y4m", "fireplace5.y4m", "fireplace19.y4m", "fireplace33.y4m" -codecs "hevc_nvenc", "h264_nvenc" -presets p1, p2, p3, p4, p5, p6, p7 -qps 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40 -heights 0, 320 -segmentTime 2 -segmentGOP 60 -segmentDirectory ".\segments" -dataFile fireplaceSuburbBitrateVmaf.csv -vmafLogDirectory "vmafLogs"
```

The results file for both `Fireplace` and `Suburb` (`fireplaceSuburbBitrateVmaf.csv`) is available in this repository.
The file follows this format.

Download the [VMAF results files](TODO).

| Column Name | Description                                                                                                                      |
|:------------|:---------------------------------------------------------------------------------------------------------------------------------|
| tile        | The file name of the tile.                                                                                                       |
| codec       | The codec used to encode the segment.                                                                                            |
| preset      | The preset used to encode the segment.                                                                                           |
| qp          | The quantization parameters to encode the segment.                                                                               |
| height      | The segment's height in pixels. A value of zero means that the height is unchanged.                                              |
| bitrate     | The number of bits in the encoded segment.                                                                                       |
| vmafMean    | The mean VMAF of the encoded segment.                                                                                            |
| vmafLogFile | The name of the VMAF results file for this segment, which includes all supported metrics, such as PSNR and SSIM, for each frame. |

## Encoding Speed Benchmark

We evaluate the time to encode all the segments of the tiles according to their encoding parameters using the following command.

```powershell
encodingSpeedBenchmark.ps1 -tiles "suburb5.y4m", "suburb13.y4m", "suburb19.y4m", "fireplace3.y4m", "fireplace5.y4m", "fireplace19.y4m", "fireplace33.y4m" -codecs "hevc_nvenc", "h264_nvenc" -presets p1, p2, p3, p4, p5, p6, p7 -qps 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40 -heights 0, 320 -repetitions 5 -segmentTime 2 -segmentGOP 60 -segmentDirectory ".\segments" -dataFile fireplaceSuburbSpeed.csv
```

The results file for both `Fireplace` and `Suburb` (`fireplaceSuburbSpeed.csv`) is available in this repository.
The file follows this format.

| Column Name | Description                                                                         |
|:------------|:------------------------------------------------------------------------------------|
| tile        | The file name of the tile.                                                          |
| codec       | The codec used to encode the segments.                                              |
| preset      | The preset used to encode the segments.                                             |
| qp          | The quantization parameters to encode the segments.                                 |
| height      | The segments' height in pixels. A value of zero means that the height is unchanged. |
| time        | The required time, in seconds, to encode all the segments of the tile.              |

## Ethics

We have obtained the consent of the recognizable people in the videos to publish the data.
Follow these rules when using the videos.

- Don't use the videos in illegal, immoral, offensive, misleading or deceptive content.
- Don't sell or redistribute the videos on other platforms.
- Don't use the videos in your trade-mark, design-mark, trade-name, business name or service mark.
- Videos containing recognizable trademarks, logos or brands cannot be used for commercial purposes.
- Don't imply that any recognizable person or brand in the videos endorses your content or product.

## Citation

**[Redacted]**