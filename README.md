# SLTNet: Efficient Event-based Semantic Segmentation with Spike-driven Lightweight Transformer-based Networks

This repository is an official PyTorch implementation of our recent work: **SLTNet**([PDF](https://arxiv.org/pdf/2412.12843)), which was submitted to **2025 IEEE International Conference on Robotics and Automation (ICRA)**, titled "Efficient Event-based Semantic Segmentation with Spike-driven Lightweight Transformer-based Networks".

* **Spiking Lightweight Dilated module**:  reduce the model parameters while maintaining efficient feature extraction ability; capture multi-scale event features while adapting to SNN architectures.
* **novel Spike-driven Lightweight Transformer-based segmentation network**: A network with events only to deal with high-dynamic complex scenarios, constructed on the basic SCBs and STBs that enable high-efficiency feature extraction and low computational cost.
* **Spike-driven Transformer Blocks**: leveraging the re-parameterization convolution technique and spike-driven multi-head self-attention mechanism to achieve long-range contextural feature interaction with only floating-point accumulation operations.

## Updates
   - The article has been submitted to the **IEEE ICRA 2025**. (Sep/15/2024)
   - Our paper was submitted to Arxiv for public access. (Dec/18/2024)
   - The training and testing codes and trained models for SLTNet are available here. (Dec/20/2024)


## Models
The finetuned models on DDD17 and DSEC-Semantic are available for direct application in road scene parsing.

| Model | Dataset | Val (% mIOU) | Params (M) | FLOPs (G) | FPS |
|:-:|:-:|:-:|:-:|:-:|:-:|
| SLTNet |DDD17 | [51.93](https://drive.google.com/file/d/1gsZ-ykM9-jMwf9UE7Adj4eLRhiaw98Fy/view?usp=drive_link) | 0.41 | 1.96 | 114.29 |

| Model |Dataset  | Val (% mIOU) | Params (M) | FLOPs (G) | FPS |
|:-:|:-:|:-:|:-:|:-:|:-:|
| SLTNet |DSEC-Semantic | [47.91](https://drive.google.com/file/d/1o5FPX1ACfRNL7WNKEkPlAhBnaUnPpKWp/view?usp=drive_link)| 1.67 | 6.97 | 114.29 |


## Installation

```
cuda == 10.2
Python == 3.6.4
Pytorch == 1.8.0+cu101
```

## Train

## Usage

### 0. Prepare the dataset
# DDD17 Dataset
The original DDD17 dataset with semantic segmentation labels can be downloaded here[https://github.com/Shathe/Ev-SegNet]. Additionally, the pre-processed DDD17 dataset with semantic labels is provided here[https://download.ifi.uzh.ch/rpg/ESS/ddd17_seg.tar.gz]. Please do not forget to cite DDD17 and Ev-SegNet if you are using the DDD17 with semantic labels.

# DSEC-Semantic Dataset
The DSEC-Semantic dataset can be downloaded here[https://dsec.ifi.uzh.ch/dsec-semantic/]. The dataset should have the following format:

├── DSEC_Semantic                 
│   ├── train                 
│   │   ├── zurich_city_00_a   
│   │   │   ├── semantic  
│   │   │   │   ├── left  
│   │   │   │   │   ├── 11classes  
│   │   │   │   │   │   └──data  
│   │   │   │   │   │       ├── 000000.png  
│   │   │   │   │   │       └── ...  
│   │   │   │   │   └── 19classes  
│   │   │   │   │       └──data  
│   │   │   │   │           ├── 000000.png  
│   │   │   │   │           └── ...  
│   │   │   │   └── timestamps.txt  
│   │   │   └── events    
│   │   │       └── left  
│   │   │           ├── events.h5  
│   │   │           └── rectify_map.h5  
│   │   └── ...  
│   └── test  
│       ├── zurich_city_13_a  
│       │   └── ...  
│       └── ... 

* Remember to replace the dataset path in the YAML with your true dataset path


### 1. Training
* For example, train the SLTNet on DDD17 with a batch size of 32 on 1 GPU:
````bash
python train.py --dataset DDD17_events --input_size 200,346 --classes 6 --dataset_path your_path
````
* Or train the SLTNet on DSEC with a batch size of 32 on 1 GPU:
````bash
python train.py --dataset DSEC_events --input_size 480,640 --classes 11 --dataset_path your_path
````


### 2. Evaluation

* Download the finetuned models for DDD17 and DSEC-Semantic and put them into `checkpoint/DDD17/` and `checkpoint/DSEC/` dirs, respectively.
* For example, evaluate the SLTNet on the DDD17 val set:
````bash
python test.py --dataset DDD17_events --input_size 200,346 --dataset_path your_path --checkpoint ./pretrained_models/DDD17/SLTNet_DDD17_Test.pth
````
* Or, evaluate the SLTNet on the DSEC-Semantic val set:
````bash
python test.py --dataset DSEC_events --input_size 480,640 --dataset_path your_path --checkpoint ./pretrained_models/DSEC/SLTNet_DSEC_Test.pth
````


## Citation

If you think this implementation is useful for your work, please cite our paper:
```
@misc{zhu2024efficienteventbasedsemanticsegmentation,
      title={Efficient Event-based Semantic Segmentation with Spike-driven Lightweight Transformer-based Networks}, 
      author={Xiaxin Zhu and Fangming Guo and Xianlei Long and Qingyi Gu and Chao Chen and Fuqiang Gu},
      year={2024},
      eprint={2412.12843},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2412.12843}, 
}
```

## Thanks && Refer

```bash
@misc{Efficient-Segmentation-Networks,
  author = {Yu Wang},
  title = {Efficient-Segmentation-Networks Pytorch Implementation},
  year = {2019},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/xiaoyufenfei/Efficient-Segmentation-Networks}},
  commit = {master}
}
```

