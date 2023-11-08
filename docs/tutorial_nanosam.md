# Tutorial - NanoSAM

Let's run NVIDIA's [NanoSAM](https://github.com/NVIDIA-AI-IOT/nanosam) to check out the performance gain by distillation.

![](https://raw.githubusercontent.com/NVIDIA-AI-IOT/nanosam/main/assets/basic_usage_out.jpg)

!!! abstract "What you need"

    1. One of the following Jetson:

        <span class="blobDarkGreen4">Jetson AGX Orin 64GB</span>
        <span class="blobDarkGreen5">Jetson AGX Orin (32GB)</span>
        <span class="blobLightGreen4">Jetson Orin Nano Orin (8GB)</span>

    2. Running one of the following [JetPack.5x](https://developer.nvidia.com/embedded/jetpack)

        <span class="blobPink1">JetPack 5.1.2 (L4T r35.4.1)</span>
        <span class="blobPink2">JetPack 5.1.1 (L4T r35.3.1)</span>
        <span class="blobPink3">JetPack 5.1 (L4T r35.2.1)</span>

    3. Sufficient storage space (preferably with NVMe SSD).

        - `6.3GB` for container image
        - Spaces for models

## Set up a container for `nanosam`

### Clone `jetson-containers`

!!! tip ""

    See [`jetson-containers`' `nanosam` package README](https://github.com/dusty-nv/jetson-containers/tree/master/packages/vit/nanosam) for more infomation**

```
git clone https://github.com/dusty-nv/jetson-containers
cd jetson-containers
sudo apt update; sudo apt install -y python3-pip
pip3 install -r requirements.txt
```

## How to start

Use `run.sh` and `autotag` script to automatically pull or build a compatible container image.

```
cd jetson-containers
./run.sh $(./autotag nanosam)
```

## Run examples

Inside the container, you can move to `/opt/nanosam` directory, to go through all the examples demonstrated on the repo.

```
cd /opt/nanosam
```

To run the "[**Example 1 - Segment with bounding box**](https://github.com/NVIDIA-AI-IOT/nanosam#example-1---segment-with-bounding-box)":

```
python3 examples/basic_usage.py \
    --image_encoder="data/resnet18_image_encoder.engine" \
    --mask_decoder="data/mobile_sam_mask_decoder.engine"
```

The result is saved under `/opt/nanosam/data/basic_usage_out.jpg`.

To check on your host machine, you can copy that into `/data` directory of the container where that is mounted from the host.

```
cp data/basic_usage_out.jpg /data/
```

Then you can go to your host system, and find the file under the `jetson_containers`' `data` directory, like `jetson_containers/data/basic_usage_out.jpg`.

## Results

![](https://raw.githubusercontent.com/NVIDIA-AI-IOT/nanosam/main/assets/basic_usage_out.jpg)