https://liveportrait.github.io

## On Host

```shell
mkdir -p ComfyUI/models/liveportrait
cd ComfyUI/models/liveportrait
wget https://huggingface.co/Kijai/LivePortrait_safetensors/resolve/main/appearance_feature_extractor.safetensors
wget https://huggingface.co/Kijai/LivePortrait_safetensors/resolve/main/motion_extractor.safetensors
wget https://huggingface.co/Kijai/LivePortrait_safetensors/resolve/main/warping_module.safetensors
wget https://huggingface.co/Kijai/LivePortrait_safetensors/resolve/main/spade_generator.safetensors
wget https://huggingface.co/Kijai/LivePortrait_safetensors/resolve/main/stitching_retargeting_module.safetensors
wget https://huggingface.co/Kijai/LivePortrait_safetensors/resolve/main/landmark.onnx
cd ../../../

mkdir -p ComfyUI/models/liveportrait/animal
cd ComfyUI/models/liveportrait/animal
wget https://huggingface.co/Kijai/LivePortrait_safetensors/blob/main/animal/appearance_feature_extractor.safetensors
wget https://huggingface.co/Kijai/LivePortrait_safetensors/blob/main/animal/motion_extractor.safetensors
wget https://huggingface.co/Kijai/LivePortrait_safetensors/blob/main/animal/spade_generator.safetensors
wget https://huggingface.co/Kijai/LivePortrait_safetensors/blob/main/animal/stitching_retargeting_module.safetensors
wget https://huggingface.co/Kijai/LivePortrait_safetensors/blob/main/animal/warping_module.safetensors
cd ../../.././

mkdir -p ComfyUI/models/insightface/models
cd ComfyUI/models/insightface/models
wget https://github.com/deepinsight/insightface/releases/download/v0.7/buffalo_l.zip
unzip buffalo_l.zip
rm buffalo_l.zip
cd ../../../../

mkdir -p ComfyUI/models/landmarks
cd ComfyUI/models/landmarks
wget https://github.com/davisking/dlib-models/raw/master/shape_predictor_68_face_landmarks.dat.bz2
bunzip2 shape_predictor_68_face_landmarks.dat.bz2
cd ../../../

mkdir -p ComfyUI/models/checkpoints
cd ComfyUI/models/checkpoints
wget -O v1-5-pruned-emaonly-fp16.safetensors "https://civitai.com/api/download/models/128713?type=Model&format=SafeTensor&size=pruned&fp=fp16"
cd ../../../

docker run -it --name liveportrait-gpu \
  --gpus all \
  --shm-size=2gb \
  --publish 8188:8188 \
  --volume $(pwd)/ComfyUI/models:/app/models \
  --volume $(pwd)/ComfyUI/input:/app/input \
  --volume $(pwd)/ComfyUI/output:/app/output \
  --entrypoint /bin/bash \
  pytorch/pytorch:2.11.0-cuda12.6-cudnn9-runtime
```

- `--device /dev/video0:/dev/video0`
- `--device /dev/video2:/dev/video2`

## Inside Container

```shell
# Check your card cuda capability for support by current PyTorch
#   GeForce GTX 1050 Ti <- cuda12.6
python3 -c "import torch; torch.ones(1).cuda(); print('Success! GPU is calculating.')" # Expected: Success! GPU is calculating.

python3 -c "import torch; print(torch.__version__)" # Expected like: 2.11.0+cu126

apt-get update && apt-get install -y build-essential git libgl1 wget libglib2.0-0

cd /app
git init . && git remote add origin https://github.com/comfyanonymous/ComfyUI.git
git fetch --depth 1 origin a2840e75520b7dc40958866b3c4da1345d5cfa9c && git checkout FETCH_HEAD
pip install --no-cache-dir --break-system-packages --requirement requirements.txt

mkdir /app/custom_nodes/ComfyUI-Custom-Scripts && cd /app/custom_nodes/ComfyUI-Custom-Scripts
git init . && git remote add origin https://github.com/pythongosssss/ComfyUI-Custom-Scripts.git
git fetch --depth 1 origin 609f3afaa74b2f88ef9ce8d939626065e3247469 && git checkout FETCH_HEAD
cd ../../

mkdir /app/custom_nodes/ComfyUI-LivePortraitKJ && cd /app/custom_nodes/ComfyUI-LivePortraitKJ
git init . && git remote add origin https://github.com/kijai/ComfyUI-LivePortraitKJ.git
git fetch --depth 1 origin 4d9dc6205b793ffd0fb319816136d9b8c0dbfdff && git checkout FETCH_HEAD
pip install --no-cache-dir --break-system-packages --requirement requirements.txt
cd ../../

mkdir /app/custom_nodes/ComfyUI-KJNodes && cd /app/custom_nodes/ComfyUI-KJNodes
git init . && git remote add origin https://github.com/kijai/ComfyUI-KJNodes.git
git fetch --depth 1 origin 068d4fee62d379723dd96dd3e768ed807f7d7135 && git checkout FETCH_HEAD
pip install --no-cache-dir --break-system-packages --requirement requirements.txt
cd ../../

mkdir /app/custom_nodes/ComfyUI-VideoHelperSuite && cd /app/custom_nodes/ComfyUI-VideoHelperSuite
git init . && git remote add origin https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite.git
git fetch --depth 1 origin 2984ec4c4b93292421888f38db74a5e8802a8ff8 && git checkout FETCH_HEAD
pip install --no-cache-dir --break-system-packages --requirement requirements.txt
cd ../../

mkdir /app/custom_nodes/ComfyUI_Essentials && cd /app/custom_nodes/ComfyUI_Essentials
git init . && git remote add origin https://github.com/cubiq/ComfyUI_Essentials.git
git fetch --depth 1 origin 9d9f4bedfc9f0321c19faf71855e228c93bd0dc9 && git checkout FETCH_HEAD
pip install --no-cache-dir --break-system-packages --requirement requirements.txt
cd ../../

python3 -c "import onnxruntime as ort; print('Available Providers:', ort.get_available_providers())" # Expected: 'TensorrtExecutionProvider' and 'CUDAExecutionProvider'

pip install --upgrade --no-cache-dir --break-system-packages mediapipe==0.10.13
pip install --no-cache-dir --break-system-packages insightface

# For GTX 1050 Ti add `--lowvram`
(cd /app && python3 main.py --listen 0.0.0.0)
```
