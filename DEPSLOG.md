# Dependencies Logs

- [https://github.com/deepinsight/insightface](State-of-the-art 2D and 3D Face Analysis Project insightface.ai)
    ```shell
    REMOTE_NAME="deepinsight.insightface"
    UPSTREAM_BRANCH="master"
    git remote add "${REMOTE_NAME}" "https://github.com/deepinsight/insightface.git"
    git fetch "${REMOTE_NAME}" "${UPSTREAM_BRANCH}"
    git push origin FETCH_HEAD:refs/heads/"${REMOTE_NAME}#${UPSTREAM_BRANCH}"
    ```
- [https://github.com/davisking/dlib-models](Trained model files for dlib example programs.). Use shape_predictor_68_face_landmarks here.
    ```shell
    REMOTE_NAME="davisking.dlib-models"
    UPSTREAM_BRANCH="master"
    git remote add "${REMOTE_NAME}" "https://github.com/davisking/dlib-models.git"
    git fetch "${REMOTE_NAME}" "${UPSTREAM_BRANCH}"
    git push origin FETCH_HEAD:refs/heads/"${REMOTE_NAME}#${UPSTREAM_BRANCH}"
    ```
- [https://github.com/cubiq/ComfyUI_Essentials](Essential nodes that are weirdly missing from ComfyUI core.)
    ```shell
    REMOTE_NAME="cubiq.ComfyUI_Essentials"
    UPSTREAM_BRANCH="main"
    git remote add "${REMOTE_NAME}" "https://github.com/cubiq/ComfyUI_Essentials.git"
    git fetch "${REMOTE_NAME}" "${UPSTREAM_BRANCH}"
    git push origin FETCH_HEAD:refs/heads/"${REMOTE_NAME}#${UPSTREAM_BRANCH}"
    ```
- [https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite](Nodes related to video workflows)
    ```shell
    REMOTE_NAME="Kosinkadink.ComfyUI-VideoHelperSuite"
    UPSTREAM_BRANCH="main"
    git remote add "${REMOTE_NAME}" "https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite.git"
    git fetch "${REMOTE_NAME}" "${UPSTREAM_BRANCH}"
    git push origin FETCH_HEAD:refs/heads/"${REMOTE_NAME}#${UPSTREAM_BRANCH}"
    ```
- [https://github.com/kijai/ComfyUI-KJNodes](Various custom nodes for ComfyUI)
    ```shell
    REMOTE_NAME="kijai.ComfyUI-KJNodes"
    UPSTREAM_BRANCH="main"
    git remote add "${REMOTE_NAME}" "https://github.com/kijai/ComfyUI-KJNodes.git"
    git fetch "${REMOTE_NAME}" "${UPSTREAM_BRANCH}"
    git push origin FETCH_HEAD:refs/heads/"${REMOTE_NAME}#${UPSTREAM_BRANCH}"
    ```
- [https://github.com/kijai/ComfyUI-LivePortraitKJ](ComfyUI nodes for LivePortrait)
    ```shell
    REMOTE_NAME="kijai.ComfyUI-LivePortraitKJ"
    UPSTREAM_BRANCH="main"
    git remote add "${REMOTE_NAME}" "https://github.com/kijai/ComfyUI-LivePortraitKJ.git"
    git fetch "${REMOTE_NAME}" "${UPSTREAM_BRANCH}"
    git push origin FETCH_HEAD:refs/heads/"${REMOTE_NAME}#${UPSTREAM_BRANCH}"
    ```
- [https://github.com/pythongosssss/ComfyUI-Custom-Scripts](Enhancements & experiments for ComfyUI, mostly focusing on UI features)
    ```shell
    REMOTE_NAME="pythongosssss.ComfyUI-Custom-Scripts"
    UPSTREAM_BRANCH="main"
    git remote add "${REMOTE_NAME}" "https://github.com/pythongosssss/ComfyUI-Custom-Scripts.git"
    git fetch "${REMOTE_NAME}" "${UPSTREAM_BRANCH}"
    git push origin FETCH_HEAD:refs/heads/"${REMOTE_NAME}#${UPSTREAM_BRANCH}"
    ```
- [https://github.com/Comfy-Org/ComfyUI](The most powerful and modular diffusion model GUI, api and backend with a graph/nodes interface.)
    ```shell
    REMOTE_NAME="Comfy-Org.ComfyUI"
    UPSTREAM_BRANCH="main"
    git remote add "${REMOTE_NAME}" "https://github.com/Comfy-Org/ComfyUI.git"
    git fetch "${REMOTE_NAME}" "${UPSTREAM_BRANCH}"
    git push origin FETCH_HEAD:refs/heads/"${REMOTE_NAME}#${UPSTREAM_BRANCH}"
    ```
