# VQ-MIC
Reporte de pruebas de calidad de video para distintos escenarios

1.  VMAF and FFMPEG installation

Machine :  c5.xlarge
OS : Ubuntu 20

wget https://github.com/Netflix/vmaf/archive/v1.5.3.tar.gz
tar -xf  v1.5.3.tar.gz

sudo apt update
sudo apt install python3 python3-pip python3-setuptools python3-wheel ninja-build doxygen
pip3 install meson
pip3 install Cython
pip3 install numpy


Needs to add filter.

| Channel name |	Config |	Bitrate (Mbps) | Lookahead | GOP (sec) | B-frames | Profile | Level | Adaptive quantization | Slides | %GPU | MEM (GB) | VMAF | PSNR |
| ------------- |	------------- |	------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| HBO HD | config/ref/HBO_HD_1080p-5Mbps-ref.xml | 5 | Medium |	2 |	3 |	High | Auto |	off |	4 | 16 | 1.2 | 98.38 | 60 |
| HBO HD | HBO_1080p_1.ts | 5 | High |	2 |	3 |	High | Auto |	off |	4 | 16 | 1.2 | 98.38 | 60 |


