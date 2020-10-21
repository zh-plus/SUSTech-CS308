# CV Lab5 Notes

TA: 郑浩 (RA in SUSTech CV Lab)

### Prerequisites

1. Python packages

   ```
   conda activate YOUR_ENV
   conda install scikit-image pillow numpy matplotlib
   ```

2. The Chinese Version of Notes can be retrieved in https://zhuanlan.zhihu.com/p/203292567

### Hough Transform

##### Hough Space in Cartesian Coordinates

A line can be determined using $A=(x_1, y_1), B=(x_2, y_2)$ in Cartesian coordinates.

<img src="https://pic2.zhimg.com/80/v2-0a8ff5fa59b5082f1e77a38b1c09982d_1440w.jpg" alt="img" style="zoom:125%;" />

in which $y=kx+q$ can be represented using $(k, q)$ in the parameter space:
$$
\begin{cases}
q& = -kx_1 + y _1\\
q& = -kx_2 + y _2\\
\end{cases}
$$
The transformation can be visualized:

<img src="https://pic4.zhimg.com/v2-92dff3e1b0f3aaa90b5e5bc82592d627_r.jpg" alt="preview" style="zoom:125%;" />

The transformed parameter space is **Hough Space**, in which a **line** in Cartesian coordinates can be represented as a **point** in Hough Space.

It also holds vice versa (a **point** in Cartesian coordinates can be represented as a **line** in Hough Space.):

<img src="https://pic3.zhimg.com/v2-adbd9d4761fcb9d9fd49a3dbb1bce696_r.jpg" alt="preview" style="zoom:125%;" />

If there're two points in Cartesian coordinates:

<img src="https://pic1.zhimg.com/v2-262e660a281b36ce0a60289479e9b738_r.jpg" alt="preview" style="zoom:125%;" />

If there're three **collinear** points in Cartesian coordinates:

<img src="https://pic1.zhimg.com/v2-7966de4cc1966a517aefa816dc6a80b8_r.jpg" alt="preview" style="zoom:125%;" />

If there're more than one coordinates with more points:

<img src="https://pic1.zhimg.com/v2-bab3a0f9416165a792d6d12b86773ed4_r.jpg" alt="preview" style="zoom:125%;" />

The lines can be determined using points that formed by most intersections in **Hough Space**:

<img src="https://pic1.zhimg.com/v2-ffef6c491efa60c5515d3315e086c528_r.jpg" alt="preview" style="zoom:125%;" />



##### Hough Space in Polar Coordinates using [Hesse normal form](https://en.wikipedia.org/wiki/Hesse_normal_form) (Not naive Polar Coordinates!)

In Polar Coordinates, the line can be represented using $(\rho, \theta)$:
$$
x \cdot cos\theta + y \cdot sin\theta = \rho
$$
<img src="C:\Users\10578\AppData\Roaming\Typora\typora-user-images\image-20201021175042972.png" alt="image-20201021175042972" style="zoom:125%;" />

Same as the Hough Space in Cartesian coordinates, a point in Polar Coordinates can be represented by a line in Hough Space:

<img src="https://pic2.zhimg.com/v2-434403a32e6626fec1484ddb6b03df21_r.jpg" alt="preview" style="zoom:125%;" />



The whole steps of detecting lines in image:

![Image for post](https://miro.medium.com/max/4800/1*pSAwZyau08leeYmTM9203Q.png)

### Reference

1. https://towardsdatascience.com/lines-detection-with-hough-transform-84020b3b1549
2. https://zhuanlan.zhihu.com/p/203292567
3. https://en.wikipedia.org/wiki/Hough_transform#:~:text=The%20Hough%20transform%20is%20a,shapes%20by%20a%20voting%20procedure.

