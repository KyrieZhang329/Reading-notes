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
\prescript{A}{B}{R}\quad\prescript{A}{}{P_{BORG}}
\end{pmatrix}
$$
其中 $\prescript{A}{}{P_{BORG}}$ 是确定位姿 **$B$** 的原点的位置矢量

在位姿的**图解表示法**中，表示矢量的箭头从**A**指向**B**，表示**B**相对于**A**的关系



## 映射：从一个坐标系到另一个坐标系的变换

### 坐标平移

假设空间中两个坐标系**{A}**与**{B}**的姿态相同，此时两者之间不同的只是**平移**，可以用矢量 **$\prescript{A}{}{P_{BORG}}$** 来表示**{B}**的原点位置相对于**{A}**的原点位置

一个位置在坐标系**{B}**中的表示为 $\prescript{B}{}{P}$ ，则可以使用矢量相加的方法求其在坐标系**{A}**中的表示 $\prescript{A}{}{P}$ ：
$$
\prescript{A}{}{P}=\prescript{B}{}{P}+\prescript{A}{}{P_{BORG}}\\
\text{p.s.  \quad只有在不同坐标系姿态相同时才可以使用这种办法相加}
$$
这就是一个简单的矢量在不同坐标系中的**映射**，称矢量 $\prescript{A}{}{P_{BORG}}$ 定义了这个映射

### 坐标旋转

用符号 $\prescript{A}{B}{R}$ 来表示**{B}**相对于**{A}**的$3\times3$的旋转矩阵，旋转矩阵各列的模**均为1**，且这些单位矢量均相互正交：
$$
\prescript{A}{B}{R}=\prescript{B}{A}{R^{-1}}=\prescript{B}{A}{R^{T}}
$$
在已知一个位置相对于**{B}**的定义 $\prescript{B}{}{P}$ ，现想求其相对于另一个与**{B}**原点重合的坐标系**{A}**的定义 $\prescript{A}{}{P}$ ，这个变换就可以由旋转矩阵 $\prescript{A}{B}{R}$ 来描述

注意到描述位置 $\prescript{A}{}{P}$ 的矢量的每个分量就是其向坐标系上单位矢量方向的投影，则可以由矢量点积来计算其分量：
$$
\prescript{A}{}{p_x}=\prescript{B}{}{\hat{X}_A}\;\cdot\prescript{B}{}{P}\\
\prescript{A}{}{p_y}=\prescript{B}{}{\hat{Y}_A}\;\cdot\prescript{B}{}{P}\\
\prescript{A}{}{p_z}=\prescript{B}{}{\hat{Z}_A}\;\cdot\prescript{B}{}{P}\\
$$
用旋转矩阵来表示：
$$
\prescript{A}{}{P}=\prescript{A}{B}{R}\prescript{B}{}{P}
$$
这即是一个矢量旋转变换的描述映射，可以看作该符号记法的前一个变量左下标消掉了后面变量的左上标

### 一般变换

在机器人学问题中，坐标的平移和旋转通常同时存在，这两个变换同时存在的映射即为一般变换

现已知确定坐标系**{B}**原点相对于坐标系**{A}**位置的矢量 $\prescript{A}{}{P_{BORG}}$ ，以及**{B}**相对于**{A}**的旋转矩阵 $\prescript{A}{B}{R}$

则**{B}**相对于**{A}**的变换可以表示为：
$$
\prescript{A}{}{P}=\prescript{A}{B}{R}\prescript{B}{}{P}+\prescript{A}{}{P_{BORG}}
$$
由此可以引入一个新的概念形式：
$$
\prescript{A}{}{P}=\prescript{A}{B}{T}\prescript{B}{}{P}
$$
代表用一个矩阵形式的算子直接表示从**{B}**到**{A}**的映射，相比较之前的表示更加简洁明确，该公式的具体形式为：
$$
\begin{pmatrix}
\prescript{A}{}{P}\\1
\end{pmatrix}=
\begin{pmatrix}
\prescript{A}{B}{R}&\prescript{A}{}{P_{BORG}}\\
0\;0\;0&1
\end{pmatrix}
\begin{pmatrix}
\prescript{B}{}{P}\\1
\end{pmatrix}
$$
其中 $\prescript{A}{B}{T}$ 称为**齐次变换矩阵**，可直接用于坐标系**{B}**到**{A}**的变换描述



