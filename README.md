<p align="center">
  <a href="https://www.uit.edu.vn/" title="Trường Đại học Công nghệ Thông tin" style="border: 5;">
    <img src="https://i.imgur.com/WmMnSRt.png" alt="Trường Đại học Công nghệ Thông tin | University of Information Technology">
  </a>
</p>

<!-- Title -->
<h1 align="center"><b>DS101.P11 - Thống kê và xác suất chuyên sâu</b></h1>

## BẢNG MỤC LỤC

- [ Giới thiệu môn học](#gioithieumonhoc)
- [ Giảng viên hướng dẫn](#giangvien)
- [ Thành viên nhóm](#thanhvien)

## GIỚI THIỆU MÔN HỌC

<a name="gioithieumonhoc"></a>

- **Tên môn học**: Thống kê và xác suất chuyên sâu
- **Mã môn học**: DS101.P11
- **Năm học**: 2024-2025

## GIẢNG VIÊN HƯỚNG DẪN

<a name="giangvien"></a>

- TS **Dương Ngọc Hảo**

## THÀNH VIÊN NHÓM

<a name="thanhvien"></a>
| STT | MSSV | Họ và Tên | Github | Email |
| ------ |:-------------:| ----------------------:|-----------------------------------------------------:|-------------------------:
| 1 | 22520914 | Nguyễn Hải Nam |[NamSee04](https://github.com/NamSee04) |22520914@gm.uit.edu.vn |
| 2 | 22520673 | Lê Hữu Khoa |[kevdn](https://github.com/kevdn) |22520673@gm.uit.edu.vn |




# RWR-GAE
Code for the paper ["Random Walk Regularized Graph Auto Encoder"](https://arxiv.org/pdf/1908.04003.pdf)


The base code is a PyTorch implementation of the Variational Graph Auto-Encoder model described in the paper:
T. N. Kipf, M. Welling, [Variational Graph Auto-Encoders](https://arxiv.org/abs/1611.07308), NIPS Workshop on Bayesian Deep Learning (2016)

The code in this repo is based on or refers to https://github.com/tkipf/gae, https://github.com/tkipf/pygcn and https://github.com/vmasrani/gae_in_pytorch.

### Requirements
- Python 3
- PyTorch 0.4 

### To train a model run the following command
```bash
cd gae
python train.py --model="gcn_ae" --dataset-str="cora" --dw=1 --epochs=200 --walk-length=5 --window-size=3 --number-walks=5 --lr_dw=0.01
```
- Supported models are "gcn_vae" and "gcn_ae"
- Supported datasets are "cora" and "citeseer"
- dw, whether to use regularization or not (0: no regularization, 1: yes)
- if dw = 0, then all the remaining params are useless
- refer to _gae/train.py_ for other program arguments 

### Results on CORA test set
Link Prediction results:

Model | AUC | AP
---|---|---
SC | 84.6 &pm; 0.01 | 88.5 &pm; 0.00
DW | 83.1 &pm; 0.01 | 85.0 &pm; 0.00
GAE  | 91.0 &pm; 0.02 | 92.0 &pm; 0.03
RWR-GAE  | **92.9 &pm; 0.3**  | **92.7 &pm; 0.5**


Clustering results:

Model | Acc | NMI | F1 | Precision | ARI
---|---|---|---|---|---
SC | 0.367 | 0.127 | 0.318 | 0.193 | 0.031
DW | 0.484 | 0.327 | 0.392 | 0.361 | 0.243
GAE | 0.596 | 0.429 | 0.595 | 0.596 | 0.347
RWR-GAE | **0.669** | **0.481**| **0.618** | **0.629** | **0.417**

### Results on Pubmed test set
Link Prediction results:

Model | AUC | AP
---|---|---
SC | 84.2 &pm; 0.02 | 87.8 &pm; 0.01
DW | 84.4 &pm; 0.00 | 84.1 &pm; 0.00
GAE | 96.4 &pm; 0.00 | 96.5 &pm; 0.00
RWR-GAE | 96.2 &pm; 0.1 | 96.3 &pm; 0.09


Clustering results:

Model | Acc | NMI | F1 | Precision | ARI
---|---|---|---|---|---
GAE | 0.697 | 0.33 | 0.69 | 0.72 | 0.322
RWR-GAE | **0.726** | **0.355** | **0.714** | **0.729** | **0.37**

Runs in 2-3 mins for cora dataset on cpu. The code currently doesn't support GPU.
