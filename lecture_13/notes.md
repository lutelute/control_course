# 第13回：リッカチ方程式と最適性

## 1. 最適制御問題の定式化

### 1.1 無限時間レギュレータ問題

$$\min_{\mathbf{u}} J = \int_0^\infty (\mathbf{x}^T Q \mathbf{x} + \mathbf{u}^T R \mathbf{u}) dt$$

制約：$\dot{\mathbf{x}} = A\mathbf{x} + B\mathbf{u}$

### 1.2 有限時間レギュレータ問題

$$\min_{\mathbf{u}} J = \mathbf{x}^T(t_f) S \mathbf{x}(t_f) + \int_0^{t_f} (\mathbf{x}^T Q \mathbf{x} + \mathbf{u}^T R \mathbf{u}) dt$$

## 2. 代数リッカチ方程式（ARE）

### 2.1 定常問題の解

無限時間問題では、最適コストは $V(\mathbf{x}) = \mathbf{x}^T P \mathbf{x}$ の形。

$P$ は **代数リッカチ方程式** を満たす：

$$A^T P + PA - PBR^{-1}B^T P + Q = 0$$

### 2.2 最適ゲイン

$$K = R^{-1}B^T P$$

最適制御則：$\mathbf{u}^* = -K\mathbf{x}$

### 2.3 解の存在条件

$(A, B)$ が可安定、$(A, Q^{1/2})$ が可検出ならば、
ARE は唯一の正定値解 $P \geq 0$ を持つ。

## 3. 微分リッカチ方程式（DRE）

### 3.1 有限時間問題

時変ゲイン $K(t) = R^{-1}B^T P(t)$ を使用。

$P(t)$ は微分リッカチ方程式を満たす：

$$-\dot{P} = A^T P + PA - PBR^{-1}B^T P + Q$$

終端条件：$P(t_f) = S$

### 3.2 後退積分

$t = t_f$ から $t = 0$ へ向かって積分。

## 4. ハミルトン行列による解法

### 4.1 ハミルトン行列

$$H = \begin{bmatrix} A & -BR^{-1}B^T \\ -Q & -A^T \end{bmatrix}$$

### 4.2 安定固有空間

$H$ の安定固有値に対応する固有空間から $P$ を計算：

$$\begin{bmatrix} X_1 \\ X_2 \end{bmatrix} \text{ が安定固有空間} \Rightarrow P = X_2 X_1^{-1}$$

## 5. 最適性の検証

### 5.1 ハミルトン・ヤコビ・ベルマン方程式

最適コスト関数 $V(\mathbf{x})$ は HJB 方程式を満たす：

$$\min_{\mathbf{u}} \left[ \mathbf{x}^T Q \mathbf{x} + \mathbf{u}^T R \mathbf{u} + \frac{\partial V}{\partial \mathbf{x}}(A\mathbf{x} + B\mathbf{u}) \right] = 0$$

### 5.2 最適制御の導出

$$\mathbf{u}^* = -\frac{1}{2}R^{-1}B^T \frac{\partial V}{\partial \mathbf{x}}^T = -R^{-1}B^T P \mathbf{x}$$

## 6. 数値解法

### 6.1 反復法（ニュートン法）

$$A_k^T P_{k+1} + P_{k+1} A_k + Q + P_k B R^{-1} B^T P_k = 0$$

ここで $A_k = A - BR^{-1}B^T P_k$

### 6.2 Schur分解法

ハミルトン行列の Schur 分解を利用した数値安定な方法。

## 7. LQR の性質

### 7.1 安定余裕

- ゲイン余裕：無限大（$K$ を 0.5 から $\infty$ まで変化させても安定）
- 位相余裕：少なくとも 60°

### 7.2 リターン差等式

$$[I + K(sI-A)^{-1}B]^T R [I + K(sI-A)^{-1}B] = R + B^T(-sI-A^T)^{-1}Q(sI-A)^{-1}B$$

## 8. まとめ

- LQR の最適ゲインは代数リッカチ方程式の解から計算
- ハミルトン行列の固有値解析が有効
- LQR は優れたロバスト性（ゲイン・位相余裕）を持つ
- 有限時間問題では微分リッカチ方程式を後退積分
