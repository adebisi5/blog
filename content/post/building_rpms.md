---
title: "Building_rpms"
date: 2017-12-08T18:06:06-05:00
subtitle: ""
tags: [linux,fedora,rpm,mock]
---
So After spending hours on trying to figure out how to build obs into an rpm using mock I finally succeeded. At the bottom is my whole history of commands and things I went through trying to figure out dependencies, building local and with mock.... I have to say this is a very interesting learning experience. But, one thing I found is that everyone does the spec file differently. Some build the spec that its easily to follow with variables and others have a mix of using some variables and hard coded lines. So one issue that I ran into was that I changed the ```version:``` at the top of the spec file but, the version was hardcoded later on. So I went I got an error in the build "can't cd x.x no file or directory" I spend around 30 minutes in the spec file and noticed that It was hardcoded for the old version.



 772  sudo dnf install obs-studio
  773  sudo dnf remove ffmpeg
  774  sudo dnf install pavucontrol
  775  pwd
  776  make -j4
  777  sudo dnf install ffmpeg-devel
  778  make -j4
  779  sudo dnf install libjack
  780  sudo dnf install jack-audio-connection-kit
  781  sudo dnf install libjack-devel
  782  sudo dnf install jack2
  783  sudo dnf install jack2*
  784  sudo dnf install jack
  785  sudo dnf install jack*
  786  sudo dnf install jack-audio-connection-kit-example-clients jack-keyboard jack-rack jack_capture
  787  make -j4
  788  sudo dnf provides \*libjack.so
  789  sudo dnf install jack-audio-connection-kit-devel
  790  sudo dnf install qmmp-1.1.10-1
  791  sudo dnf install qmmp
  792  make -j4
  793  history | grep dnf
  794  dnfdownloader --source obs-studio
  795  dnf downloader --source obs-studio
  796  sudo dnf downloader --source obs-studio
  797  sudo dnf-command downloader --source obs-studio
  798  sudo dnf-command download --source obs-studio
  799  sudo dnf download --source obs-studio
  800  ls
  801  mkdir rpm
  802  mv obs-studio-20.0.1-1.fc27.src.rpm rpm
  803  cd rpm
  804  rpm2cpio ./obs-studio-20.0.1-1.fc27.src.rpm | cpio -idmv
  805  ls
  806  vim obs-studio.spec 
  807  rpmbuild -ba obs-studio.spec 
  808  cp ~/Downloads/obs-studio-20.1.3.tar.gz ~/rpmbuild/SOURCES/
  809  rpmbuild -ba obs-studio.spec 
  810  vim obs-studio.spec 
  811  rpmbuild -ba obs-studio.spec 
  812  ls
  813  cp obs-ffmpeg-mux.patch ~/rpmbuild/SOURCES/
  814  rpmbuild -ba obs-studio.spec 
  815  vim obs-studio.spec 
  816  rpmbuild -ba obs-studio.spec 
  817  vim obs-studio.spec 
  818  rpmbuild -ba obs-studio.spec 
  819  vim obs-studio.spec 
  820  rpmlint obs-studio.spec 
  821  vim obs-studio.spec 
  822  rpmlint obs-studio.spec 
  823  rpmbuild -bi --short-circuit obs-studio.spec 
  824  vim obs-studio.spec 
  825  cat /var/tmp/rpm-tmp.Kc8Iwe 
  826  ls
  827  fedpkg
  828  fedpkg --release f27 mockbuild
  829  ls
  830  cp ~/Downloads/obs-studio-20.1.3.tar.gz .
  831  fedpkg --release f27 mockbuild
  832  ls
  833  ls results_obs-studio/
  834  ls results_obs-studio/20.1.3/
  835  ls results_obs-studio/20.1.3/1.fc27/
  836  ls
  837  vim /etc/mock/fedora-27-x86_64.cfg
  838  sudo vim /etc/mock/epel-7-x86_64-rpmfusion_free.cfg
  839  fedpkg --release f27 mockbuild
  840  cd
  841  cd Downloads/
  842  ls
  843  mkdir obs_studio_test_srpm
  844  ls
  845  cp obs-studio-20.0.1-1.fc27.src.rpm obs_studio_test_srpm
  846  cd obs_studio_test_srpm/
  847  ls
  848  rpm2cpio ./obs-studio-20.0.1-1.fc27.src.rpm | cpio -idmv
  849  ls
  850  vim obs-studio
  851  vim obs-studio.spec 
  852  fedpkg --release f27 mockbuild
  853  cp ~/Downloads/obs-studio-20.1.3.tar.gz .
  854  fedpkg --release f27 mockbuild
  855  ls /var/lib/mock/
  856  sudo dnf install ffmpeg-devel
  857  sudo dnf clean all
  858  sudo dnf install ffmpeg-devel
  859  sudo dnf what provides ffmpeg-devel
  860  sudo dnf  provides ffmpeg-devel
  861  sudo ls /etc/mock/
  862  sudo vim /etc/mock/epel-7-x86_64-rpmfusion_free.cfg
  863  cd /etc/mock
  864  sudo mv -f epel-7-x86_64-rpmfusion_free.cfg fedora-27-x86_64-rpmfusion_free.cfg
  865  ls
  866  vim fedora-27-x86_64-rpmfusion_free.cfg
  867  vim fedora-27-x86_64.cfg
  868  vim fedora-27-x86_64-rpmfusion_free.cfg
  869  sudo dnf install mock-rpmfusion-free mock-rpmfusion-nonfree
  870  ls
  871  cat fedora-27-x86_64-rpmfusion_nonfree.cfg
  872  ls
  873  fedpkg --release f27 mockbuild
  874  ls
  875  cd -
  876  fedpkg --release f27 mockbuild
  877  man mock
  878  man fedpck
  879  man fedpckg
  880  man fedpkg
  881  man mock
  882  sudo vim /etc/mock/default.cfg 
  883  sudo vim /etc/mock/epel-7-x86_64-rpmfusion_free.cfg 
  884  sudo vim /etc/mock/default.cfg 
  885  fedpkg --release f27 mockbuild
  886  ls
  887  vim obs-studio.spec 
  888  ls
  889  mock
  890  ls /etc/mock/
  891  ;s
  892  ls
  893  rm -rf obs-studio-20.1.3-1.fc27.src.rpm
  894  ls
  895  man rpmbuild-bs
  896   rpmbuild-bs
  897  sudo dnf install fedora-packager fedora-review
  898  sudo usermod -a -g mock jcasanova
  899  sudo usermod -a -G mock jcasanova
  900  exit
  901  cd Downloads/
  902  ls
  903  cd obs_studio_test_srpm/
  904  ls
  905  man fedora-packager-setup
  906  id
  907  fedora-packager-setup
  908  ls
  909  fedpkg --release f27 local
  910  ls
  911  cd obs-studio-20.1.3
  912  ls
  913  cd ..
  914  ls
  915  rpmbuild-bs obs-studio.spec 
  916  sudo dnf provides rpmbuild-bs
  917  rpmbuild -bs obs-studio.spec 
  918  ls
  919  cp ~/rpmbuild/SRPMS/obs-studio-20.1.3-1.fc27.src.rpm .
  920  ls
  921  mock /etc/mock/default --rebuild obs-studio-20.1.3-1.fc27.src.rpm
  922  mock /etc/mock/default --rebuild obs-studio-20.1.3-1.fc27.src.rpm 
  923  mkdir results
  924  mock /etc/mock/default --rebuild obs-studio-20.1.3-1.fc27.src.rpm --resultdir=results
  925  mock -r /etc/mock/ --rebuild obs-studio-20.1.3-1.fc27.src.rpm --resultdir=results
  926  mock /etc/mock/default.cfg --rebuild obs-studio-20.1.3-1.fc27.src.rpm --resultdir=results
  927  fedpkg mockbuild
  928  ls
  929  ls obs-studio.spec 
  930  fedpkg mockbuild obs-studio.spec
  931  fedpkg mockbuild --release f27
  932  history | grep fedpkg
  933  fedpkg --release f27 mockbuild
  934  fedpkg --release f27 mockbuildls
  935  ls
  936  ls /var/mock
  937  ls /var/lib/mock
  938  ls
  939  rm -rf obs-studio-20.1.3-1.fc27.src.rpm
  940  ls
  941  fedpkg --release f27 mockbuildls
  942  fedpkg --release f27 mockbuilds
  943  fedpkg --release f27 mockbuild
  944  ls
  945  ls results
  946  rm -rf results
  947  ls results_obs-studio/
  948  cat results_obs-studio/20.1.3/1.fc27/build.log 
  949  ls /var/lib/mock/
  950  ls
  951  cd ..
  952  ls
  953  rm -rf obs_studio_test_srpm/
  954  cd git/
  955  ls
  956  mkdir obs_studio_test_srpm
  957  cd obs_studio_test_srpm/
  958  ls
  959  cp ../../obs-studio-20.1.3.tar.gz .
  960  ls
  961  cp ../../obs-studio-20.0.1-1.fc27.src.rpm .
  962  ls
  963  rpm2cpio ./obs-studio-20.0.1-1.fc27.src.rpm | cpio -idmv
  964  ls
  965  vim obs-studio.spec 
  966  ls
  967  fedpkg --release f27 mockbuild
  968  vim obs-studio.spec 
  969  vim /etc/mock/default.cfg 
  970  sudo vim /etc/mock/default.cfg 
  971  fedpkg --release f27 mockbuild
  972  cat /etc/mock/fedora-27-x86_64-rpmfusion_free.cfg
  973  sudo vim /etc/mock/default.cfg 
  974  fedpkg --release f27 mockbuild
  975  vim obs-studio.spec 
  976  ls
  977  cp obs-studio-20.1.3.tar.gz ~/rpmbuild/SOURCES/
  978  ls
  979  fedpkg --release f27 mockbuild
  980  sudo vim /etc/mock/default.cfg 
  981  fedpkg --release f27 mockbuild
  982  sudo dnf install rpmfusion-free-release
  983  sudo vim /etc/mock/default.cfg 
  984  sudo dnf install rpmfusion-free-release
  985  fedpkg --release f27 mockbuild
  986  sudo dnf install rpmfusion-nonfree-release
  987  sudo vim /etc/mock/default.cfg 
  988  fedpkg --release f27 mockbuild
  989  sudo vim /etc/mock/default.cfg 
  990  fedpkg --release f27 mockbuild
  991  sudo vim /etc/mock/default.cfg 
  992  sudo cat /etc/yum.repos.d/rpmfusion-free.repo 
  993  sudo vim /etc/mock/default.cfg 
  994  sudo cat /etc/yum.repos.d/rpmfusion-free-updates.repo 
  995  cd Downloads/git/
  996  ls
  997  cd obs_studio_test_srpm/
  998  ls
  999  sudo vim /etc/mock/default.cfg 
 1000  sudo cat /etc/yum.repos.d/rpmfusion-free-updates.repo 
 1001  cd Downloads/obs_test/
 1002  cd ../git/obs_studio_test_srpm/
 1003  ls
 1004  sudo vim /etc/mock/default.cfg 
 1005  fedpkg --release f27 mockbuild
 1006  fedpkg --release f27 mockbuild -v
 1007  fedpkg -h
 1008  fedpkg --release f27 mockbuild -
 1009  fedpkg --release f27 mockbuild 
 1010  sudo vim /etc/mock/default.cfg 
 1011  fedpkg --release f27 mockbuild 
 1012  sudo vim /etc/mock/default.cfg 
 1013  fedpkg --release f27 mockbuild 
 1014  sudo vim /etc/mock/default.cfg 
 1015  fedpkg --release f27 mockbuild 
 1016  sudo vim /etc/mock/fedora-27-x86_64-rpmfusion_free.cfg
 1017  sudo vim /etc/mock/default.cfg 
 1018  mock -r MOCK_CONFIG --init
 1019  mock -r fedora-27-ppc64-rpmfusion_free.cfg fedora-27-ppc64-rpmfusion_nonfree.cfg
 1020  mock -r fedora-27-x86_64-rpmfusion_free.cfg fedora-27-x86_64-rpmfusion_nonfree.cfg --init
 1021  mock -r fedora-27-x86_64-rpmfusion_free.cfg  --init
 1022  mock -r fedora-27-x86_64-rpmfusion_free  --init
 1023  mock -r fedora-27-x86_64-rpmfusion_nonfree  --init
 1024  ls
 1025  cat obs-studio.spec 
 1026  mock -r fedora-27-x86_64-rpmfusion_free  --install ffmpeg
 1027  mock -r fedora-27-x86_64 fedora-27-x86_64-rpmfusion_free  --install ffmpeg
 1028  mock -r fedora-27-x86_64-rpmfusion_nonfree  --init
 1029  mock -r fedora-27-x86_64  --init
 1030  fedpkg --release f27 mockbuild 
 1031  mock -r fedora-27-x86_64 fedora-27-x86_64-rpmfusion_free  --install ffmpeg-devel vlc-devel x264-devel
 1032  mock -r   --install ffmpeg-devel vlc-devel x264-devel
 1033  mock    --install ffmpeg-devel vlc-devel x264-devel
 1034  ls
 1035  mock -r  fedora-27-x86_64-rpmfusion_nonfree --init
 1036  mock    --install ffmpeg-devel vlc-devel x264-devel
 1037  mock -r fedora-27-x86_64 init
 1038  mock -r fedora-27-x86_64-rpmfusion_free --install ffmpeg-devel
 1039  mock -r fedora-27-x86_64-rpmfusion_free --install vlc-devel
 1040  fedpkg --release f27 mockbuild 
 1041  sudo vim /etc/mock/default.cfg 
 1042  fedpkg --release f27 mockbuild 
 1043  sudo vim /etc/mock/default.cfg 
 1044  fedpkg --release f27 mockbuild 
 1045  sudo vim /etc/mock/default.cfg 
 1046  fedpkg --release f27 mockbuild 
 1047  df -h
 1048  ls /var/lib/mock/
 1049  ls
 1050  vim /etc/mock/site-defaults.cfg 
 1051  sudo vim /etc/mock/site-defaults.cfg 
 1052  fedpkg --release f27 mockbuild 
 1053  mkdir ~/mock
 1054  fedpkg --release f27 mockbuild 
 1055  sudo dnf update
 1056  sudo dnf update --alowerasing
 1057  sudo dnf update --allowerasing
 1058  sudo dnf update --best --allowerasing
 1059  df -h
 1060  cd /
 1061  ls
 1062  cd tmp/
 1063  ls
 1064  ds -h .
 1065  du -h .
 1066  ls
 1067  cd
 1068  cd /
 1069  ls
 1070  cd
 1071  df -h
 1072  sudo vim /etc/mock/site-defaults.cfg 
 1073  pwd
 1074  cd 
 1075  cd Downloads/git/obs_studio_test_srpm/
 1076  fedpkg --release f27 mockbuild 
 1077  sudo vim /etc/mock/site-defaults.cfg 
 1078  vim ~/.config/mock.cfg
 1079  sudo vim /etc/mock/site-defaults.cfg 
 1080  fedpkg --release f27 mockbuild 

