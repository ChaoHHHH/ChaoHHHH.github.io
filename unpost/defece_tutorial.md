---
math: true
---
## 点缺陷能级
![DefectLevel](./defect_tutorial_figs/defect_level.png)

缺陷能级按照其在带隙中的位置可以分为浅能级（靠近带边）和深能级（原理带边），其中深能级可以作为复合中心，俘获电子或者空穴。从波函数的角度讲，浅能级的波函数一般比较离域，即波函数弥漫在缺陷附近的大片空间，深能级的波函数则十分局域，一般就在只在缺陷附近。

![DefectWF](./defect_tutorial_figs/defectWF.png)

上面就是两者典型的区别，左侧深能级的结构是96个原子的胞，缺陷能级的波函数只在局限在一个小范围内，右侧是一个数千原子的胞，浅能级缺陷的波函数几乎覆盖了整个胞。因此相对而言，对于DFT计算而言，深能级缺陷比较好研究。
## 点缺陷分类
有本征缺陷包括空位、反位、间隙。外来杂质缺陷包括替位、间隙。也有一些更复杂的点缺陷形式，点缺陷计算普遍使用超胞法（建立一个尽可能大的晶胞，在这个晶胞中制造一个点缺陷）

## 缺陷形成能与缺陷转变能级
缺陷形成能，顾名思义就是指形成一个缺陷所需的能量，实际计算中采用下面的公式

$$E(X) = E_{total}(X) − E_{bulk} + ∑_{i} n_{i}μ_{i} + qE_{F} + E_{corr}$$

$E_{total}(X)$ 代表缺陷体系的总能，$E_{bulk}$代表无缺陷bulk体系总能，$μ_{i}$代表原子化学势，单个原子的化学势通过依赖于具体的生长环境，通常是一个能量范围，在实际画图中通常取化学势的最大值或最小值，对应于缺陷能级图中的rich或者poor的情况。$q$表示体系带电量，$E_{F}=\varepsilon+E_{VBM}$代表外部电子化学势，$E_{corr}$则表示有限尺寸和镜像电荷的能量修正。需要注意的是，这里的缺陷体系通常需要扩为足够大的方胞。

>一个粗糙的说明，缺陷形成能表示形成一个缺陷所需的能量，以氧空位缺陷的形成为例，其中前两项能量之差表示把缺陷和完美晶体（Bulk）分离所需的能量（体系能量升高），以及这之后体系需要重新驰豫，会放出一部分能量（补偿），接着单个缺陷需要重新融入环境中（单个O原子不可能独立存在，会以氧气分子，或者水分子等各种化合的状态存在，这就是化学势项，这一步同样会释放一部分能量，作为补偿项），此外，如果缺陷需要带电，需要从外界获取一个电子/释放出一个电子，获取电子的能量是费米能，会导致体系能量升高/降低，这一项只是从外界电子库获取/放入电子所需的能量，驰豫后的补偿在前两项中就被计算了。最后一项为DFT计算的修正项。

![defectEnergy](./defect_tutorial_figs/defeceEnergy.png)

一个典型的结果如图所示，缺陷形成能最终会是 $q$ 的函数，而转变能级则对应着不同电荷态的缺陷形成能的交点，在转变能级处，缺陷可以在两种电荷态之间相互转换。

形成能用来判断一个缺陷在热力学上的性质，即这个缺陷的稳定性，以及缺陷的浓度。转变能级则用来判断缺陷的电学性质

The experimental significance of this level is that for Fermi-level positions below $\varepsilon(q_{1}/q_{2})$, charge state $q_{1}$ is stable, while for Fermi-level positions above $\varepsilon(q_{1}/q_{2})$, charge state $q_{2}$ is stable.

Transition levels correspond to thermal ionization energies. Conventionally, if a transition level is positioned such that the defect is likely to be thermally ionized at room temperature (or at device operating temperatures), this transition level is called a shallow level; if it is unlikely to be ionized at room temperature, it is called a deep level.

讲两个点：

In principle, internal excitations of the defect can occur in which the charge state of the defect remains unchanged. More commonly, however, carriers are exchanged with the semiconductor host and a transition to a different charge state occurs.

这是说，缺陷的状态改变有两种情况，一种是缺陷内部本身的电子发生一个能级的改变，但是整个缺陷的带电量不会发生改变，类似于一个分子中的电子发生跃迁换了一个能级，但是整个分子依旧是中性的。另一种也就是我们此处讨论的情况，即缺陷从外界背景中（semiconductor host）中获取了一个电子/空穴，使得缺陷的电荷状态发生改变。

These different charge states may correspond to quite different local lattice configurations. It is important to realize that the Kohn-Sham (KS) levels that result from a bandstructure calculation for the center cannot directly be identified with any levels that are relevant for experiment, even if there were no concerns about the accuracy of the KS band gap. Instead, the total energies of the defect configurations before and after the transition must be considered.

电荷态的改变会同时改变晶格结构（电子-声子耦合），我们虽然可以从K-S的结果中读到缺陷能级的位置，但是这个数据不能直接用来与实验结果做比对，必须考虑缺陷电荷态改变对结构造成的影响

Ref. Freysoldt, C. et al. First-principles calculations for point defects in solids. Rev. Mod. Phys. 86, 253–305 (2014).

## 原子化学势
如上所述，这里的化学势实际上是单质化合后所释放的能量，所以对于不同的化合物，计算出的原子的化学势并不一致，取决于实际的制备条件

>ToDo 详细说明

## 电子化学势
即费米能级，可以通过外界条件改变，因此此处为一个变量

