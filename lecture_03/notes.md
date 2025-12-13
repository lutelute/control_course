# 第3回：状態方程式の解

## 1. 問題設定

線形時不変システムの状態方程式：

$$\dot{\mathbf{x}}(t) = A\mathbf{x}(t) + B\mathbf{u}(t), \quad \mathbf{x}(0) = \mathbf{x}_0$$

この初期値問題の解を求めます。

## 2. 同次方程式の解（自由応答）

入力がない場合 $\mathbf{u}(t) = 0$：

$$\dot{\mathbf{x}}(t) = A\mathbf{x}(t)$$

### 2.1 スカラーの場合との類推

スカラー方程式 $\dot{x} = ax$ の解は $x(t) = e^{at}x_0$ です。

行列の場合も同様に：

$$\mathbf{x}(t) = e^{At}\mathbf{x}_0$$

ここで $e^{At}$ は **行列指数関数** です。

### 2.2 行列指数関数の定義

$$e^{At} = \sum_{k=0}^{\infty} \frac{(At)^k}{k!} = I + At + \frac{(At)^2}{2!} + \frac{(At)^3}{3!} + \cdots$$

**性質：**
1. $e^{A \cdot 0} = I$
2. $\frac{d}{dt}e^{At} = Ae^{At} = e^{At}A$
3. $e^{A(t+s)} = e^{At}e^{As}$
4. $(e^{At})^{-1} = e^{-At}$

## 3. 非同次方程式の解（強制応答）

入力がある場合の一般解：

$$\mathbf{x}(t) = e^{At}\mathbf{x}_0 + \int_0^t e^{A(t-\tau)}B\mathbf{u}(\tau)d\tau$$

**導出：** 定数変化法を用いて $\mathbf{x}(t) = e^{At}\mathbf{c}(t)$ とおき、微分方程式に代入：

$$e^{At}\dot{\mathbf{c}}(t) + Ae^{At}\mathbf{c}(t) = Ae^{At}\mathbf{c}(t) + B\mathbf{u}(t)$$

$$\dot{\mathbf{c}}(t) = e^{-At}B\mathbf{u}(t)$$

積分して：

$$\mathbf{c}(t) = \mathbf{x}_0 + \int_0^t e^{-A\tau}B\mathbf{u}(\tau)d\tau$$

## 4. 遷移行列

### 4.1 定義

**状態遷移行列（State Transition Matrix）** $\Phi(t)$ は：

$$\Phi(t) = e^{At}$$

時刻 $t_0$ から $t$ への遷移を表す：

$$\Phi(t, t_0) = e^{A(t-t_0)}$$

### 4.2 遷移行列の性質

1. **初期条件**: $\Phi(0) = I$
2. **微分方程式を満たす**: $\dot{\Phi}(t) = A\Phi(t)$
3. **半群性**: $\Phi(t_2, t_0) = \Phi(t_2, t_1)\Phi(t_1, t_0)$
4. **逆行列**: $\Phi^{-1}(t, t_0) = \Phi(t_0, t)$

## 5. 出力の計算

状態と出力の関係 $\mathbf{y}(t) = C\mathbf{x}(t) + D\mathbf{u}(t)$ より：

$$\mathbf{y}(t) = Ce^{At}\mathbf{x}_0 + \int_0^t Ce^{A(t-\tau)}B\mathbf{u}(\tau)d\tau + D\mathbf{u}(t)$$

初期状態がゼロのとき：

$$\mathbf{y}(t) = \int_0^t g(t-\tau)\mathbf{u}(\tau)d\tau + D\mathbf{u}(t)$$

ここで $g(t) = Ce^{At}B$ は **インパルス応答行列** です。

## 6. 畳み込み積分

入力 $\mathbf{u}(t)$ に対する出力は畳み込み積分で表現：

$$\mathbf{y}(t) = (g * \mathbf{u})(t) = \int_0^t g(t-\tau)\mathbf{u}(\tau)d\tau$$

**ラプラス変換** では：

$$Y(s) = G(s)U(s)$$

ここで $G(s) = C(sI-A)^{-1}B + D$ は伝達関数行列です。

## 7. 例題

### 2次系の解

$$A = \begin{bmatrix} 0 & 1 \\ -2 & -3 \end{bmatrix}, \quad \mathbf{x}_0 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$$

固有値：$\lambda_1 = -1, \lambda_2 = -2$

遷移行列（対角化により）：

$$e^{At} = \begin{bmatrix} 2e^{-t} - e^{-2t} & e^{-t} - e^{-2t} \\ -2e^{-t} + 2e^{-2t} & -e^{-t} + 2e^{-2t} \end{bmatrix}$$

解：

$$\mathbf{x}(t) = e^{At}\mathbf{x}_0 = \begin{bmatrix} 2e^{-t} - e^{-2t} \\ -2e^{-t} + 2e^{-2t} \end{bmatrix}$$

## 8. まとめ

- 状態方程式の解は行列指数関数 $e^{At}$ を用いて表現
- 自由応答：$\mathbf{x}(t) = e^{At}\mathbf{x}_0$
- 強制応答：畳み込み積分で計算
- 遷移行列は状態の時間発展を記述する基本量
