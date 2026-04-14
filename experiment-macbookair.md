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

docker run -it --name liveportrait-cpu \
  --publish 8188:8188 \
  --volume $(pwd)/ComfyUI/models:/app/models \
  --volume $(pwd)/ComfyUI/input:/app/input \
  --volume $(pwd)/ComfyUI/output:/app/output \
  --entrypoint /bin/sh \
  python:3.10-slim
```

- `--device /dev/video0:/dev/video0`
- `--device /dev/video2:/dev/video2`

## Inside Container

```shell
apt-get install --yes \
    git \
    libgl1 \
    libglib2.0-0 \
    ffmpeg

pip install --no-cache-dir torch torchvision torchaudio

cd /app
git init . && git remote add origin https://github.com/comfyanonymous/ComfyUI.git
git fetch --depth 1 origin a2840e75520b7dc40958866b3c4da1345d5cfa9c && git checkout FETCH_HEAD
pip install --no-cache-dir --requirement requirements.txt

mkdir /app/custom_nodes/ComfyUI-Custom-Scripts && cd /app/custom_nodes/ComfyUI-Custom-Scripts
git init . && git remote add origin https://github.com/pythongosssss/ComfyUI-Custom-Scripts.git
git fetch --depth 1 origin 609f3afaa74b2f88ef9ce8d939626065e3247469 && git checkout FETCH_HEAD
cd ../../

mkdir /app/custom_nodes/ComfyUI-LivePortraitKJ && cd /app/custom_nodes/ComfyUI-LivePortraitKJ
git init . && git remote add origin https://github.com/kijai/ComfyUI-LivePortraitKJ.git
git fetch --depth 1 origin 4d9dc6205b793ffd0fb319816136d9b8c0dbfdff && git checkout FETCH_HEAD
pip install --no-cache-dir --requirement requirements-mac.txt
cd ../../

cd /app/custom_nodes
git clone --depth 1 https://github.com/kijai/ComfyUI-KJNodes.git
cd ComfyUI-KJNodes
pip install --no-cache-dir --requirement requirements.txt

cd /app/custom_nodes
git clone --depth 1 https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite.git
cd ComfyUI-VideoHelperSuite
pip install --no-cache-dir --requirement requirements.txt

cd /app/custom_nodes
git clone --depth 1 https://github.com/cubiq/ComfyUI_Essentials.git
cd ComfyUI_Essentials
pip install --no-cache-dir --requirement requirements.txt

(cd /app && python3 main.py --listen 0.0.0.0 --lowvram)
