# 第15回：サーボシステム

## 1. サーボ問題の定義

### 1.1 目標値追従問題

システムの出力 $\mathbf{y}$ を参照入力 $\mathbf{r}$ に追従させる：

$$\lim_{t \to \infty} \mathbf{y}(t) = \mathbf{r} \quad (\text{ステップ参照の場合})$$

### 1.2 レギュレータとサーボの違い

- **レギュレータ問題**：$\mathbf{x} \to \mathbf{0}$（原点への安定化）
- **サーボ問題**：$\mathbf{y} \to \mathbf{r}$（目標値への追従）

## 2. 定常偏差と内部モデル原理

### 2.1 内部モデル原理

参照信号の生成モデルをコントローラに含めることで定常偏差をゼロにできる。

ステップ参照 → 積分器（1/s）を含む
ランプ参照 → 二重積分器（1/s²）を含む

### 2.2 1型サーボ系

積分器を1つ含むシステム：
- ステップ参照に対して定常偏差ゼロ
- ランプ参照に対して有限の定常偏差

## 3. サーボ系の設計法

### 3.1 拡大系を用いた設計

誤差 $\mathbf{e} = \mathbf{r} - \mathbf{y}$ の積分を導入：

$$\dot{\mathbf{z}} = \mathbf{e} = \mathbf{r} - C\mathbf{x}$$

拡大状態：
$$\bar{\mathbf{x}} = \begin{bmatrix} \mathbf{x} \\ \mathbf{z} \end{bmatrix}$$

### 3.2 拡大系の状態方程式

$$\dot{\bar{\mathbf{x}}} = \begin{bmatrix} A & 0 \\ -C & 0 \end{bmatrix} \bar{\mathbf{x}} + \begin{bmatrix} B \\ 0 \end{bmatrix} \mathbf{u} + \begin{bmatrix} 0 \\ I \end{bmatrix} \mathbf{r}$$

$$\bar{A} = \begin{bmatrix} A & 0 \\ -C & 0 \end{bmatrix}, \quad \bar{B} = \begin{bmatrix} B \\ 0 \end{bmatrix}$$

### 3.3 状態フィードバック

$$\mathbf{u} = -\bar{K}\bar{\mathbf{x}} = -K_x\mathbf{x} - K_z\mathbf{z}$$

- $K_x$：状態フィードバックゲイン
- $K_z$：積分ゲイン

## 4. 最適サーボ系

### 4.1 LQ サーボ問題

コスト関数：
$$J = \int_0^\infty (\mathbf{e}^T Q_e \mathbf{e} + \mathbf{u}^T R \mathbf{u}) dt$$

### 4.2 拡大系の LQR

拡大系 $(\bar{A}, \bar{B})$ に対して LQR を適用：

$$\bar{Q} = \begin{bmatrix} C^T Q_e C & 0 \\ 0 & Q_z \end{bmatrix}$$

## 5. 2自由度制御系

### 5.1 構造

$$\mathbf{u} = -K\mathbf{x} + N\mathbf{r}$$

- フィードバック補償器：$-K\mathbf{x}$
- フィードフォワード補償器：$N\mathbf{r}$

### 5.2 フィードフォワードゲイン

定常状態 $\dot{\mathbf{x}} = 0$, $\mathbf{y} = \mathbf{r}$ から：

$$N = -[C(A-BK)^{-1}B]^{-1}$$

## 6. ロバストサーボ系

### 6.1 モデル誤差への対応

積分動作により：
- パラメータ変動に対してロバスト
- 定常外乱の除去

### 6.2 アンチワインドアップ

積分器の飽和を防ぐ対策：
- 積分値のリミッタ
- バックカリキュレーション

## 7. 離散時間サーボ系

### 7.1 離散時間拡大系

$$\bar{\mathbf{x}}_{k+1} = \bar{A}_d \bar{\mathbf{x}}_k + \bar{B}_d \mathbf{u}_k + \bar{E}_d \mathbf{r}_k$$

### 7.2 デジタル実装

- サンプリング周期の選択
- 遅れ補償

## 8. まとめ

- サーボ系は目標値追従を実現
- 内部モデル原理：参照信号のモデルを含める
- 拡大系での状態フィードバック設計
- 積分動作によりロバスト性と定常偏差ゼロを達成