## 算子：平移、旋转和变换

用于坐标系间点的映射的**通用数学表达式**称为**算子**

和“坐标映射”的区别在于：

- **映射**强调“同一个点在不同坐标系中的表示如何转换,强调坐标系的变换”
- **算子**强调“对一个矢量/点施加某种操作，在同一个坐标系中，得到新的矢量/点”

两者**数学形式可以相同**，但**物理解释不同**

------

### 平移算子

平移是指将空间中的一个点沿着某个已知方向移动一定距离

设在坐标系 **{A}** 中，一个点由位置矢量 $\prescript{A}{}{P_1}$ 表示，沿矢量 $\prescript{A}{}{Q}$ 平移后得到新点 $\prescript{A}{}{P_2}$ ，则有：
$$
\prescript{A}{}{P_2}=\prescript{A}{}{P_1}+\prescript{A}{}{Q}
$$
若把平移写成矩阵算子形式，则可记为：
$$
\prescript{A}{}{P_2}=D_Q(q)\prescript{A}{}{P_1}
$$
其中 $D_Q(q)$ 表示沿矢量 $Q$ 方向平移的算子，其齐次形式可写为：
$$
D_Q(q)=
\begin{pmatrix}
1&0&0&q_x\\
0&1&0&q_y\\
0&0&1&q_z\\
0&0&0&1
\end{pmatrix}
$$


其中 $q_x,q_y,q_z$ 是平移矢量 $Q$ 的三个分量，且
$$
q=\sqrt{q_x^2+q_y^2+q_z^2}
$$

### 旋转算子

旋转算子表示将一个矢量绕某一轴旋转一定角度，得到新的矢量

设点（或矢量） $\prescript{A}{}{P_1}$ 经旋转后得到 $\prescript{A}{}{P_2}$ ，则可写为：
$$
\prescript{A}{}{P_2}=R\prescript{A}{}{P_1}
$$
为了明确旋转轴与旋转角，通常记作：
$$
\prescript{A}{}{P_2}=R_K(\theta)\prescript{A}{}{P_1}
$$
其中：

- $K$ 表示旋转轴
- $\theta$ 表示绕该轴旋转的角度

若绕 $Z$ 轴旋转 $\theta$ ，对应的齐次旋转算子为：
$$
R_Z(\theta)=
\begin{pmatrix}
\cos\theta&-\sin\theta&0&0\\
\sin\theta&\cos\theta&0&0\\
0&0&1&0\\
0&0&0&1\
\end{pmatrix}
$$
若只考虑位置矢量的旋转，也可只取其左上角的 $3\times3$ 旋转矩阵：
$$
R_Z(\theta)=
\begin{pmatrix}
\cos\theta&-\sin\theta&0\\
\sin\theta&\cos\theta&0\\
0&0&1
\end{pmatrix}
$$
旋转算子同样只涉及**一个坐标系内的矢量变化**

------

### 变换算子

平移和旋转可以合并为一个统一的变换算子

设点 $\prescript{A}{}{P_1}$ 经过“先旋转、再平移”后得到 $\prescript{A}{}{P_2}$ ，则有：
$$
\prescript{A}{}{P_2}=T\prescript{A}{}{P_1}
$$
其中 $T$ 为齐次变换算子，一般形式为：
$$
T=
\begin{pmatrix}
R&Q\\
0&1
\end{pmatrix}
$$
展开写为：
$$
T=
\begin{pmatrix}
r_{11}&r_{12}&r_{13}&q_x\\
r_{21}&r_{22}&r_{23}&q_y\\
r_{31}&r_{32}&r_{33}&q_z\\
0&0&0&1
\end{pmatrix}
$$
于是其次坐标下有：
$$
 \begin{pmatrix} \prescript{A}{}{P_2}\\ 1 \end{pmatrix}=

\begin{pmatrix}
R&Q\\
0&1
\end{pmatrix}
\begin{pmatrix}
\prescript{A}{}{P_1}\\
1
\end{pmatrix}
$$


