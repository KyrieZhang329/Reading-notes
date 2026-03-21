# Chapter 2: 空间描述与变换



## 引言

位置与姿态是描述三维空间中物体的两个非常重要的特性，通过在空间中设置的**坐标系（位姿）**来描述

任一位姿都可以用作物体研究的参考坐标系，所以经常将**物体空间属性的描述**在不同坐标系中**变换**

**世界坐标系**：讨论任何问题均可参照这个坐标系，定义的位置和姿态都是参照世界坐标系或者由世界坐标系定义的笛卡尔坐标系



## 描述：位置、姿态与位姿

**描述**可用来确定一个操作系统处理的对象的特性 

**位置**、**姿态**均是描述，**位姿**是包含这两个描述的统一体

### 位置描述

建立坐标系后，可以用一个 $3\times1$ 的**位置矢量**来定位世界坐标系中的任何点，矢量上常附加一些信息来表明其定义在哪一个坐标系
$$
e.g.\qquad \prescript{A}{}{P}= 
\begin{pmatrix}
p_{x} \\
p_{y} \\
p_{z} \\
\end{pmatrix}
$$
可用于表示坐标系 **{A}** 下的一个位置（一个点），其中的元素数值是指点在坐标系轴线上的投影

### 姿态描述

我们可以**在物体上固定一个坐标系，并给出该坐标系相对于参考坐标系的描述**来描述姿态 

将坐标系**{A}**作为参考坐标系，坐标系**{B}**的主轴方向单位矢量可以写作$\prescript{A}{}{\hat{X}_{B}}\;、\prescript{A}{}{\hat{Y}_{B}}\;、\prescript{A}{}{\hat{X}_{Z}}$，可以很容易将这三个单位矢量排成一个$3\times3$的矩阵，称为**旋转矩阵**：
$$
\prescript{A}{B}{R}=(\prescript{A}{}{\hat{X}_{B}}\quad\prescript{A}{}{\hat{Y}_{B}}\quad\prescript{A}{}{\hat{Z}_{B}})=
\begin{pmatrix}
r_{11}\quad r_{12}\quad r_{13} \\
r_{21}\quad r_{22}\quad r_{23} \\
r_{31}\quad r_{32}\quad r_{33} \\
\end{pmatrix}
$$
其中，变量 $r_{ij}$ 可以用每个矢量在其参考坐标系中轴线方向上投影的分量来表示，于是每个 $r_{ij}$ 可以用一对单位矢量的点积来表示：
$$
\prescript{A}{B}{R}=(\prescript{A}{}{\hat{X}_{B}}\quad\prescript{A}{}{\hat{Y}_{B}}\quad\prescript{A}{}{\hat{X}_{Z}})=
\begin{pmatrix}
\hat{X}_B\cdot\hat{X}_{A}\quad \hat{Y}_B\cdot\hat{X}_{A}\quad \hat{Z}_B\cdot\hat{X}_{A} \\
\hat{X}_B\cdot\hat{Y}_{A}\quad \hat{Y}_B\cdot\hat{Y}_{A}\quad \hat{Z}_B\cdot\hat{Y}_{A} \\
\hat{X}_B\cdot\hat{Z}_{A}\quad \hat{Y}_B\cdot\hat{Z}_{A}\quad \hat{Z}_B\cdot\hat{Z}_{A} \\
\end{pmatrix}
$$
对于点积，只要各对矢量在同一坐标系中描述，左上标即可省略

两个单位矢量的点积可以得到二者夹角的余弦，所以旋转矩阵各分量常被称为**方向余弦**

同时，不难发现 $\prescript{A}{B}{R}$ 中每一行是坐标系**{A}**的单位矢量在坐标系**{B}**中的表达：
$$
\prescript{A}{B}{R}=(\prescript{A}{}{\hat{X}_{B}}\quad\prescript{A}{}{\hat{Y}_{B}}\quad\prescript{A}{}{\hat{X}_{Z}})=
\begin{pmatrix}
\prescript{A}{}{\hat{X}_{B}^T}\\
\prescript{A}{}{\hat{Y}_{B}^T}\\
\prescript{A}{}{\hat{Z}_{B}^T}
\end{pmatrix}
$$
因此，$\prescript{B}{A}{R}$ 可以由 $\prescript{A}{B}{R}$ 转置得到，且可以证明旋转矩阵的逆为其的转置：
$$
\prescript{A}{B}{R^T}\prescript{B}{A}{R}=\begin{pmatrix}
\prescript{A}{}{\hat{X}_{B}^T}\\
\prescript{A}{}{\hat{Y}_{B}^T}\\
\prescript{A}{}{\hat{Z}_{B}^T}
\end{pmatrix}
(\prescript{A}{}{\hat{X}_{B}}\quad\prescript{A}{}{\hat{Y}_{B}}\quad\prescript{A}{}{\hat{Z}_{B}})=E_3
$$
即**旋转矩阵是正交矩阵**

### 位姿描述

在机器人学中，位置和姿态通常成对出现，故称其组合为**位姿**，包含4个矢量

一个位姿可以等价地用一个位置矢量和一个旋转矩阵（3个矢量）来描述
$$
e.g.\qquad{B}=
\begin{pmatrix}
\prescript{A}{B}{R},\;\prescript{A}{}{P_{BORG}}
\end{pmatrix}
$$
其中 $\prescript{A}{}{P_{BORG}}$ 是确定位姿 **$B$** 的原点的位置矢量

在位姿的**图解表示法**中，表示矢量的箭头从**A**指向**B**，表示**B**相对于**A**的关系



## 映射：从一个坐标系到另一个坐标系的变换

