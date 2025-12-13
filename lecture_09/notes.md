# 第9回：可観測性

## 1. 可観測性の定義

### 1.1 状態の可観測性

システム $(A, C)$ において、初期状態 $\mathbf{x}(0)$ が **可観測** とは：
有限時間 $[0, t_f]$ の出力 $\mathbf{y}(t)$ の観測から $\mathbf{x}(0)$ を一意に決定可能

### 1.2 システムの可観測性

すべての初期状態が可観測のとき、システムは **完全可観測** と呼ばれます。

## 2. 可観測性の判定

### 2.1 可観測性行列

$$\mathcal{O} = \begin{bmatrix} C \\ CA \\ CA^2 \\ \vdots \\ CA^{n-1} \end{bmatrix}$$

**定理（カルマン）：** $(A, C)$ が可観測 ⟺ $\text{rank}(\mathcal{O}) = n$

### 2.2 例

$$A = \begin{bmatrix} 0 & 1 \\ -2 & -3 \end{bmatrix}, \quad C = \begin{bmatrix} 1 & 0 \end{bmatrix}$$

$$\mathcal{O} = \begin{bmatrix} C \\ CA \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$$

$\text{rank}(\mathcal{O}) = 2$ なので可観測。

## 3. 可観測性のグラム行列

### 3.1 定義

$$W_o(t) = \int_0^t e^{A^T\tau}C^TCe^{A\tau}d\tau$$

### 3.2 判定条件

$(A, C)$ が可観測 ⟺ ある $t > 0$ で $W_o(t)$ が正定値

### 3.3 初期状態の推定

出力観測から初期状態を復元：

$$\mathbf{x}(0) = W_o^{-1}(t_f) \int_0^{t_f} e^{A^T\tau}C^T \mathbf{y}(\tau)d\tau$$

## 4. 可観測正準形

可観測なシステムは座標変換により以下の形に変換可能：

$$A_o = \begin{bmatrix} 0 & 0 & \cdots & 0 & -a_n \\ 1 & 0 & \cdots & 0 & -a_{n-1} \\ 0 & 1 & \cdots & 0 & -a_{n-2} \\ \vdots & & \ddots & & \vdots \\ 0 & 0 & \cdots & 1 & -a_1 \end{bmatrix}, \quad C_o = \begin{bmatrix} 0 & 0 & \cdots & 0 & 1 \end{bmatrix}$$

## 5. 双対性

### 5.1 可制御性と可観測性の双対関係

$(A, B)$ が可制御 ⟺ $(A^T, B^T)$ が可観測

$(A, C)$ が可観測 ⟺ $(A^T, C^T)$ が可制御

### 5.2 双対システム

元のシステム：$\dot{\mathbf{x}} = A\mathbf{x} + B\mathbf{u}$, $\mathbf{y} = C\mathbf{x}$

双対システム：$\dot{\mathbf{z}} = A^T\mathbf{z} + C^T\mathbf{v}$, $\mathbf{w} = B^T\mathbf{z}$

## 6. 可観測性の物理的意味

- 可観測 = 出力からすべての状態の情報が得られる
- 不可観測 = 出力に現れない隠れた状態（モード）が存在
- オブザーバ設計には可観測性が必要

## 7. 可検出性（Detectability）

不安定なモードが可観測であれば **可検出** と呼ばれます。
オブザーバによる安定な推定には可検出性で十分。

## 8. PBH可観測性テスト

**定理（Popov-Belevitch-Hautus）：**

$(A, C)$ が可観測 ⟺ すべての $\lambda \in \mathbb{C}$ に対して

$$\text{rank}\begin{bmatrix} \lambda I - A \\ C \end{bmatrix} = n$$

## 9. 最小実現

### 9.1 定義

伝達関数 $G(s)$ の状態空間実現 $(A, B, C, D)$ が **最小実現** とは：
状態の次元 $n$ が可能な限り小さい実現。

### 9.2 条件

**定理：** $(A, B, C, D)$ が最小実現 ⟺ $(A, B)$ が可制御かつ $(A, C)$ が可観測

### 9.3 伝達関数との関係

- 不可制御モード → 極零相殺により伝達関数に現れない
- 不可観測モード → 同様に相殺される

## 10. まとめ

| 性質 | 行列条件 | 意味 |
|------|---------|------|
| 可観測 | $\text{rank}(\mathcal{O}) = n$ | 全状態が推定可能 |
| 可検出 | 不安定モードが可観測 | 安定なオブザーバが存在 |
| 最小実現 | 可制御 + 可観測 | 伝達関数の次数 = 状態次元 |

- 可観測性はオブザーバ設計の前提条件
- 可観測性行列 $\mathcal{O}$ のランクで判定
- 可制御性と可観測性は双対関係
- 最小実現 = 可制御かつ可観測
