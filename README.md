# InNeRF360


> 'Text-Guided 3D-Consistent Object Inpainting on 360-degree Neural Radiance Fields' (CVPR 2024)

### [Project](https://ivrl.github.io/InNeRF360/) | [arXiv](https://arxiv.org/abs/2305.15094) 

Dongqing Wang, Tong Zhang, Alaa Abboud, Sabine Süsstrunk

[![DOI](https://zenodo.org/badge/777345232.svg)](https://zenodo.org/doi/10.5281/zenodo.11094775)

![Figure Abstract](/docs/static/images/banner.png)

>**Abstract:** We propose InNeRF360, an automatic system that accurately removes text-specified objects from 360-degree Neural Radiance Fields (NeRF). The challenge is to effectively remove objects while inpainting perceptually consistent content for the missing regions, which is particularly demanding for existing NeRF models due to their implicit volumetric representation. Moreover, unbounded scenes are more prone to floater artifacts in the inpainted region than frontal-facing scenes, as the change of object appearance and background across views is more sensitive to inaccurate segmentations and inconsistent inpainting. With a trained NeRF and a text description, our method efficiently removes specified objects and inpaints visually consistent content without artifacts. We apply depth-space warping to enforce consistency across multiview text-encoded segmentations, and then refine the inpainted NeRF model using perceptual priors and 3D diffusion-based geometric priors to ensure visual plausibility. Through extensive experiments in segmentation and inpainting on 360-degree and frontal-facing NeRFs, we show that our approach is effective and enhances NeRF's editability. 

If you find this project useful for your research, please cite: 

```
@InProceedings{wang2024innerf360,
    author={Wang, Dongqing and Zhang, Tong and Abboud, Alaa and S{\"u}sstrunk, Sabine},
    title     = {{InNeRF360: Text-Guided 3D-Consistent Object Inpainting on 360-degree Neural Radiance Fields}},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
    month     = {June},
    year      = {2024}
}
```


## Installation

1. Setup conda 

```bash
conda create --name innerf360 -y python=3.9
conda activate innerf360
python -m pip install --upgrade pip
```

2. Install [Nerfstudio and dependencies](https://docs.nerf.studio/en/latest/quickstart/installation.html).

```bash
cd nerfstudio
pip install -e .
pip install torch==1.13.1 torchvision functorch --extra-index-url https://download.pytorch.org/whl/cu117
pip install git+https://github.com/NVlabs/tiny-cuda-nn/#subdirectory=bindings/torch
```

3. Install binvox

```bash
mkdir bins
cd bins
wget -O binvox https://www.patrickmin.com/binvox/linux64/binvox?rnd=16811490753710
cd ../
chmod +x bins/binvox
```

4. Install InNeRF360

```bash
cd ../
git clone https://github.com/IVRL/InNeRF360.git
cd InNeRF360
```


## Project Organization

```
root
├── nerfstudio               # installation of NeRFStudio
└── InNeRF360                # github repo fils. Model details to be released!
    ├── data
        └── ShapeNetCore.v2  # ShapeNet data
    ├── data_modules
    ...
    └── bins
        └── binvox           # binvox to voxelize cubes
└── docs                     # website

```

## 3D diffusion model

Our geometric prior is trained on sampling cubes from ShapeNet meshes. To download the ShapeNet dataset, login or create an account at https://shapenet.org and then download the [ShapeNetCore.v2](https://shapenet.cs.stanford.edu/shapenet/obj-zip/ShapeNetCore.v2.zip) dataset.

We will release training details soon, in the meantime, we provide a trained [pretrained checkpoint](https://drive.google.com/file/d/1krt7xg0fujtRX_pXafQ8fDWFK9BoaeHq/view?usp=sharing) for our model. 

## Dataset Preparation

We perform our experiments on NeRFStudio datasets, which can be downloaded from the [website](https://docs.nerf.studio/quickstart/existing_dataset.html) as follows: 

```bash
ns-download-data nerfstudio --capture-name nerfstudio-dataset
```

## Inference

Our code is build upon NeRFbusters from a specific branch of the original NeRFStudio model. It is thus not feasible to use the default ``ns-viewer`` to inspect the trained results. 

For inspection and comparison purposes, we retrain our checkpoints to be compatible with default viewer, which can be found [here](https://drive.google.com/drive/folders/1UBS4qLOW1Cv70Lsvt9ZYL2Z7i-Oell5g?usp=sharing). 

## (TODO) Training

## Acknowledgement

This project is based on [Nerfstudio](https://docs.nerf.studio/) and [Nerfbusters](https://github.com/ethanweber/nerfbusters). We thank the incredible codebases of our brilliant prior works. 



