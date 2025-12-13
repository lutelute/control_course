# 第14回：カルマンフィルタ

## 1. 状態推定問題

### 1.1 確率的システムモデル

$$\dot{\mathbf{x}} = A\mathbf{x} + B\mathbf{u} + G\mathbf{w}$$
$$\mathbf{y} = C\mathbf{x} + \mathbf{v}$$

ここで：
- $\mathbf{w}$：プロセスノイズ（共分散 $Q_w$）
- $\mathbf{v}$：観測ノイズ（共分散 $R_v$）
- $\mathbf{w}, \mathbf{v}$ は白色ガウスノイズ

### 1.2 推定の目的

観測 $\mathbf{y}(t)$ から状態 $\mathbf{x}(t)$ の最適推定値 $\hat{\mathbf{x}}(t)$ を求める

## 2. カルマンフィルタの構造

### 2.1 連続時間カルマンフィルタ

$$\dot{\hat{\mathbf{x}}} = A\hat{\mathbf{x}} + B\mathbf{u} + L(\mathbf{y} - C\hat{\mathbf{x}})$$

- $\hat{\mathbf{x}}$：状態推定値
- $L$：カルマンゲイン（オブザーバゲイン）
- $\mathbf{y} - C\hat{\mathbf{x}}$：イノベーション（推定誤差）

### 2.2 最適カルマンゲイン

$$L = PC^T R_v^{-1}$$

$P$ は推定誤差共分散：$P = E[(\mathbf{x} - \hat{\mathbf{x}})(\mathbf{x} - \hat{\mathbf{x}})^T]$

## 3. フィルタリカッチ方程式

### 3.1 共分散の時間発展

$$\dot{P} = AP + PA^T - PC^T R_v^{-1} CP + GQ_w G^T$$

### 3.2 定常カルマンフィルタ

$t \to \infty$ で $P$ は代数リカッチ方程式の解に収束：

$$AP + PA^T - PC^T R_v^{-1} CP + GQ_w G^T = 0$$

## 4. LQR との双対性

### 4.1 双対関係

| LQR | カルマンフィルタ |
|-----|--------------|
| $A$ | $A^T$ |
| $B$ | $C^T$ |
| $Q$ | $GQ_w G^T$ |
| $R$ | $R_v$ |
| $K$ | $L^T$ |

### 4.2 分離定理

LQG（線形2次ガウス）問題において：
- 最適制御器（LQR）と最適推定器（カルマンフィルタ）は独立に設計可能
- 全体の最適性が保証される

## 5. 離散時間カルマンフィルタ

### 5.1 システムモデル

$$\mathbf{x}_{k+1} = A_d \mathbf{x}_k + B_d \mathbf{u}_k + \mathbf{w}_k$$
$$\mathbf{y}_k = C\mathbf{x}_k + \mathbf{v}_k$$

### 5.2 予測ステップ

$$\hat{\mathbf{x}}_{k|k-1} = A_d \hat{\mathbf{x}}_{k-1|k-1} + B_d \mathbf{u}_{k-1}$$
$$P_{k|k-1} = A_d P_{k-1|k-1} A_d^T + Q_w$$

### 5.3 更新ステップ

$$L_k = P_{k|k-1} C^T (CP_{k|k-1}C^T + R_v)^{-1}$$
$$\hat{\mathbf{x}}_{k|k} = \hat{\mathbf{x}}_{k|k-1} + L_k(\mathbf{y}_k - C\hat{\mathbf{x}}_{k|k-1})$$
$$P_{k|k} = (I - L_k C)P_{k|k-1}$$

## 6. 拡張カルマンフィルタ（EKF）

非線形システムへの拡張：
- ヤコビアンによる線形化
- 各時刻で線形カルマンフィルタを適用

## 7. カルマンフィルタの性質

### 7.1 最適性

- 線形システム + ガウスノイズ → 最小分散推定
- MMSE（最小平均二乗誤差）推定

### 7.2 収束性

$(A, C)$ が可観測ならば、初期推定誤差は減少

## 8. まとめ

- カルマンフィルタは確率的状態推定の最適解
- LQR と双対関係（フィルタリカッチ方程式）
- 離散時間では予測・更新の2ステップ
- LQG 制御では分離定理が成立
