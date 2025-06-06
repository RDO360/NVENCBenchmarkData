# NVENC Benchmark Data

This repository contains the data produced during our NVENC benchmark for the paper *Benchmarking Hardware Encoding for Live 360° Video Tiled Streaming*.

To reproduce our results, first [install, run and learn about the use of our benchmarking tools](https://github.com/RDO360/PerformanceBenchmarks).

If you use any part of this dataset, please [cite our work](#citation) and observe our [ethics code](#ethics).

## 360° videos

The video material used in our benchmark consists of the following 360° videos that we filmed using an [Insta Pro 2 camera](https://www.insta360.com/product/insta360-pro2).

| Name           | Duration (s) | Download Links |
|:---------------|:------------:|:-----|
| Fireplace      | 227          | [Unstitched](https://drive.google.com/drive/folders/1frlmlmifdCWKG49qPODrS5D0DePwRN9b?usp=sharing) <br> [Stitched Monoscopic (2D)](https://mega.nz/file/KH5DQLDS#l2zXviW31GlZjJiaYlelKCDgU722iI4_w6SZA8C-M8g) <br> [Stitched Stereo (3D)](https://mega.nz/file/qCA3nA4S#_X_2Cox9nLeK79boyZOz8TlXpCbBBdGJRikODagC3ZA) |
| Suburb         | 245          | [Unstitched](https://drive.google.com/drive/folders/1Kzkjj760CbdvMjUtqj-3w0OEdigf9511?usp=sharing) <br> [Stitched Monoscopic (2D)](https://drive.google.com/file/d/1sqyIkJpC4A5vrl9T0_--A5txX_zkNCc7/view?usp=sharing) <br> [Stitched Stereo (3D)](https://mega.nz/file/CaAlxTYI#lJj40dXpZdxIIw1K9A7_roIjG90HfzTz2vVP_Z3FSuc) |
| VirtualReality | 253          | [Unstitched](https://drive.google.com/drive/folders/1HiJw3-ik9uMjILK7pkP7xLR5bXM1djKH?usp=sharing) <br> [Stitched Monoscopic (2D)](https://drive.google.com/file/d/1Os0p9dXafcvzEM4S_s4JxNQPExLcAEGm/view?usp=sharing) <br> [Stitched Stereo (3D)](https://mega.nz/file/OWB1wIBY#5hRt-kmMrxzCopxQT2qF9fSqs97Cb-IpDYDbeQXqVw4) |

We stitched the 360° videos in equirectangular projection using the [Insta360 Stitcher 3.1.3 software](https://www.mantis-sub.com/support/) and the following parameters.

| Parameter                   | Value                                            |
|:----------------------------|:------------------------------------------------:|
| Content Type                | Monoscopic <br> Stereo (Left Eye on Top)         |
| Stitching Mode              | New Optical Flow                                 |
| Sampling Type               | Fast                                             |
| Blender Type                | Cuda                                             |
| Opticalflow stitching range | 20 (Monoscopic) <br> 16 (Stereo)                 |
| Template stitching range    | 0.5                                              |
| Use Original Offset         | Enabled                                          |
| Smooth Stitch               | Enabled                                          |
| Flowstate Stabilization     | Disabled                                         |
| Use Hardware Decoding       | 8                                                |
| Use Hardware Encoding       | Enabled                                          |
| Use nadir logo              | Disabled                                         |
| Resolution                  | 8K (7680 $\times$ 3840 pixels)                   |
| Output Format               | MP4                                              |
| Codec Type                  | H265 codec                                       |
| Bitrate                     | 144 Mibps* (Monoscopic) <br> 288 Mibps* (Stereo) |
| Frame Rate                  | 29.97                                            |
| Audio Type                  | Spatial                                          |

\* Even though Insta360 Stitcher shows the bitrate in Mbps, Mibps are used during encoding.
A bitrate of 144 Mibps is approximately 151 Mbps and 288 Mibps is approximately 302 Mbps.

## Tiles

The 360° videos were cut into 6 by 6 tiles (from left to right, then top to bottom) using the following FFmpeg command.

```bash
ffmpeg -y -hide_banner -i video.mp4 -vf "crop=1280:640:0:0" -pix_fmt yuv420p tile1.y4m -vf "crop=1280:640:1280:0" -pix_fmt yuv420p tile2.y4m -vf "crop=1280:640:2560:0" -pix_fmt yuv420p tile3.y4m -vf "crop=1280:640:3840:0" -pix_fmt yuv420p tile4.y4m -vf "crop=1280:640:5120:0" -pix_fmt yuv420p tile5.y4m -vf "crop=1280:640:6400:0" -pix_fmt yuv420p tile6.y4m -vf "crop=1280:640:0:640" -pix_fmt yuv420p tile7.y4m -vf "crop=1280:640:1280:640" -pix_fmt yuv420p tile8.y4m -vf "crop=1280:640:2560:640" -pix_fmt yuv420p tile9.y4m -vf "crop=1280:640:3840:640" -pix_fmt yuv420p tile10.y4m -vf "crop=1280:640:5120:640" -pix_fmt yuv420p tile11.y4m -vf "crop=1280:640:6400:640" -pix_fmt yuv420p tile12.y4m -vf "crop=1280:640:0:1280" -pix_fmt yuv420p tile13.y4m -vf "crop=1280:640:1280:1280" -pix_fmt yuv420p tile14.y4m -vf "crop=1280:640:2560:1280" -pix_fmt yuv420p tile15.y4m -vf "crop=1280:640:3840:1280" -pix_fmt yuv420p tile16.y4m -vf "crop=1280:640:5120:1280" -pix_fmt yuv420p tile17.y4m -vf "crop=1280:640:6400:1280" -pix_fmt yuv420p tile18.y4m -vf "crop=1280:640:0:1920" -pix_fmt yuv420p tile19.y4m -vf "crop=1280:640:1280:1920" -pix_fmt yuv420p tile20.y4m -vf "crop=1280:640:2560:1920" -pix_fmt yuv420p tile21.y4m -vf "crop=1280:640:3840:1920" -pix_fmt yuv420p tile22.y4m -vf "crop=1280:640:5120:1920" -pix_fmt yuv420p tile23.y4m -vf "crop=1280:640:6400:1920" -pix_fmt yuv420p tile24.y4m -vf "crop=1280:640:0:2560" -pix_fmt yuv420p tile25.y4m -vf "crop=1280:640:1280:2560" -pix_fmt yuv420p tile26.y4m -vf "crop=1280:640:2560:2560" -pix_fmt yuv420p tile27.y4m -vf "crop=1280:640:3840:2560" -pix_fmt yuv420p tile28.y4m -vf "crop=1280:640:5120:2560" -pix_fmt yuv420p tile29.y4m -vf "crop=1280:640:6400:2560" -pix_fmt yuv420p tile30.y4m -vf "crop=1280:640:0:3200" -pix_fmt yuv420p tile31.y4m -vf "crop=1280:640:1280:3200" -pix_fmt yuv420p tile32.y4m -vf "crop=1280:640:2560:3200" -pix_fmt yuv420p tile33.y4m -vf "crop=1280:640:3840:3200" -pix_fmt yuv420p tile34.y4m -vf "crop=1280:640:5120:3200" -pix_fmt yuv420p tile35.y4m -vf "crop=1280:640:6400:3200" -pix_fmt yuv420p tile36.y4m
```

## Spatial and Temporal Information

We evaluated the spatial information (SI) and temporal information (TI) of the tiles using the following command.

```powershell
siTi.ps1 -tiles "tile1.y4m", "tile2.y4m", "tile3.y4m", "tile4.y4m", "tile5.y4m", "tile6.y4m", "tile7.y4m", "tile8.y4m", "tile9.y4m", "tile10.y4m", "tile11.y4m", "tile12.y4m", "tile13.y4m", "tile14.y4m", "tile15.y4m", "tile16.y4m", "tile17.y4m", "tile18.y4m", "tile19.y4m", "tile20.y4m", "tile21.y4m", "tile22.y4m", "tile23.y4m", "tile24.y4m", "tile25.y4m", "tile26.y4m", "tile27.y4m", "tile28.y4m", "tile29.y4m", "tile30.y4m", "tile31.y4m", "tile32.y4m", "tile33.y4m", "tile34.y4m", "tile35.y4m", "tile36.y4m" -resultsFile siTiTiles.csv
```

The result files for `Fireplace` (`siTiFireplace.csv`), `Suburb` (`siTiSuburb.csv`) and `VirtualReality` (`siTiVirtualReality.csv`) are available in this repository.
The files follow this format.

| Column Name | Description                            |
|:------------|:---------------------------------------|
| input_file  | The file name of the tile.             |
| n           | The index of the frame (starts at 1).  |
| si          | The spatial information of the frame.  |
| ti          | The temporal information of the frame. |

## Rate-distortion Benchmark

To calculate the rate-distortion of each tile, we first evaluate the bitrate and visual quality of their segments according to their encoding parameters using the following command.

```powershell
bitrateVmaf.ps1 -tiles "suburb13.y4m", "suburb19.y4m", "suburb31.y4m", "fireplace5.y4m", "fireplace6.y4m", "fireplace33.y4m", "virtualReality24.y4m", "virtualReality26.y4m" -codecs "hevc_nvenc", "h264_nvenc" -presets p1, p2, p3, p4, p5, p6, p7 -qps 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40 -heights 0, 320 -segmentTime 2 -segmentGOP 60 -segmentDirectory ".\segments" -dataFile fireplaceSuburbVirtualRealityBitrateVmaf.csv -vmafLogDirectory "vmafLogs"
```

The results file for all videos (`fireplaceSuburbVirtualRealityBitrateVmaf.csv`) is available in this repository.
The file follows this format.

To get detailed information about the visual quality, download the [VMAF logs files](https://drive.google.com/file/d/1N82Ca6uBmQ5JlUA_ZmwfTpxqEywr0tij/view?usp=sharing) for all segments.
Every file contains the PSNR (Y, Cb and Cr), VIF, VMAF and more of every frame.

| Column Name | Description                                                                                                                      |
|:------------|:---------------------------------------------------------------------------------------------------------------------------------|
| tile        | The file name of the tile.                                                                                                       |
| segment     | The index of the segment (starts at 0).                                                                                          |
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
encodingTime.ps1 -tiles "suburb13.y4m", "suburb19.y4m", "suburb31.y4m", "fireplace5.y4m", "fireplace6.y4m", "fireplace33.y4m", "virtualReality24.y4m", "virtualReality26.y4m" -codecs "hevc_nvenc", "h264_nvenc" -presets p1, p2, p3, p4, p5, p6, p7 -qps 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40 -heights 0, 320 -repetitions 5 -segmentTime 2 -segmentGOP 60 -segmentDirectory ".\segments" -dataFile fireplaceSuburbVirtualRealityEncodingTime.csv
```

The results file all videos (`fireplaceSuburbVirtualRealityEncodingTime.csv`) is available in this repository.
The file follows this format.

| Column Name | Description                                                                         |
|:------------|:------------------------------------------------------------------------------------|
| tile        | The file name of the tile.                                                          |
| repetition  | The index of the repetition (starts at 0).                                          |
| codec       | The codec used to encode the segments.                                              |
| preset      | The preset used to encode the segments.                                             |
| qp          | The quantization parameters to encode the segments.                                 |
| height      | The segments' height in pixels. A value of zero means that the height is unchanged. |
| time        | The required time, in seconds, to encode all the segments of the tile.              |

## Per Segment Encoding Speed Benchmark

We evaluate the time to encode every segment of the tiles according to their encoding parameters using the following command.

```powershell
perSegmentEncodingTime.ps1 -tiles "suburb13.y4m", "suburb19.y4m", "suburb31.y4m", "fireplace5.y4m", "fireplace6.y4m", "fireplace33.y4m", "virtualReality24.y4m", "virtualReality26.y4m" -codecs "hevc_nvenc", "h264_nvenc" -presets p1, p2, p3, p4, p5, p6, p7 -qps 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40 -heights 0, 320 -repetitions 1 -segmentTime 2 -segmentGOP 60 -segmentDirectory ".\segments" -dataFile fireplaceSuburbVirtualRealitySegmentsEncodingTime.csv
```

The results file for all videos (`fireplaceSuburbVirtualRealitySegmentsEncodingTime.csv`) is available in this repository.
The file follows this format.

| Column Name | Description                                                                         |
|:------------|:------------------------------------------------------------------------------------|
| tile        | The file name of the tile.                                                          |
| segment     | The index of the segment (starts at 0).                                             |
| repetition  | The index of the repetition (starts at 0).                                          |
| codec       | The codec used to encode the segments.                                              |
| preset      | The preset used to encode the segments.                                             |
| qp          | The quantization parameters to encode the segments.                                 |
| height      | The segments' height in pixels. A value of zero means that the height is unchanged. |
| time        | The required time, in seconds, to encode all the segments of the tile.              |

## VMAF Speed

We evaluate the computing speed of VMAF for every segment according to subsampling value using the following command.

```
ffmpeg -loglevel error -i comparedSegment.mp4 -i originalSegment.mp4 -filter_complex "libvmaf=feature=name=psnr:n_threads=8:n_subsample=2:log_path=log.json:log_fmt=json" -f null -
```

The results file (`vmafSpeed.csv`) is available in this repository.
The file follows this format.

| Column Name | Description                                                               |
|:------------|:--------------------------------------------------------------------------|
| subsampling | The subsampling value, i.e., to calculate scores only every $ N $ frames. |
| speed       | The computing speed in frames per second.                                 |

## Ethics

We have obtained the consent of the recognizable people in the videos to publish the data.
Follow these rules when using the videos.

- Don't use the videos in illegal, immoral, offensive, misleading or deceptive content.
- Don't sell or redistribute the videos on other platforms.
- Don't use the videos in your trade-mark, design-mark, trade-name, business name or service mark.
- Videos containing recognizable trademarks, logos or brands cannot be used for commercial purposes.
- Don't imply that any recognizable person or brand in the videos endorses your content or product.

## Citation

To be added after acceptance.
