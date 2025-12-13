# 第1回：システムの状態空間表現

## 1. はじめに

制御工学において、システムを数学的に表現する方法は大きく分けて2つあります：
- **伝達関数表現**（古典制御）：入出力関係をラプラス変換で記述
- **状態空間表現**（現代制御）：内部状態を含めて微分方程式で記述

本講義では、状態空間表現を中心に学びます。

## 2. 状態とは何か

### 2.1 状態の定義

**状態（state）** とは、システムの過去の履歴をすべて要約し、現在の入力と合わせて将来の挙動を完全に決定できる最小限の情報の集合です。

### 2.2 状態変数

状態を表す変数を **状態変数（state variables）** と呼び、ベクトルとしてまとめて表記します：

$$\mathbf{x}(t) = \begin{bmatrix} x_1(t) \\ x_2(t) \\ \vdots \\ x_n(t) \end{bmatrix}$$

ここで $n$ は **システムの次数** と呼ばれます。

## 3. 状態空間表現の基本形

### 3.1 連続時間システム

線形時不変（LTI: Linear Time-Invariant）システムの状態空間表現は以下の形式で与えられます：

$$\dot{\mathbf{x}}(t) = A\mathbf{x}(t) + B\mathbf{u}(t)$$
$$\mathbf{y}(t) = C\mathbf{x}(t) + D\mathbf{u}(t)$$

ここで：
- $\mathbf{x}(t) \in \mathbb{R}^n$：状態ベクトル
- $\mathbf{u}(t) \in \mathbb{R}^m$：入力ベクトル
- $\mathbf{y}(t) \in \mathbb{R}^p$：出力ベクトル
- $A \in \mathbb{R}^{n \times n}$：システム行列（状態行列）
- $B \in \mathbb{R}^{n \times m}$：入力行列
- $C \in \mathbb{R}^{p \times n}$：出力行列
- $D \in \mathbb{R}^{p \times m}$：直達行列

## 4. 物理システムからの導出例

### 4.1 例1：RLC回路

直列RLC回路を考えます。キルヒホッフの電圧則より：

$$L\frac{di}{dt} + Ri + \frac{1}{C}\int i \, dt = v(t)$$

状態変数として電荷 $q$ と電流 $i$ を選ぶと：

$$\begin{bmatrix} \dot{q} \\ \dot{i} \end{bmatrix} = \begin{bmatrix} 0 & 1 \\ -\frac{1}{LC} & -\frac{R}{L} \end{bmatrix} \begin{bmatrix} q \\ i \end{bmatrix} + \begin{bmatrix} 0 \\ \frac{1}{L} \end{bmatrix} v$$

### 4.2 例2：質量-ばね-ダンパ系

運動方程式：$m\ddot{y} + c\dot{y} + ky = f(t)$

状態変数 $x_1 = y$、$x_2 = \dot{y}$ とすると：

$$\begin{bmatrix} \dot{x}_1 \\ \dot{x}_2 \end{bmatrix} = \begin{bmatrix} 0 & 1 \\ -\frac{k}{m} & -\frac{c}{m} \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} + \begin{bmatrix} 0 \\ \frac{1}{m} \end{bmatrix} f$$

## 5. 状態空間表現の特徴

### 5.1 利点

1. **多入力多出力（MIMO）システム** を自然に扱える
2. **非線形システム** への拡張が容易
3. **内部状態** の情報が得られる
4. **数値計算** に適している
5. **最適制御** などの高度な設計法との親和性が高い

### 5.2 状態変数の非一意性

座標変換 $\mathbf{z} = T\mathbf{x}$ により異なる表現が得られます：

$$\dot{\mathbf{z}} = TAT^{-1}\mathbf{z} + TB\mathbf{u}$$

## 6. まとめ

- 状態空間表現は現代制御理論の基礎
- システムを $\dot{\mathbf{x}} = A\mathbf{x} + B\mathbf{u}$、$\mathbf{y} = C\mathbf{x} + D\mathbf{u}$ の形式で記述
- 物理システムから系統的に導出可能
