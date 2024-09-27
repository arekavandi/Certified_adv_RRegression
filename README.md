# Certified Adversarial Robustness via Randomized $\alpha$-Smoothing for Regression Models

## Overview
This GitHub repository was made to present the results of certification of regression models against adversarial attack (Lp-Attack) using randomized smoothing and $\alpha$-trimming filter. Following the results/analyses in [RS-Reg](https://github.com/arekavandi/Certified_Robust_Regression), in this work, we show how the maximum adversarial perturbation of the input data can be derived for the base regression model, and then we show how a similar certificate can be extracted for the robust smoothing function adopted from the robust statistic literature, i.e., $\alpha$-trimming filter. We derive the minimum required trimming rate that is requiered to enhance the certification of the base model in the worst case performance setup.

This repository contains a Jupyter Notebook file for figures presented in the paper for a synthetic function as well as a Python script for the certification of camera re-localization task using RGB images using the code and model provided in [DSAC*](https://github.com/vislearn/dsacstar) repository.

We included all the files/models/datasets required to run the project and there is no need to download external files. 

## Installation
Synthetic simulation requires the following Python libraries/packages:
```
plotly (5.18.0)
matplotlib (3.8.2)
numpy (1.26.2)
scipy (1.11.4)
```
To run the Camera re-localization pipeline, all the packages suggested in  [DSAC*](https://github.com/vislearn/dsacstar) as well as the following packages repository should be installed:
```
scipy (1.11.4)
matplotlib (3.8.2)
```
The repository contains an ```environment.yml``` for the use with Conda. Perform the following steps:

1. Clone the repository:
```
git clone https://github.com/arekavandi/Certified_adv_RRegression.git
```
2. Go to the project folder and Make a new environment and install the required packages by
```
conda env create -f environment.yml
```


## Project Structure

The repository is organized as follows:

- **`notebooks/`:** Jupyter notebook for evaluating synthetic regression function.
- **`dsacstar/test_certificate.py`:** Python script for evaluating the robustness of camera re-localization model.
- **`dsacstar/datasets/`:** Contains the dataset used for evaluation. Download it [here](https://paperswithcode.com/dataset/cambridge-landmarks).
- **`dsacstar/newmodels/`:** Contains pre-trained models for the Cambridge landmarks dataset. Download them [here](https://heidata.uni-heidelberg.de/file.xhtml?persistentId=doi:10.11588/data/N07HKC/CBK0OL).

For extracting figures of synthetic function, please go to the `notebook/` directory, open `synthetic.ipynb` file, and run all the cells.

For running the camera re-localization code, please go to the `dsactstar/` directory in Anaconda Prompt and run:
```
python test_certificate.py <scene_name> <network_input_file> --n_tr <50-10K> --n_sample <10-1000> --alpha <0-0.5> --P <0-0.999> --n_test_image <10-max_test_image> --beta <0-2> --epsilon <0-infty> --K <0-infty>
```
As an example:
```
python test_certificate.py Cambridge_GreatCourt newmodels\rgb\cambridge\Cambridge_GreatCourt.net --n_tr 100 --n_sample 10 --alpha 0.35 --P 0.8 --n_test_image 760 --beta 0.5 --epsilon 5 --K 1.5 
```
## Main Idea
We aim to find the upper bound on the input perturbation (w.r.t. Lp norm) such that the output values of a regression model stay  with probability P within the accepted region defined by the user (see the below Figure).

<img width="962" alt="image" src="https://github.com/user-attachments/assets/d97c7548-ab4b-46ee-8b70-713fac465491">

Our certification flowchart:

<img width="962" alt="image" src="https://github.com/user-attachments/assets/148591cb-0c24-4ad9-a26b-173e4562a9d8">


## Experimental Results
We considered a mapping function $f:\mathbb{R}^2\rightarrow \mathbb{R}$ given by $f(\textbf{x})=10\sin(2x_1)+2(x_2-2)^3$. This function was investigated for the interval $(-1, 5)$ with $P=0.8$, $\sigma=0.15$, $\epsilon_y=6$ using $\ell_1$ norm, $n=10,000$ at two different rates of $\alpha=0.35$ and $\alpha=0.49$. The following Figure illustrates the derived bounds for the base regression model (blue) and smoothed regression model (green and red).

<img width="926" alt="image" src="https://github.com/user-attachments/assets/1e93214c-a16c-49d8-83d7-96bd1eab53f3">


For real data and camera positionig task, the input bound of the adversary norm for Great Court scene has been demonstrated below for each taken images as a point in the 3D scene. Brighter points show more robust pose estimation of the images.

<img width="612" alt="image" src="https://github.com/user-attachments/assets/b4f5541e-a622-477b-87fa-a1a17dc0736c">


# Citations
If you found this GitHub page helpful, please cite the following papers:
```
@article{rekavandi2024certified,
  title={Certified Adversarial Robustness via Randomized $\alpha$-Smoothing for Regression Models},
  author={Miri Rekavandi, Aref and Farokhi, Farhad and Ohrimenko, Olga and Rubinstein, Benjamin IP},
  journal={Advances in Neural Information Processing Systems},
  year={2024}
}
@article{rekavandi2024rs,
  title={RS-Reg: Probabilistic and Robust Certified Regression Through Randomized Smoothing},
  author={Miri Rekavandi, Aref and Ohrimenko, Olga and Rubinstein, Benjamin IP},
  journal={arXiv preprint arXiv:2405.08892},
  year={2024}
}
```
