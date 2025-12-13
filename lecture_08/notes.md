# 第8回：可制御性

## 1. 可制御性の定義

### 1.1 状態の可制御性

システム $(A, B)$ において、状態 $\mathbf{x}_0$ が **可制御** とは：
有限時間 $t_f$ と入力 $\mathbf{u}(t)$ が存在して、$\mathbf{x}(0) = \mathbf{x}_0$ から $\mathbf{x}(t_f) = \mathbf{0}$ へ移動可能

### 1.2 システムの可制御性

すべての状態が可制御のとき、システムは **完全可制御** と呼ばれます。

## 2. 可制御性の判定

### 2.1 可制御性行列

$$\mathcal{C} = \begin{bmatrix} B & AB & A^2B & \cdots & A^{n-1}B \end{bmatrix}$$

**定理（カルマン）：** $(A, B)$ が可制御 ⟺ $\text{rank}(\mathcal{C}) = n$

### 2.2 例

$$A = \begin{bmatrix} 0 & 1 \\ -2 & -3 \end{bmatrix}, \quad B = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

$$\mathcal{C} = \begin{bmatrix} B & AB \end{bmatrix} = \begin{bmatrix} 0 & 1 \\ 1 & -3 \end{bmatrix}$$

$\det(\mathcal{C}) = -1 \neq 0$ なので $\text{rank}(\mathcal{C}) = 2$、可制御。

## 3. 可制御性のグラム行列

### 3.1 定義

$$W_c(t) = \int_0^t e^{A\tau}BB^Te^{A^T\tau}d\tau$$

### 3.2 判定条件

$(A, B)$ が可制御 ⟺ ある $t > 0$ で $W_c(t)$ が正定値

### 3.3 最小エネルギー制御

$\mathbf{x}(0) = \mathbf{x}_0$ から $\mathbf{x}(t_f) = \mathbf{0}$ への最小エネルギー入力：

$$\mathbf{u}^*(t) = -B^T e^{A^T(t_f-t)} W_c^{-1}(t_f) e^{At_f} \mathbf{x}_0$$

## 4. 可制御正準形

可制御なシステムは座標変換により以下の形に変換可能：

$$A_c = \begin{bmatrix} 0 & 1 & 0 & \cdots & 0 \\ 0 & 0 & 1 & \cdots & 0 \\ \vdots & & & \ddots & \vdots \\ 0 & 0 & 0 & \cdots & 1 \\ -a_n & -a_{n-1} & \cdots & -a_2 & -a_1 \end{bmatrix}, \quad B_c = \begin{bmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix}$$

## 5. 可制御性の物理的意味

- 可制御 = 入力がすべての状態に影響を与えられる
- 不可制御 = 入力では動かせない状態（モード）が存在
- 極配置やフィードバック制御には可制御性が必要

## 6. 可制御部分空間

不可制御なシステムでは、可制御な部分空間を特定：

$$\mathcal{R}(\mathcal{C}) = \text{Im}(\mathcal{C})$$

この部分空間内の状態のみ制御可能。

## 7. PBH可制御性テスト

### 7.1 固有値条件

**定理（Popov-Belevitch-Hautus）：**

$(A, B)$ が可制御 ⟺ すべての $\lambda \in \mathbb{C}$ に対して

$$\text{rank}\begin{bmatrix} \lambda I - A & B \end{bmatrix} = n$$

### 7.2 幾何学的解釈

不可制御モードは $A$ の固有ベクトルで $B$ と直交するもの。

## 8. 離散時間システムの可制御性

離散時間システム $\mathbf{x}_{k+1} = A_d\mathbf{x}_k + B_d\mathbf{u}_k$ に対しても同様：

$$\mathcal{C}_d = \begin{bmatrix} B_d & A_dB_d & \cdots & A_d^{n-1}B_d \end{bmatrix}$$

$\text{rank}(\mathcal{C}_d) = n$ ⟺ 可制御

## 9. 可制御性と安定化

**定理：** システム $(A, B)$ において、不安定な固有値に対応するモードが可制御ならば、
状態フィードバックにより安定化可能（可安定性）。

## 10. まとめ

| 判定法 | 条件 |
|-------|------|
| ランク条件 | $\text{rank}(\mathcal{C}) = n$ |
| グラム行列 | $W_c(t) > 0$ |
| PBHテスト | $\text{rank}[\lambda I - A \; B] = n$ |

- 可制御性は状態フィードバック制御の前提条件
- 可制御性行列 $\mathcal{C}$ のランクで判定
- 可制御なシステムは可制御正準形に変換可能
- 不可制御でも不安定モードが可制御なら安定化可能
