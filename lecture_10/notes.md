# 第10回：状態フィードバックと極配置

## 1. 状態フィードバック制御

### 1.1 制御則

$$\mathbf{u} = -K\mathbf{x} + \mathbf{r}$$

ここで $K$ はフィードバックゲイン行列、$\mathbf{r}$ は参照入力。

### 1.2 閉ループ系

開ループ系：$\dot{\mathbf{x}} = A\mathbf{x} + B\mathbf{u}$

閉ループ系：$\dot{\mathbf{x}} = (A - BK)\mathbf{x} + B\mathbf{r}$

## 2. 極配置法

### 2.1 目的

閉ループ系の極（$A - BK$ の固有値）を望ましい位置に配置。

### 2.2 極配置の定理

**定理：** $(A, B)$ が可制御 ⟺ 任意の極配置が実現可能

### 2.3 アッカーマンの公式（SISO系）

望ましい特性多項式を $\phi(s) = s^n + p_1 s^{n-1} + \cdots + p_n$ とすると：

$$K = \begin{bmatrix} 0 & \cdots & 0 & 1 \end{bmatrix} \mathcal{C}^{-1} \phi(A)$$

ここで $\mathcal{C}$ は可制御性行列。

## 3. 2次系の極配置

### 3.1 設計例

$$A = \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix}, \quad B = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

目標極：$s = -2 \pm j2$

目標特性多項式：$(s+2-j2)(s+2+j2) = s^2 + 4s + 8$

### 3.2 ゲインの計算

$K = \begin{bmatrix} k_1 & k_2 \end{bmatrix}$ とすると：

$$A - BK = \begin{bmatrix} 0 & 1 \\ -k_1 & -k_2 \end{bmatrix}$$

特性方程式：$s^2 + k_2 s + k_1 = s^2 + 4s + 8$

よって $k_1 = 8$, $k_2 = 4$

## 4. 望ましい極の選び方

### 4.1 過渡応答の要求仕様

- **減衰比** $\zeta$：オーバーシュートの抑制
- **固有角周波数** $\omega_n$：応答速度

### 4.2 支配極の概念

高速極の影響は相対的に小さいため、支配極で設計。

### 4.3 実用的な指針

- 整定時間 $t_s \approx 4/\sigma$ を考慮
- オーバーシュート許容量から $\zeta$ を決定
- アクチュエータの制約を考慮

## 5. 定常偏差の除去

状態フィードバックのみでは定常偏差が生じる場合がある。

### 5.1 積分器の追加

拡大系：
$$\dot{\mathbf{x}}_a = \begin{bmatrix} A & 0 \\ -C & 0 \end{bmatrix}\mathbf{x}_a + \begin{bmatrix} B \\ 0 \end{bmatrix}\mathbf{u} + \begin{bmatrix} 0 \\ 1 \end{bmatrix}\mathbf{r}$$

## 6. ロバスト性の考慮

### 6.1 ゲイン余裕と位相余裕

極配置だけでは保証されない。

### 6.2 最適レギュレータとの比較

LQR（次回）では自動的に一定のロバスト性が保証される。

## 7. まとめ

- 状態フィードバック $\mathbf{u} = -K\mathbf{x}$ で極を任意配置可能（可制御性が必要）
- アッカーマンの公式で系統的に $K$ を計算
- 極の位置は応答仕様から決定
- 実用上はロバスト性や入力制約も考慮が必要
