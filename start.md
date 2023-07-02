## docker build
```
docker build -t="registry.cn-hangzhou.aliyuncs.com/kaithen/colmap:latest" .
```

```
# start docker
xhost +local
```

## build
```
cd build
cmake .. -GNinja -DCMAKE_CUDA_ARCHITECTURES=75 && \
ninja && \
ninja install
```

## run gui
```
PWD=`pwd`
docker run \
    -e QT_XCB_GL_INTEGRATION=xcb_egl \
    -e DISPLAY=${DISPLAY} \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -v ${PWD}:/colmap \
    -v /media/work:/media/work: \
    --gpus all \
    --privileged \
    --rm \
    -it registry.cn-hangzhou.aliyuncs.com/kaithen/colmap:latest \
    colmap gui
```