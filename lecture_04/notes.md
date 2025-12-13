# 第4回：遷移行列の計算

## 1. 遷移行列の計算法

行列指数関数 $e^{At}$ を計算する方法は複数あります。

## 2. ラプラス変換による方法

### 2.1 基本公式

$$e^{At} = \mathcal{L}^{-1}\{(sI - A)^{-1}\}$$

**導出：** 状態方程式 $\dot{\mathbf{x}} = A\mathbf{x}$ のラプラス変換：

$$sX(s) - \mathbf{x}_0 = AX(s)$$
$$(sI - A)X(s) = \mathbf{x}_0$$
$$X(s) = (sI - A)^{-1}\mathbf{x}_0$$

逆変換して $\mathbf{x}(t) = e^{At}\mathbf{x}_0$ と比較。

### 2.2 計算手順

1. $sI - A$ を計算
2. $(sI - A)^{-1}$ を求める（余因子行列と行列式を使用）
3. 各要素を逆ラプラス変換

### 2.3 例：2次系

$$A = \begin{bmatrix} 0 & 1 \\ -6 & -5 \end{bmatrix}$$

$$sI - A = \begin{bmatrix} s & -1 \\ 6 & s+5 \end{bmatrix}$$

$$\det(sI - A) = s(s+5) + 6 = s^2 + 5s + 6 = (s+2)(s+3)$$

$$(sI - A)^{-1} = \frac{1}{(s+2)(s+3)}\begin{bmatrix} s+5 & 1 \\ -6 & s \end{bmatrix}$$

部分分数展開と逆変換で $e^{At}$ を得る。

## 3. 対角化による方法

### 3.1 対角化可能な場合

$A$ が対角化可能で $A = PDP^{-1}$（$D$ は固有値の対角行列）のとき：

$$e^{At} = Pe^{Dt}P^{-1}$$

$$e^{Dt} = \begin{bmatrix} e^{\lambda_1 t} & 0 & \cdots \\ 0 & e^{\lambda_2 t} & \cdots \\ \vdots & & \ddots \end{bmatrix}$$

### 3.2 計算手順

1. 固有値 $\lambda_1, \lambda_2, \ldots$ を求める
2. 対応する固有ベクトルから $P$ を構成
3. $e^{Dt}$ を計算
4. $e^{At} = Pe^{Dt}P^{-1}$

### 3.3 複素固有値の場合

$\lambda = \alpha \pm j\omega$ のとき、実数形式で：

$$e^{\alpha t}\begin{bmatrix} \cos\omega t & \sin\omega t \\ -\sin\omega t & \cos\omega t \end{bmatrix}$$

## 4. ケーリー・ハミルトンの定理を用いた方法

### 4.1 定理

任意の正方行列 $A$ は自身の特性方程式を満たす：

$$\chi_A(A) = A^n + a_{n-1}A^{n-1} + \cdots + a_1A + a_0I = 0$$

### 4.2 応用

$e^{At}$ は $A$ の $n-1$ 次以下の多項式で表現可能：

$$e^{At} = \alpha_0(t)I + \alpha_1(t)A + \cdots + \alpha_{n-1}(t)A^{n-1}$$

係数 $\alpha_i(t)$ は固有値から決定される連立方程式を解いて求める。

### 4.3 2次系の場合

$$e^{At} = \alpha_0(t)I + \alpha_1(t)A$$

相異なる固有値 $\lambda_1, \lambda_2$ の場合：

$$\begin{cases} e^{\lambda_1 t} = \alpha_0 + \alpha_1 \lambda_1 \\ e^{\lambda_2 t} = \alpha_0 + \alpha_1 \lambda_2 \end{cases}$$

解いて：

$$\alpha_0 = \frac{\lambda_1 e^{\lambda_2 t} - \lambda_2 e^{\lambda_1 t}}{\lambda_1 - \lambda_2}, \quad \alpha_1 = \frac{e^{\lambda_1 t} - e^{\lambda_2 t}}{\lambda_1 - \lambda_2}$$

## 5. 級数展開による数値計算

### 5.1 定義式の直接計算

$$e^{At} = \sum_{k=0}^{N} \frac{(At)^k}{k!}$$

$N$ を十分大きくとれば近似精度が向上。

### 5.2 パデ近似

より効率的な数値計算法：

$$e^{At} \approx [N_m(At)][D_m(At)]^{-1}$$

多くの数値計算ライブラリで採用。

## 6. シルベスターの公式

相異なる固有値 $\lambda_1, \ldots, \lambda_n$ をもつ場合：

$$e^{At} = \sum_{i=1}^{n} e^{\lambda_i t} \prod_{j \neq i} \frac{A - \lambda_j I}{\lambda_i - \lambda_j}$$

## 7. まとめ

| 方法 | 利点 | 欠点 |
|-----|-----|-----|
| ラプラス変換 | 直接的 | 手計算が煩雑 |
| 対角化 | 見通しが良い | 対角化不可能な場合あり |
| ケーリー・ハミルトン | 任意の行列に適用可 | 重根で場合分け |
| 級数展開 | 数値計算向き | 収束に注意 |
