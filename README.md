# Slide Puzzle CAPTCHA Datasets

- Slide Puzzle CAPTCHA Datasets contain **Capy**, **Dingxiang**, **Geetest**, **Kaige**, **Shumei** and **Tencent**, and each CAPTCHA contains a **Notch Detection Dataset** and a **Slide Trajectory Dataset**.
- Download: https://pan.baidu.com/s/1L809SbAPSkm1z5htDf2o4Q (need request)
- Some examples are shown in this repositories.

## Notch Detection Datasets (ND-Datasets)

- Firstly, we use crawler programs to download different background images from six CAPTCHA websites (using MD5 to filter background images).
- Secondly, we manually annotate notch positions in the ND-Datasets. LabelImg is an open-source image annotation tool, and we use it to annotate the notch positions.

## Slide Trajectory Datasets (ST-Datasets)

We define the slide trajectory as follow: during the verification process of the slide puzzle CAPTCHA, from the moment the left mouse button is pressed to the moment the left mouse button is released, the slide path of the mouse on the two-dimensional space is the slide trajectory. For each type of CAPTCHA, we build a Slide Trajectory Dataset (ST-Dataset) by collecting the human slide trajectories that have passed the verification.

The method for collecting a human slide trajectory under time interval $\Delta t = 0.05s$ is as follows:

- After pressing the left mouse button, record the position of the mouse $\left[ {{x_0},{y_0}} \right]$ . Every $\Delta t$ later, record the mouse positions $\left[ {{x_i},{y_i}} \right]\left( {0 \le i \le k} \right)$.  Connecting the above mouse positions in sequence will form a mouse position list like $\left[ {\left[ {{x_0},{y_0}} \right],\left[ {{x_1},{y_1}} \right], \cdots ,\left[ {{x_k},{y_k}} \right]} \right]$.


- In the above mouse position list, subtract the horizontal and vertical coordinates of adjacent positions respectively to obtain the sub-trajectory within $\Delta t$, which is denoted as
  $\left[ {\Delta {x_i},\Delta {y_i}} \right]\left( {1 \le i \le k} \right)$ ($\Delta {x_i} = {x_i} - {x_{i - 1}}$,$\Delta {y_i} = {y_i} - {y_{i - 1}}$). Connecting all the sub-trajectories in sequence will result in a slide trajectory like $\left[ {\left[ {\Delta {x_1},\Delta {y_1}} \right],\left[ {\Delta {x_2},\Delta {y_2}} \right], \cdots ,\left[ {\Delta {x_k},\Delta {y_k}} \right]} \right]$ (where $k$ represents the trajectory length).

- Calculate the horizontal slide distance $\Delta x$ ($\Delta x = \sum\nolimits_{i = 1}^k {\Delta {x_i}}$) and the vertical slide distance $\Delta y$ ($\Delta y = \sum\nolimits_{i = 1}^k {\Delta {y_i}}$) of the slide trajectory $\left[ {\left[ {\Delta {x_1},\Delta {y_1}} \right],\left[ {\Delta {x_2},\Delta {y_2}} \right], \cdots ,\left[ {\Delta {x_k},\Delta {y_k}} \right]} \right]$. Combining the horizontal slide distance, the vertical slide distance, the slide trajectory and the slide time together, a trajectory data can be obtained.
