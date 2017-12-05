---
title: "Obs_with_gpu"
date: 2017-12-02T21:28:34-05:00
subtitle: ""
tags: []
---
```
679  cd Downloads/
  680  wget https://developer.nvidia.com/video-sdk-601
  681  ls
  682  unzip video-sdk-601
  683  ls
  684  cd nvidia_video_sdk_6.0.1/
  685  ls
  686  ls Samples/common/inc/
  687  sudo dnf install libfdk-aac-dev
  688  sudo dnf install fdk-acc-devel
  689  sudo dnf install fdk-aac-devel
  690  dnfdownloader
  691  sudo dnf install dnfdownloader
  692  sudo dnf install dnf*
  693  sudo dnf install dnf-utils
  694  dnfdownloader
  695  cd ..
  696  ls
  697  dnf download --source ffmpeg
  698  ls
  699  dnf builddep
  700  ls
  701  mkdir ffmpeg_source
  702  mv -f ffmpeg-3.3.5-2.fc27.src.rpm ffmpeg_source/
  703  cd ffmpeg_source/
  704  untar -azxvf ffmpeg-3.3.5-2.fc27.src.rpm 
  705  tar -azxvf ffmpeg-3.3.5-2.fc27.src.rpm 
  706  ls
  707  dnf install ffmpeg-3.3.5-2.fc27.src.rpm 
  708  sudo dnf install ffmpeg-3.3.5-2.fc27.src.rpm 
  709  rpm2cpio
  710  man rpm2cpio
  711  rpm2cpio ffmpeg-3.3.5-2.fc27.src.rpm 
  712  rpm2cpio ./ffmpeg-3.3.5-2.fc27.src.rpm | cpio -idmv
  713  ls
  714  tar -azxvf ffmpeg-3.3.5.tar.xz
  715  tar -axvf ffmpeg-3.3.5.tar.xz
  716  ls
  717  vim ffmpeg.spec 
  718  ffmpeg -buildconf
  719  ls
  720  cd ffmpeg-3.3.5/
  721  ls
  722  cd ..
  723  ls
  724  cd ..
  725  ls
  726  cd nvidia_video_sdk_6.0.1/
  727  ls
  728  cp nvidia_video_sdk_6.0.1/Samples/common/inc/*.h /usr/local/include/
  729  ls Samples/common/inc/*.h
  730  cp /Samples/common/inc/*.h /usr/local/include/
  731  ls
  732  cp Samples/common/inc/*.h /usr/local/include/
  733  ls /usr/local/include/
  734  sudo cp Samples/common/inc/*.h /usr/local/include/
  735  ls /usr/local/include/
  736  cd
  737  cd Downloads/
  738  ls
  739  cd ffmpeg_source/
  740  ls
  741  cd ffmpeg-3.3.5/
  742   ffmpeg -buildconf
  743  ls
  744  ./configure --prefix=/usr --bindir=/usr/bin --datadir=/usr/share/ffmpeg --docdir=/usr/share/doc/ffmpeg --incdir=/usr/include/ffmpeg --libdir=/usr/lib64 --mandir=/usr/share/man --arch=x86_64 --optflags='-O2 -g -pipe -Wall -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches -specs=/usr/lib/rpm/redhat/redhat-hardened-cc1 -m64 -mtune=generic' --extra-ldflags='-Wl,-z,relro -specs=/usr/lib/rpm/redhat/redhat-hardened-ld ' --extra-cflags='-I/usr/include/nvenc ' --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libvo-amrwbenc --enable-version3 --enable-bzlib --disable-crystalhd --enable-fontconfig --enable-frei0r --enable-gcrypt --enable-gnutls --enable-ladspa --enable-libass --enable-libbluray --enable-libcdio --enable-indev=jack --enable-libfreetype --enable-libfribidi --enable-libgsm --enable-libmp3lame --enable-nvenc --enable-openal --enable-opencl --enable-opengl --enable-libopenjpeg --enable-libopus --enable-libpulse --enable-libschroedinger --enable-libsoxr --enable-libspeex --enable-libtheora --enable-libvorbis --enable-libv4l2 --enable-libvpx --enable-libx264 --enable-libx265 --enable-libxvid --enable-avfilter --enable-avresample --enable-postproc --enable-pthreads --disable-static --enable-shared --enable-gpl --disable-debug --disable-stripping --shlibdir=/usr/lib64 --enable-libmfx --enable-runtime-cpudetect
  745  sudo dnf install yasm/nasm
  746  sudo dnf install yasm mas,
  747  sudo dnf install yasm nasm
  748  ./configure --prefix=/usr --bindir=/usr/bin --datadir=/usr/share/ffmpeg --docdir=/usr/share/doc/ffmpeg --incdir=/usr/include/ffmpeg --libdir=/usr/lib64 --mandir=/usr/share/man --arch=x86_64 --optflags='-O2 -g -pipe -Wall -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches -specs=/usr/lib/rpm/redhat/redhat-hardened-cc1 -m64 -mtune=generic' --extra-ldflags='-Wl,-z,relro -specs=/usr/lib/rpm/redhat/redhat-hardened-ld ' --extra-cflags='-I/usr/include/nvenc ' --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libvo-amrwbenc --enable-version3 --enable-bzlib --disable-crystalhd --enable-fontconfig --enable-frei0r --enable-gcrypt --enable-gnutls --enable-ladspa --enable-libass --enable-libbluray --enable-libcdio --enable-indev=jack --enable-libfreetype --enable-libfribidi --enable-libgsm --enable-libmp3lame --enable-nvenc --enable-openal --enable-opencl --enable-opengl --enable-libopenjpeg --enable-libopus --enable-libpulse --enable-libschroedinger --enable-libsoxr --enable-libspeex --enable-libtheora --enable-libvorbis --enable-libv4l2 --enable-libvpx --enable-libx264 --enable-libx265 --enable-libxvid --enable-avfilter --enable-avresample --enable-postproc --enable-pthreads --disable-static --enable-shared --enable-gpl --disable-debug --disable-stripping --shlibdir=/usr/lib64 --enable-libmfx --enable-runtime-cpudetect
  749  sudo dnf install frei0r
  750  sudo dnf install frei0r*
  751  sudo dnf install frei0r-devel
  753  sudo dnf install gnutls
  754  sudo dnf uninstall sudo dnf install libgnutls-devel
  755   sudo dnf install libgnutls-devel
  756   sudo dnf install gnutls*
  757   sudo dnf install gnutls-devel
  759  sudo dnf install caml
  760  sudo dnf install ocaml
  762  sudo dnf install ladspa
  764  sudo dnf install ladspa-devel
  766  sudo dnf install libass
  767  sudo dnf install libass-devel
  769  sudo dnf install libbluray
  770  sudo dnf install libbluray-devel
  772  sudo dnf install libgsm
  773  sudo dnf install libgsm-devel
  774  sudo dnf install *libgsm*
  775  sudo dnf install gsm-devel
  777  sudo dnf install libmfx-devel
  779  sudo dnf install libmfx
  780  sudo dnf install libmfx*
  782  sudo dnf install libmfx*
  783  ffmpeg -buildconf
  785  ls
  786  pwd
  787  cd ..
  788  ls
  789  cd -
  790  ls
  791  vim INSTALL.md 
  792  vim VERSION 
  793  cd ..
  794  ls
  795  vim ffmpeg.spec 
  797  clear
 798  sudo dnf install bzip2-devel faac-devel fdk-aac-devel flite-devel fontconfig-devel freetype-devel frei0r-devel game-music-emu-devel gnutls-devel gsm-devel ilbc-devel lame-devel jack-audio-connection-kit-devel ladspa-devel libass-devel libbluray-devel libbs2b-devel libcaca-devel libcdio-paranoia-devel libchromaprint-devel libcrystalhd-devel libavc1394-devel libdc1394-devel libiec61883-devel libgcrypt-devel libGL-devel libmodplug-devel librtmp-devel libsmbclient-devel libssh-devel libtheora-devel libv4l-devel libvdpau-devel libvorbis-devel libvpx-devel libmfx-devel libXvMC-devel libva-devel yasm libwebp-devel netcdf-devel nvenc-devel opencore-amr-devel vo-amrwbenc-devel openal-soft-devel opencl-headers ocl-icd-devel  opencv-devel openjpeg2-devel opus-devel pulseaudio-libs-devel perl rubberband-devel schroedinger-devel SDL2-devel snappy-devel soxr-devel speex-devel subversion tesseract-devel twolame-devel wavpack-devel x264-devel x265-devel xvidcore-devel zlib-devel zeromq-devel zvbi-devel 
  799  ls
  800  cd ffmpeg-3.3.5/
  802  sudo dnf install libopenjpeg
  803  sudo dnf install libopenjpeg-devel
  804  sudo dnf install openjpeg-libs
  805  sudo dnf install openjpeg-libs-devel
  807  sudo dnf install openjpeg
  809  sudo dnf install openjpeg*
  810  sudo dnf install openjpeg-devel
```

