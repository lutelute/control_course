# 第5回：伝達関数と状態空間表現

## 1. 伝達関数の定義

### 1.1 SISO（単入力単出力）システム

初期値ゼロの条件下で、入力 $U(s)$ と出力 $Y(s)$ のラプラス変換の比：

$$G(s) = \frac{Y(s)}{U(s)}$$

### 1.2 状態空間表現からの導出

状態方程式：
$$\dot{\mathbf{x}} = A\mathbf{x} + B\mathbf{u}$$
$$\mathbf{y} = C\mathbf{x} + D\mathbf{u}$$

ラプラス変換（初期値ゼロ）：
$$sX(s) = AX(s) + BU(s)$$
$$Y(s) = CX(s) + DU(s)$$

$X(s)$ を消去：
$$X(s) = (sI - A)^{-1}BU(s)$$
$$Y(s) = [C(sI - A)^{-1}B + D]U(s)$$

したがって：
$$G(s) = C(sI - A)^{-1}B + D$$

## 2. 伝達関数の性質

### 2.1 極と固有値

伝達関数の **極**（分母の根）は、行列 $A$ の **固有値** に一致します。

$$\det(sI - A) = 0 \quad \Rightarrow \quad s = \lambda_i$$

### 2.2 可約な極零相殺

状態空間表現の固有値がすべて伝達関数の極として現れるとは限りません。
**可制御でない** または **可観測でない** モードは相殺されます。

## 3. 状態空間表現から伝達関数への変換

### 3.1 公式

$$G(s) = C(sI - A)^{-1}B + D = C \cdot \frac{\text{adj}(sI-A)}{\det(sI-A)} \cdot B + D$$

### 3.2 計算例

$$A = \begin{bmatrix} 0 & 1 \\ -2 & -3 \end{bmatrix}, \quad B = \begin{bmatrix} 0 \\ 1 \end{bmatrix}, \quad C = \begin{bmatrix} 1 & 0 \end{bmatrix}, \quad D = 0$$

$$sI - A = \begin{bmatrix} s & -1 \\ 2 & s+3 \end{bmatrix}$$

$$\det(sI-A) = s^2 + 3s + 2 = (s+1)(s+2)$$

$$(sI-A)^{-1} = \frac{1}{(s+1)(s+2)}\begin{bmatrix} s+3 & 1 \\ -2 & s \end{bmatrix}$$

$$G(s) = \frac{1}{(s+1)(s+2)}\begin{bmatrix} 1 & 0 \end{bmatrix}\begin{bmatrix} s+3 & 1 \\ -2 & s \end{bmatrix}\begin{bmatrix} 0 \\ 1 \end{bmatrix} = \frac{1}{(s+1)(s+2)}$$

## 4. 伝達関数から状態空間表現への変換

### 4.1 可制御正準形

$$G(s) = \frac{b_1s^{n-1} + \cdots + b_n}{s^n + a_1s^{n-1} + \cdots + a_n}$$

$$A_c = \begin{bmatrix} 0 & 1 & 0 & \cdots & 0 \\ 0 & 0 & 1 & \cdots & 0 \\ \vdots & & & \ddots & \vdots \\ 0 & 0 & 0 & \cdots & 1 \\ -a_n & -a_{n-1} & -a_{n-2} & \cdots & -a_1 \end{bmatrix}$$

$$B_c = \begin{bmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix}, \quad C_c = \begin{bmatrix} b_n & b_{n-1} & \cdots & b_1 \end{bmatrix}$$

### 4.2 可観測正準形

$$A_o = A_c^T, \quad B_o = C_c^T, \quad C_o = B_c^T$$

### 4.3 対角正準形

相異なる極 $p_1, p_2, \ldots, p_n$ の場合、部分分数展開：

$$G(s) = \frac{r_1}{s - p_1} + \frac{r_2}{s - p_2} + \cdots + \frac{r_n}{s - p_n}$$

$$A_d = \begin{bmatrix} p_1 & & \\ & p_2 & \\ & & \ddots \end{bmatrix}, \quad B_d = \begin{bmatrix} 1 \\ 1 \\ \vdots \end{bmatrix}, \quad C_d = \begin{bmatrix} r_1 & r_2 & \cdots \end{bmatrix}$$

## 5. 実現の等価性

### 5.1 等価な実現

同じ伝達関数を持つ状態空間表現は無数に存在します。

座標変換 $\tilde{\mathbf{x}} = T\mathbf{x}$ による等価な実現：
$$\tilde{A} = TAT^{-1}, \quad \tilde{B} = TB, \quad \tilde{C} = CT^{-1}, \quad \tilde{D} = D$$

### 5.2 最小実現

状態の次元が最小となる実現を **最小実現** と呼びます。
- 可制御かつ可観測
- 状態の次元 = 伝達関数の次数（McMillan次数）

## 6. MIMO システム

多入力多出力システムの伝達関数行列：

$$G(s) = C(sI - A)^{-1}B + D \in \mathbb{R}^{p \times m}$$

各要素 $G_{ij}(s)$ は入力 $j$ から出力 $i$ への伝達関数。

## 7. まとめ

- 伝達関数は $G(s) = C(sI-A)^{-1}B + D$ で計算
- 極は行列 $A$ の固有値に対応
- 正準形を使って伝達関数から状態空間表現を構成
- 等価な実現は無数に存在するが、最小実現は一意（座標変換を除く）
