# 第7回：リアプノフ方程式

## 1. リアプノフ安定性理論

### 1.1 リアプノフ関数

**リアプノフ関数** $V(\mathbf{x})$ は、システムのエネルギーのような量を表す正定値関数です。

**正定値関数の条件：**
- $V(\mathbf{0}) = 0$
- $V(\mathbf{x}) > 0$ for all $\mathbf{x} \neq \mathbf{0}$

### 1.2 リアプノフの安定定理

システム $\dot{\mathbf{x}} = f(\mathbf{x})$ について：

1. $V(\mathbf{x})$ が正定値
2. $\dot{V}(\mathbf{x}) = \frac{\partial V}{\partial \mathbf{x}} f(\mathbf{x}) \leq 0$ （負準定値）

ならば、原点は **安定**。

さらに $\dot{V}(\mathbf{x}) < 0$ （負定値）ならば **漸近安定**。

## 2. 線形システムのリアプノフ方程式

### 2.1 2次形式リアプノフ関数

線形システム $\dot{\mathbf{x}} = A\mathbf{x}$ に対し、2次形式：

$$V(\mathbf{x}) = \mathbf{x}^T P \mathbf{x}$$

ここで $P$ は正定値対称行列。

### 2.2 時間微分の計算

$$\dot{V} = \dot{\mathbf{x}}^T P \mathbf{x} + \mathbf{x}^T P \dot{\mathbf{x}}$$
$$= \mathbf{x}^T A^T P \mathbf{x} + \mathbf{x}^T P A \mathbf{x}$$
$$= \mathbf{x}^T (A^T P + P A) \mathbf{x}$$

### 2.3 リアプノフ方程式

$\dot{V} = -\mathbf{x}^T Q \mathbf{x}$ となるためには：

$$A^T P + P A = -Q$$

これが **連続時間リアプノフ方程式** です。

**定理：** $A$ が安定（すべての固有値が左半平面）⟺ 任意の正定値 $Q$ に対して一意な正定値解 $P$ が存在

## 3. リアプノフ方程式の解法

### 3.1 ベクトル化による方法

クロネッカー積を用いて行列方程式を連立方程式に変換：

$$\text{vec}(A^T P + P A) = (I \otimes A^T + A^T \otimes I)\text{vec}(P) = -\text{vec}(Q)$$

### 3.2 数値解法

MATLAB: `P = lyap(A', Q)`
Python (scipy): `P = solve_continuous_lyapunov(A.T, -Q)`

### 3.3 2次系の解析解

$$A = \begin{bmatrix} 0 & 1 \\ -a_0 & -a_1 \end{bmatrix}, \quad Q = I$$

リアプノフ方程式を解くと：

$$P = \begin{bmatrix} \frac{a_0 + a_1^2 + 1}{2a_0 a_1} & \frac{1}{2a_0} \\ \frac{1}{2a_0} & \frac{a_0 + 1}{2a_0 a_1} \end{bmatrix}$$

## 4. リアプノフ関数の幾何学的解釈

### 4.1 等高線（レベルセット）

$$V(\mathbf{x}) = c \quad (\text{定数})$$

は楕円を描く。$P$ の固有ベクトルが楕円の主軸方向。

### 4.2 状態軌道とレベルセット

漸近安定ならば、軌道は常により小さなレベルセットへ移動：

$$\dot{V} < 0 \Rightarrow \text{軌道は内側へ}$$

## 5. 離散時間リアプノフ方程式

離散時間システム $\mathbf{x}_{k+1} = A\mathbf{x}_k$ に対して：

$$A^T P A - P = -Q$$

**安定条件：** すべての固有値の絶対値が1未満

## 6. 応用：コントローラ設計への利用

### 6.1 リアプノフ不等式（LMI）

$A^T P + PA < 0$ を満たす $P > 0$ の存在が安定性と等価。

### 6.2 $H_\infty$ 制御との関係

リアプノフ方程式は $H_\infty$ ノルムの計算にも使用：

$$\|G\|_{\infty}^2 < \gamma^2 \Leftrightarrow \exists P > 0: A^T P + PA + \frac{1}{\gamma^2}PBB^T P + C^T C < 0$$

## 7. まとめ

- リアプノフ関数は系のエネルギーを一般化した概念
- $V = \mathbf{x}^T P \mathbf{x}$ が減少すれば安定
- リアプノフ方程式 $A^T P + PA = -Q$ の正定値解の存在が安定性の判定条件
- 数値的に効率よく解ける（多項式時間）
