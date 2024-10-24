2024/10/24

- QiboTensornetwork を使いたい
    * 失敗
- Hello QiboTensornetwork
- リンク

# QiboTensornetwork を使いたい

GitHubから最新版をクローンしてドキュメントの指示の通りにインストールします。`qibo 0.0.2`がインストールされました。
```
$ git clone https://github.com/qiboteam/qibotn.git qibotn
$ cd qibotn
$ pip install .
```

```
In [1]: import qibotn
In [2]: qibotn.__version__
Out[2]: '0.0.2'
```

個人ではNVIDIAのハードウェアを持っている訳ではないため、[Quimb](https://quimb.readthedocs.io/en/latest/index.html) (quantum information many-body) を使うことにします。
```
$ pipenv install quimb
```

## 失敗

pipenv からインストールする場合にはPython 3.11以上では使えないライブラリを用いているため、3.10.5の環境を作り直す必要があります。下の方法でインストールすると `qibo v0.0.1`がインストールされてしまいました。このバージョンは古く、`qibo` から `qibotn` バックエンドの読み込みのところでエラーを生じてしまいました。
```
$ pipenv install qubotn
```


# Hello QiboTensornetwork

QiboTensornetwork のサンプルを見ながら使ってみます。バックエンドは Quimb を使って計算をしてみます。テンソルネットワークは簡単に計算ができるはずなので、25量子ビットのGHZ状態を作ってみます。

```
import qibo
import os

os.environ["QUIMB_NUM_PROCS"] = str( os.cpu_count() // 2 )

computation_settings = {                # computation_settings = {
    'MPI_enabled' : False,              #     'MPI_enabled' : False,
    'MPS_enabled' : False,              #     'MPS_enabled' : False, 
    'NCCL_enabled': False,              #     'NCCL_enabled': False,
    'expectation_enabled': False,       #     'expectation_enabled': { 'pauli_string_pattern': 'IXZ' }
}                                       # }
                                        # computation_settings = { 'MPS_enabled'  : { 'method': 'svd', 'cutoff': 1e-6, 'cutoff_mode': 'abs' }}

qibo.set_backend(backend = 'qibotn', platform = 'qutensornet', runcard = computation_settings )

number_of_qubits = 25

c = qibo.Circuit( number_of_qubits )
c.add( qibo.gates.H( 0 ))
for i in range( 0, number_of_qubits - 1 ):
    c.add( qibo.gates.CNOT( i, i + 1 ))

result = c.execute()

print( c.diagram() )
print( result.state() )
```

50量子ビットにすると `RuntimeError: State does not fit in /CPU:0 memory.Please switch the execution device to a different one using qibo.set_device.` というエラーが出てしまいました。少し期待外れですが25量子ビットでは動いています。

`computation_settings` はバックエンドの動作を指定します。`qibotn.backends.quimb` のソースコードを読めば分かるのですが、Quimb では MPI並列、[NCCL](https://developer.nvidia.com/nccl) (NVIDIA Collective Communications Library)、期待値計算は使うことができず、numpyベースのQuimbのみを使うことができます。その場合にはテンソルの縮約をとった最後は `2^num_of_qubits x 16 byte` の状態ベクトルが必要になります。20ビットで16 MByte、30ビットで16 GByteですので、50量子ビットは無理そうですね。密ベクトル表現さえしなければGHZ状態の表現は大したことないはのですが、ここが足かせになっているようです。

```
q0 : ─H─o───────────────────────────────────────────────
q1 : ───X─o─────────────────────────────────────────────
q2 : ─────X─o───────────────────────────────────────────
q3 : ───────X─o─────────────────────────────────────────
q4 : ─────────X─o───────────────────────────────────────
q5 : ───────────X─o─────────────────────────────────────
q6 : ─────────────X─o───────────────────────────────────
q7 : ───────────────X─o─────────────────────────────────
q8 : ─────────────────X─o───────────────────────────────
q9 : ───────────────────X─o─────────────────────────────
q10: ─────────────────────X─o───────────────────────────
q11: ───────────────────────X─o─────────────────────────
q12: ─────────────────────────X─o───────────────────────
q13: ───────────────────────────X─o─────────────────────
q14: ─────────────────────────────X─o───────────────────
q15: ───────────────────────────────X─o─────────────────
q16: ─────────────────────────────────X─o───────────────
q17: ───────────────────────────────────X─o─────────────
q18: ─────────────────────────────────────X─o───────────
q19: ───────────────────────────────────────X─o─────────
q20: ─────────────────────────────────────────X─o───────
q21: ───────────────────────────────────────────X─o─────
q22: ─────────────────────────────────────────────X─o───
q23: ───────────────────────────────────────────────X─o─
q24: ─────────────────────────────────────────────────X─
[0.70710678+0.j 0.        +0.j 0.        +0.j ... 0.        +0.j
 0.        +0.j 0.70710678+0.j]
```


# リンク

- [Qibotn](https://github.com/qiboteam/qibotn)
- [Quimb](https://quimb.readthedocs.io/en/latest/index.html) (quantum information many-body)
- NVIDIA Collective Communications Library: [NCCL](https://developer.nvidia.com/nccl)
