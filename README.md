This is a sample HLS stream for HEVC / H265 / HEV1 / HVC1 with chunk duration of 2 seconds. Source data is downloaded from https://download.blender.org/durian/movies/Sintel.2010.4k.mkv, then re-encoded using FFmpeg. This is the version info given by FFmpeg when it's run without arguments:

```
ffmpeg version 2024-03-18-git-a32f75d6e2-full_build-www.gyan.dev Copyright (c) 2000-2024 the FFmpeg developers
  built with gcc 13.2.0 (Rev5, Built by MSYS2 project)
  configuration: --enable-gpl --enable-version3 --enable-static --pkg-config=pkgconf --disable-w32threads --disable-autodetect --enable-fontconfig --enable-iconv --enable-gnutls --enable-libxml2 --enable-gmp --enable-bzlib --enable-lzma --enable-libsnappy --enable-zlib --enable-librist --enable-libsrt --enable-libssh --enable-libzmq --enable-avisynth --enable-libbluray --enable-libcaca --enable-sdl2 --enable-libaribb24 --enable-libaribcaption --enable-libdav1d --enable-libdavs2 --enable-libuavs3d --enable-libzvbi --enable-librav1e --enable-libsvtav1 --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxavs2 --enable-libxvid --enable-libaom --enable-libjxl --enable-libopenjpeg --enable-libvpx --enable-mediafoundation --enable-libass --enable-frei0r --enable-libfreetype --enable-libfribidi --enable-libharfbuzz --enable-liblensfun --enable-libvidstab --enable-libvmaf --enable-libzimg --enable-amf --enable-cuda-llvm --enable-cuvid --enable-ffnvcodec --enable-nvdec --enable-nvenc --enable-dxva2 --enable-d3d11va --enable-libvpl --enable-libshaderc --enable-vulkan --enable-libplacebo --enable-opencl --enable-libcdio --enable-libgme --enable-libmodplug --enable-libopenmpt --enable-libopencore-amrwb --enable-libmp3lame --enable-libshine --enable-libtheora --enable-libtwolame --enable-libvo-amrwbenc --enable-libcodec2 --enable-libilbc --enable-libgsm --enable-libopencore-amrnb --enable-libopus --enable-libspeex --enable-libvorbis --enable-ladspa --enable-libbs2b --enable-libflite --enable-libmysofa --enable-librubberband --enable-libsoxr --enable-chromaprint
  libavutil      59.  2.100 / 59.  2.100
  libavcodec     61.  1.101 / 61.  1.101
  libavformat    61.  0.100 / 61.  0.100
  libavdevice    61.  0.100 / 61.  0.100
  libavfilter    10.  0.100 / 10.  0.100
  libswscale      8.  0.100 /  8.  0.100
  libswresample   5.  0.100 /  5.  0.100
  libpostproc    58.  0.100 / 58.  0.100
```

This is the conversion command: HLS with HEVC / H265 packaged into MPEG-TS (.ts) files.

```
ffmpeg -y '-i' Sintel.2010.4k.mkv '-map' 'v:0' -c:v libx265 -preset ultrafast -b:v 40597530 -g 24 '-f' 'hls' '-hls_time' '2' '-hls_playlist_type' 'vod' '-hls_segment_type' 'mpegts' '-hls_list_size' '0' '-hls_segment_filename' 'seg_%d.ts' '-start_number' '0' '-master_pl_name' 'master-video.m3u8' '-muxdelay' '0' '-muxpreload' '0' '-output_ts_offset' '0.000000' '-segment_format_options' 'movflags=frag_keyframe+empty_moov+default_base_moof' 'manifest.m3u8'
```
