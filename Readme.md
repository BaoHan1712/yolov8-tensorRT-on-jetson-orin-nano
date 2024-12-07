<h2>Cách chạy yolov8 bằng GPU trên jetson orin nano</h2>

<h3>Yêu cầu là phải JETPACK 5x trở lên, Ở đây tôi đang chạy là JP5.1.3 và python 3.8</h3>

Trước khi chạy hãy cài jtop

`sudo apt update`

`sudo apt install python3-pip`

`sudo pip3 install -U jetson-stats`

`sudo reboot`

`jtop`

Bật Chế độ nguồn MAX

`sudo nvpmodel -m 0`

Bật Đồng hồ Jetson sẽ đảm bảo tất cả CPU, GPU Lõi được xung nhịp ở tần số tối đa của chúng.

`sudo jetson_clocks`

1 Cập nhật danh sách gói, cài đặt pip và nâng cấp lên mới nhất

`sudo apt update`

`sudo apt install python3-pip -y`

`pip3 install -U pip`

2 Cài đặt ultralytics Gói pip với các phụ thuộc của nó

`pip3 install ultralytics[export]`

3 Khởi động lại thiết bị

`sudo reboot`

4 Gỡ cài đặt hiện đang được cài đặt PyTorch và Torchvision

`pip3 uninstall torch torchvision`

<h4>Lý do ta xóa đi xong phải cài lại là :  2 gói này được cài đặt qua pip không tương thích để chạy trên nền tảng Jetson dựa trên kiến trúc ARM64. Do đó, chúng ta cần cài đặt thủ công</h4>

5 Cài đặt PyTorch 2.1.0 theo JP5.1.3

`sudo apt-get install -y libopenblas-base libopenmpi-dev`

`wget https://developer.download.nvidia.com/compute/redist/jp/v512/pytorch/torch-2.1.0a0+41361538.nv23.06-cp38-cp38-linux_aarch64.whl -O torch-2.1.0a0+41361538.nv23.06-cp38-cp38-linux_aarch64.whl`

`pip3 install torch-2.1.0a0+41361538.nv23.06-cp38-cp38-linux_aarch64.whl`

6 Cài đặt Torchvision v0.16.2 theo PyTorch v2.1.0

`sudo apt install -y libjpeg-dev zlib1g-dev`

`git clone https://github.com/pytorch/vision torchvision`

`cd torchvision`

`git checkout v0.16.2`

`python3 setup.py install --user`

7 Cài đặt onnx GPU

`wget https://nvidia.box.com/shared/static/zostg6agm00fb6t5uisw51qi6kpcuwzd.whl -O onnxruntime_gpu-1.17.0-cp38-cp38-linux_aarch64.whl`

`pip install onnxruntime_gpu-1.17.0-cp38-cp38-linux_aarch64.whl`

`pip install numpy==1.23.5`

Thế là xong phần cài đặt , tiếp theo tới phần chạy trên gpu

Mở terminal lên chạy

`yolo export model=yolov8n.pt format=engine` 

Lưu ý :

có thể custom 
___________________________________________________________________________________________________________________________

Hãy chắc chắn rằng đã cài đủ bước và đúng thư viện , đúng phiên bản , hay chạy bằng môi trường ảo để không bị xung đột thư viện ( Đây là lời khuyên)
