# Video-Quality
Reporte de pruebas de calidad de video para distintos escenarios

## VMAF and FFMPEG installation

- Server :  t3.large
- OS : Ubuntu 20.X
- ffmpeg static version : version N-55618-ga0acc44106-static https://johnvansickle.com/ffmpeg/


### Prerequisites:

- sudo apt update 
- sudo apt install pkg-config -y
- sudo apt-get install --no-install-recommends\
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
- exit


### FFMPEG Static Installation:

- wget https://johnvansickle.com/ffmpeg/builds/ffmpeg-git-amd64-static.tar.xz
- tar -xvf ffmpeg-git-amd64-static.tar.xz
- sudo mv ffmpeg-git-20210110-amd64-static/ffmpeg ffmpeg-git-20210110-amd64-static/ffprobe  /usr/local/bin/
- sudo mkdir /usr/local/share/model
- sudo mv  ffmpeg-git-20210110-amd64-static/model/* /usr/local/share/model/

### VMAF Instalation (Optional) - To use the c library directly:

- wget https://github.com/Netflix/vmaf/archive/v1.5.3.tar.gz
- tar -xf  v1.5.3.tar.gz
- cd vmaf-1.5.3/libvmaf/
- meson build --buildtype release
- ninja -vC build
- ninja -vC build test
- ninja -vC build install


### Examples:

*ffmpeg -i HBO_HD_RxSat27Oc2020_5min.ts -i HBO_HD_1080-5M-ref.ts -filter_complex "[0:v]select=gt(n\\,0),setpts=PTS-STARTPTS[main]; [1:v]select=gt(n\\,0),setpts=PTS-STARTPTS[ref]; [main][ref]libvmaf=psnr=1:log_path=prueba.json:log_fmt=json" -frames:v  100 -f null -*

*ffmpeg -i HBO_HD_RxSat27Oc2020_5min.ts -i HBO_HD_720-2.5M-ref.ts -filter_complex "[0:v]select=gt(n\\,0),setpts=PTS-STARTPTS[main]; [1:v]select=gt(n\\,1),setpts=PTS-STARTPTS,scale=1920x1080:flags=bicubic[ref]; [main][ref]libvmaf=psnr=1:log_path=prueba7200_1.json:log_fmt=json:n_threads=100" -frames:v 100 -f null -*


