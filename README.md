**Photogrammetry and Gaussian Splatting Assignment Report**

**Author:** Shalom Pakhare
**ASU ID:** 1232608015

---

### Abstract

This report explores a two-stage 3D reconstruction process that combines traditional photogrammetry with a modern neural rendering technique called Gaussian Splatting. In Part A, a textured mesh model was built using 10 input images in Agisoft Metashape. These original views were compared with views generated using Gaussian Splatting, and evaluated using PSNR and SSIM. In Part B, 10 synthetic novel views were created using the same splatting model. These new images were added to the original set, and the complete 25-image dataset was used for a second round of reconstruction. The comparison between the two mesh models shows how neural view synthesis can enhance photogrammetric outputs in terms of surface coverage and reconstruction quality.

---

### Keywords

Photogrammetry, Gaussian Splatting, 3D Reconstruction, Agisoft Metashape, View Synthesis, PSNR, SSIM, Neural Rendering, Dense Cloud, Camera Pose Augmentation

---

### Objective

The main goal of this assignment is to compare the results of traditional image-based 3D reconstruction and a hybrid approach that includes generated views from Gaussian Splatting. We break it down into:

* **Part A**: Generate a dense and textured 3D mesh from 10 input images using Metashape. Then, evaluate how well Gaussian Splatting can reproduce the same views and compare them quantitatively.
* **Part B**: Generate 10 new views from the trained splatting model. Add them to the original dataset and re-run the photogrammetry pipeline. Then analyze whether this improves the reconstruction.

---

### Dataset

* **Name**: Agisoft\_Dataset
* **Images**: 10 PNG files (simulated lunar scene)
* **Resolution**: 1540 x 856 px approx.

---

### Tools Used

* **Agisoft Metashape Professional** (Demo Version)
* **Gaussian Splatting** (Inria, 2023 repo)
* **Python 3.10**, **OpenCV**, **NumPy**, **scikit-image**
* **GPU**: NVIDIA RTX 4060
* **OS**: Ubuntu 22.04

---

### Project Directory Structure

```text
├── 25viewsDataset
├── ApolloDataset
│   ├── apollo_1.png
│   ├── apollo_2.png
│   ├── apollo_3.png
│   ├── apollo_4.png
│   ├── apollo_5.png
│   ├── apollo_6.png
│   ├── apollo_7.png
│   ├── apollo_8.png
│   ├── apollo_9.png
│   ├── apollo_10.png
│   ├── apollo_11.png
│   ├── apollo_12.png
│   ├── apollo_13.png
│   ├── apollo_14.png
│   ├── apollo_15.png
│   ├── transforms_capture.json
│   ├── transforms_test.json
│   └── transforms_train.json
├── gaussian-splatting
│   ├── arguments
│   ├── assets
│   ├── convert.py
│   ├── environment.yml
│   ├── full_eval.py
│   ├── gaussian_renderer
│   ├── LICENSE.md
│   ├── lpipsPyTorch
│   ├── metrics.py
│   ├── output
│   ├── README.md
│   ├── render.py
│   ├── results.md
│   ├── scene
│   ├── SIBR_viewers
│   ├── submodules
│   ├── train.py
│   └── utils
├── gs_metrics
│   └── evaluate_psnr_ssim.py
├── mesh_metrics
│   └── compare_mesh_stats.py
└── Models
    ├── Model1.obj
    ├── model1.psx
    ├── Model2.obj
    └── model2.psx
```

### Part A: Photogrammetry and Neural Rendering Comparison

1. **Initial Setup**: All 10 images were imported into Metashape. A sparse cloud was generated using high-accuracy alignment.
2. **Dense Cloud & Mesh**: Dense cloud built with confidence estimation enabled. Mesh was created and textured using default parameters.
3. **Gaussian Splatting Rendering**: A model was trained using the 10 images. Original views were rendered from the model.
4. **Evaluation**: Rendered outputs were compared to the actual images using PSNR and SSIM.

#### Results Table (PSNR and SSIM sample)

![Screenshot from 2025-05-11 02-33-05](https://github.com/user-attachments/assets/f5fce99e-b57c-4106-b69d-76d050e3ba46)

Although the PSNR/SSIM scores are relatively low, this step confirms the process and gives a base for comparison.

---

### Part B: Augmenting with Novel Views

1. **View Synthesis**: Using Gaussian Splatting, we rendered 10 novel views from new camera positions.
2. **Combined Dataset**: We merged these with the original 15 images to form a 25-image set.
3. **Photogrammetry Run 2**: The same steps from Part A were repeated with this larger dataset.
4. **Results**: The new mesh had improved surface continuity and less missing geometry.

#### Comparison Table

![Screenshot from 2025-05-11 02-33-37](https://github.com/user-attachments/assets/840d8236-5878-413b-a814-e16248685d2e)

Despite fewer faces, the 25-view model covered more space and resolved occlusions better. This suggests that well-placed novel views improve scene understanding.

---

### Conclusion

This assignment demonstrated how traditional photogrammetry can be improved by using neural rendering to generate additional viewpoints. While Gaussian Splatting on its own had limitations due to dataset sparsity, using it to generate support views for photogrammetry proved effective. The final 25-image model outperformed the original in quality and coverage.

**Future Work**: A denser initial image set and wider viewing angles could allow better neural rendering. Exploring multi-view consistency in splatting and integrating with real-time SLAM could be valuable next steps.

---
