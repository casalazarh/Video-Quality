# Video-Quality
Reporte de pruebas de calidad de video para distintos escenarios

1.  VMAF and FFMPEG installation

- Server :  t3.large
- OS : Ubuntu 20.X
- ffmpeg static version : version N-55618-ga0acc44106-static https://johnvansickle.com/ffmpeg/


Prerequisites:

- apt update 
- apt install pkg-config -y
- apt-get install --no-install-recommends\
    ninja-build \
    python3 \
    python3-pip \
    python3-setuptools \
    python3-wheel \
    ninja-build \
    wget \
    doxygen \
    autoconf \
    automake \
    cmake \
    g++ \
    gcc \
    pkg-config \
    make \
    nasm \
    yasm -y
    
- sudo -i
- curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
- python3 get-pip.py
- python3 -m pip install meson


FFMPEG Static Installation:

- wget https://johnvansickle.com/ffmpeg/builds/ffmpeg-git-amd64-static.tar.xz
- tar xvf ffmpeg-git-amd64-static.tar.xz
- sudo mv ffmpeg-git-20210110-amd64-static/ffmpeg fffmpeg-git-20210110-amd64-static/ffprobe  /usr/local/bin/

VMAF Instalattion:

- wget https://github.com/Netflix/vmaf/archive/v1.5.3.tar.gz
- tar -xf  v1.5.3.tar.gz
- cd vmaf-1.5.3/libvmaf/
- meson build --buildtype release
- ninja -vC build
- ninja -vC build test
- ninja -vC build install


2. Example:

ffmpeg -i HBO_HD_RxSat27Oc2020_5min.ts -i HBO_HD_1080-5M-ref.ts -filter_complex "[0:v]select=gt(n\,0),setpts=PTS-STARTPTS[main]; [1:v]select=gt(n\,1),setpts=PTS-STARTPTS[ref]; [main][ref]libvmaf=psnr=1:log_path=HBO_HD_1080_1.json:log_fmt=json" -frames:v 5000 -f null -



| Channel name |	Config |	Bitrate (Mbps) | Lookahead | GOP (sec) | B-frames | Profile | Level | Adaptive quantization | Slides | %GPU | MEM (GB) | VMAF | PSNR |
| ------------- |	------------- |	------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| HBO HD | config/ref/HBO_HD_1080p-5Mbps-ref.xml | 5 | Medium |	2 |	3 |	High | Auto |	off |	4 | 16 | 1.2 | 98.38 | 60 |
| HBO HD | HBO_1080p_1.ts | 5 | High |	2 |	3 |	High | Auto |	off |	4 | 16 | 1.2 | 98.38 | 60 |