## 能量修正项
势能影响和静电相互作用

## 计算流程
下面的结构优化过程全部使用PBE泛函，SCF计算全部使用HSE泛函

1、对初始结构（无缺陷结构）进行结构优化，作为Host（Bulk），顺便做一次SCF

2、扩胞，构建缺陷结构（中性、+q、-q ...）

3、对上述构造出的缺陷结构进行结构优化（保持与Host的晶格常数一致，即只优化原子位置）

4、对优化后的结构进行SCF计算

5、原子化学势的计算、修正项的计算

6、汇总

## Example Vo@SiO2
1、Host为包含324个原子的 Amor-SiO2 结构，对其进行结构优化，参数如下
```
16 1
job = relax 

# scf
rho_error = 1.0e-5
e_error = 0.0 # 1.0e-5
wg_error = 0.0
ecut = 50
ecut2 = 200
mp_n123 = 1 1 1 0 0 0 0 
xcfunctional = pbe 
relax_detail = 1, 500, 0.02, 0, 0.01 # 不要优化晶格，受力收敛不了 ~

# input
in.atom = atom.config
spin = 1 
## pseudo potential
in.psp1 = Si.SG15.PBE.UPF
in.psp2 = O.SG15.PBE.UPF

# in.wg = t
# in.rho = t
# in.vr = t
# in.kpt = t

# output
out.wg = f
out.rho = f
out.vr = f
out.force = t
out.stress = t
```
>确保电子步（SCF）收敛，以及最后的总受力达标，可以查看 RELAXSTEPS 文件

```
It=  160 CORR E=  -0.1056701980731E+06  Av_F=  0.52E-02 M_F=  0.25E-01 dE=  0.26E-04 dRho=  0.50E-05 SCF=     3 dL= -0.55E-02 p*F= -0.31E-02 p*F0= -0.67E-01 Fch=  0.81E+00
It=  161  NEW E=  -0.1056701985283E+06  Av_F=  0.42E-02 M_F=  0.25E-01 dE=  0.85E-04 dRho=  0.58E-05 SCF=     5 dL=  0.34E-02 p*F= -0.17E-01 p*F0= -0.74E-01 Fch=  0.12E+01
It=  162 CORR E=  -0.1056701985093E+06  Av_F=  0.52E-02 M_F=  0.35E-01 dE=  0.37E-04 dRho=  0.38E-05 SCF=     3 dL=  0.44E-02 p*F= -0.33E-02 p*F0= -0.74E-01 Fch=  0.10E+01
It=  163  NEW E=  -0.1056701988853E+06  Av_F=  0.39E-02 M_F=  0.16E-01 dE=  0.31E-04 dRho=  0.91E-05 SCF=     4 dL=  0.35E-02 p*F= -0.30E-01 p*F0= -0.67E-01 Fch=  0.94E+00
It=  164 *END E=  -0.1056701988853E+06  Av_F=  0.39E-02 M_F=  0.16E-01 dE=  0.31E-04 dRho=  0.91E-05 SCF=     4 dL=  0.35E-02 p*F= -0.30E-01 p*F0= -0.67E-01 Fch=  0.94E+00
```

2、对 Host 结构优化完成后，换 HSE 泛函进行一次 SCF 计算，注意最后计算出的带隙要合理

0.8063 - 7.7613 默认参数 alpha=0.25 omega=0.2 beta=0.0

0.4094 - 8.1154 beta=0.25，其余默认

-0.5820 - 8.2459 alpha=0.5，其余默认，计算时间从800+s 到了 1000+s 

带隙大约 8.8 eV 足够合理，后续 HSE 计算使用 alpha=0.5，omega=0.2，beta=0.0
```
16 1

job = scf 

# scf
rho_error = 1.0e-5
e_error = 0.0 # 1.0e-5
wg_error = 0.0
ecut = 50
ecut2 = 200
mp_n123 = 1 1 1 0 0 0 0 

xcfunctional = hse
hse_omega = 0.2
hse_alpha = 0.5
hse_beta = 0.0

# input
in.atom = atom.config
spin = 1 

## pseudo potential
in.psp1 = Si.SG15.PBE.UPF
in.psp2 = O.SG15.PBE.UPF

# in.wg = t
# in.rho = t
# in.vr = t
# in.kpt = t

# output
out.wg = t
out.rho = t
out.vr = t
out.force = t
out.stress = t
out.vatom = t
```

3、构建缺陷结构（在优化好的 Host 的合适的位置处挖去一个 O 原子），然后进行结构优化（不优化晶格），参数如下

删除 Host 中的 Atom: 247  O139   O   0.41846   0.60278   0.44260  ( 0  0  0)+ x, y, z


```
16 1
job = relax 

# scf
rho_error = 1.0e-5
e_error = 0.0 # 1.0e-5
wg_error = 0.0
ecut = 50
ecut2 = 200
mp_n123 = 1 1 1 0 0 0 0 
xcfunctional = pbe 
relax_detail = 1, 500, 0.02, 0, 0.01 # 不要优化晶格，受力收敛不了 ~

# input
in.atom = atom.config
spin = 2 # 缺陷计算开启自旋 
## pseudo potential
in.psp1 = Si.SG15.PBE.UPF
in.psp2 = O.SG15.PBE.UPF

# in.wg = t
# in.rho = t
# in.vr = t
# in.kpt = t

# output
out.wg = f
out.rho = f
out.vr = f
out.force = t
out.stress = t
```

4、同样的换 HSE 泛函进行一次 SCF 计算，输出所需的各种量

参数同 Host ，但是开启自旋