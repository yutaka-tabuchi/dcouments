2024/10/27

- はじめての Quimb
    * インストール
    * 回路シミュレーターとして何ができるのか
        - SU4
- リンク

# はじめての Quimb

[Quimb](https://quimb.readthedocs.io/en/latest/index.html)は量子情報の多体系のテンソルネットワークライブラリのようです。

## インストール

```
$ pipenv install quimb
```

```
import quimb
```

## 回路シミュレーターとしてどんなゲートが実装できるのか

後にやりたいことができないことが判ると悲しいため、最初に使えるそうな2量子ビットゲートを調べておきます。
```
print(quimb.tensor.circuit.TWO_QUBIT_GATES)
```

なんでも出来そうな2量子ビットゲートとしては、`SU4`あたりですね。
```
{'CNOT', 'CRX', 'CRY', 'CRZ', 'CU1', 'CU2', 'CU3', 'CX', 'CY', 'CZ', 'FS', 'FSIM', 'FSIMG', 'GIVENS', 'IS', 'ISWAP', 'RXX', 'RYY', 'RZZ', 'SU4', 'SWAP'}
```

そういえば回路の途中での測定または射影演算子が見当たりません。毎回新しい量子ビットをくっつけて最後にまとめて測定するしかないのでしょう。

### SU4

```
 quimb.tensor.circuit.Circuit.su4(theta1, phi1, lamda1, theta2, phi2, lamda2, theta3, phi3, lamda3, theta4, phi4, lamda4, t1, t2, t3, i, j, gate_round=None, parametrize=False, **kwargs)

# ---- A1 ---o--- Rz(t1) ---+--------------o--- A3 ---
#            |              |              |
# ---- A2 ---+--- Ry(t2) ---o--- Ry(t3) ---+--- A4 ---

```


こちらの論文 [quant-ph/0308006](https://arxiv.org/abs/quant-ph/0308006) が引用されており、15個の1量子ビット回転と3つのCNOTから構成されるゲートとなっており、SU(4)のパラメータ表現(恐らく既約)となっています。各 `θ_i`、`φ_i`、`λ_i`は1量子ビットの回転量、`t_i` はCNOT中に挿入される回転ゲートの回転量となっています。自分で任意のSU2を印加したい場合にはこの形への変形を要する点が面倒です。`θ`、 `φ`、`λ` の表現はU3と同じであり、次のようになっています。ざっくりですが `θ` は緯度方向の回転量、`φ` が回転軸方向、`λ` は経度方向の回転量を決めるイメージです。
```
                           [             cos( theta / 2 )  -exp(j lambda)         sin( theta / 2 ) ]
 A (theta, phi, lambda) =  [                                                                       ]
                           [ exp (j phi) sin( theta / 2 )   exp(j (phi + lambda)) cos( theta / 2 ) ]
```
[前回](./qibotn-1.md)のようにネイティブゲートの1つのタイムステップを毎回この形に変形するのも面倒ですね。

# 量子回路の実装とグラフ表現

100量子ビットでGHZ状態を生成してみます。

```
%config InlineBackend.figure_formats = ['svg']

import random
import quimb
import quimb.tensor


num_qubits = 100
circuit = quimb.tensor.Circuit( num_qubits )

circuit.apply_gate('H', regs[ 0 ])
for i in range( 1, num_qubits ):
    circuit.apply_gate( 'CNOT', i - 1, i )

fig = circuit.psi.draw( color = ['PSI0', 'H', 'CNOT'], figsize = ( 10, 4 ), return_fig = True )
fig.savefig( 'quimb-10.svg' )

```
![](./quimb-10.svg)
長い鎖状のグラフが生成されました。元々状態は PSI0 で表示され、テンソルの足は `k<数字>`で表示されているようです。図では小さすぎて足が見えないようです。

## 計算と測定値

次のような計算ができるようです。

- 完全波動関数を示す密ベクトル
- 局所的な期待値または部分系の密度行列
- 周辺確率分布やシングルショットのビット列
- 状態の忠実度やユニタリ過程の忠実度

## 結果のサンプリング

結果を測定してみます。結果のビット値を頻度値でカウントすることができます。
```
import collections

number_of_samples = 128
collections.Counter( circuit.sample( number_of_samples ))
```

```
Counter({'000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000': 67,
        '111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111': 61})
```

またはビット列値を毎回生成することもできます。乱数のシード値を与えることもできるようです。
```
for _bitstring in circuit.sample( number_of_samples, seed = 42 ):                    # sample it a few times
    print( _bitstring )
```

## 局所的な期待値の測定

局所的な演算子をパウリ演算子を用いて定義します。`&`を使うとテンソル積が表現できるようです。どのビットに作用させたいのかは、`local_expectation()` の第2引数で指定します。

```
quimb.pauli('X') & quimb.pauli('X')
# [[0.+0.j 0.+0.j 0.+0.j 1.+0.j]
#  [0.+0.j 0.+0.j 1.+0.j 0.+0.j]
#  [0.+0.j 1.+0.j 0.+0.j 0.+0.j]
#  [1.+0.j 0.+0.j 0.+0.j 0.+0.j]]

circuit.local_expectation( quimb.pauli('X') & quimb.pauli('X'), ( 0, 1 ))
# 0j
```

本来であれば GHZ状態の XXX....X パリティを測定したいのですが、そもそもそんなパウリ行列すら作ることが難しいようです。100量子ビットから見ると16個のパウリXの直積は十分局所的だと思うのですが、メモリ不足だとエラーが生じてしまいました。
```
circuit.local_expectation( \
    quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & \
    quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & \
    quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & \
    quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X'),  \
    ( 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 ))
# Unable to allocate 64.0 GiB for an array with shape (65536, 65536) and data type complex128
```

# リンク
- [Quimb](https://quimb.readthedocs.io/en/latest/index.html)
- Optimal Quantum Circuits for General Two-Qubit Gates [arXiv:quant-ph/0308006](https://arxiv.org/abs/quant-ph/0308006)
- QiboTensornetwork を使いたい [yutaka-tabuchi/documents](./qibotn-1.md)
