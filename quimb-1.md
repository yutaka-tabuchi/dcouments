2024/10/27

- �͂��߂Ă� Quimb
    * �C���X�g�[��
    * ��H�V�~�����[�^�[�Ƃ��ĉ����ł���̂�
        - SU4
- �����N

# �͂��߂Ă� Quimb

[Quimb](https://quimb.readthedocs.io/en/latest/index.html)�͗ʎq���̑��̌n�̃e���\���l�b�g���[�N���C�u�����̂悤�ł��B

## �C���X�g�[��

```
$ pipenv install quimb
```

```
import quimb
```

## ��H�V�~�����[�^�[�Ƃ��Ăǂ�ȃQ�[�g�������ł���̂�

��ɂ�肽�����Ƃ��ł��Ȃ����Ƃ�����Ɣ߂������߁A�ŏ��Ɏg���邻����2�ʎq�r�b�g�Q�[�g�𒲂ׂĂ����܂��B
```
print(quimb.tensor.circuit.TWO_QUBIT_GATES)
```

�Ȃ�ł��o��������2�ʎq�r�b�g�Q�[�g�Ƃ��ẮA`SU4`������ł��ˁB
```
{'CNOT', 'CRX', 'CRY', 'CRZ', 'CU1', 'CU2', 'CU3', 'CX', 'CY', 'CZ', 'FS', 'FSIM', 'FSIMG', 'GIVENS', 'IS', 'ISWAP', 'RXX', 'RYY', 'RZZ', 'SU4', 'SWAP'}
```

���������Ή�H�̓r���ł̑���܂��͎ˉe���Z�q����������܂���B����V�����ʎq�r�b�g���������čŌ�ɂ܂Ƃ߂đ��肷�邵���Ȃ��̂ł��傤�B

### SU4

```
 quimb.tensor.circuit.Circuit.su4(theta1, phi1, lamda1, theta2, phi2, lamda2, theta3, phi3, lamda3, theta4, phi4, lamda4, t1, t2, t3, i, j, gate_round=None, parametrize=False, **kwargs)

# ---- A1 ---o--- Rz(t1) ---+--------------o--- A3 ---
#            |              |              |
# ---- A2 ---+--- Ry(t2) ---o--- Ry(t3) ---+--- A4 ---

```


������̘_�� [quant-ph/0308006](https://arxiv.org/abs/quant-ph/0308006) �����p����Ă���A15��1�ʎq�r�b�g��]��3��CNOT����\�������Q�[�g�ƂȂ��Ă���ASU(4)�̃p�����[�^�\��(���炭����)�ƂȂ��Ă��܂��B�e `��_i`�A`��_i`�A`��_i`��1�ʎq�r�b�g�̉�]�ʁA`t_i` ��CNOT���ɑ}��������]�Q�[�g�̉�]�ʂƂȂ��Ă��܂��B�����ŔC�ӂ�SU2������������ꍇ�ɂ͂��̌`�ւ̕ό`��v����_���ʓ|�ł��B`��`�A `��`�A`��` �̕\����U3�Ɠ����ł���A���̂悤�ɂȂ��Ă��܂��B��������ł��� `��` �͈ܓx�����̉�]�ʁA`��` ����]�������A`��` �͌o�x�����̉�]�ʂ����߂�C���[�W�ł��B
```
                           [             cos( theta / 2 )  -exp(j lambda)         sin( theta / 2 ) ]
 A (theta, phi, lambda) =  [                                                                       ]
                           [ exp (j phi) sin( theta / 2 )   exp(j (phi + lambda)) cos( theta / 2 ) ]
```
[�O��](./qibotn-1.md)�̂悤�Ƀl�C�e�B�u�Q�[�g��1�̃^�C���X�e�b�v�𖈉񂱂̌`�ɕό`����̂��ʓ|�ł��ˁB

# �ʎq��H�̎����ƃO���t�\��

100�ʎq�r�b�g��GHZ��Ԃ𐶐����Ă݂܂��B

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
��������̃O���t����������܂����B���X��Ԃ� PSI0 �ŕ\������A�e���\���̑��� `k<����>`�ŕ\������Ă���悤�ł��B�}�ł͏��������đ��������Ȃ��悤�ł��B

## �v�Z�Ƒ���l

���̂悤�Ȍv�Z���ł���悤�ł��B

- ���S�g���֐����������x�N�g��
- �Ǐ��I�Ȋ��Ғl�܂��͕����n�̖��x�s��
- ���ӊm�����z��V���O���V���b�g�̃r�b�g��
- ��Ԃ̒����x�⃆�j�^���ߒ��̒����x

## ���ʂ̃T���v�����O

���ʂ𑪒肵�Ă݂܂��B���ʂ̃r�b�g�l��p�x�l�ŃJ�E���g���邱�Ƃ��ł��܂��B
```
import collections

number_of_samples = 128
collections.Counter( circuit.sample( number_of_samples ))
```

```
Counter({'000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000': 67,
        '111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111': 61})
```

�܂��̓r�b�g��l�𖈉񐶐����邱�Ƃ��ł��܂��B�����̃V�[�h�l��^���邱�Ƃ��ł���悤�ł��B
```
for _bitstring in circuit.sample( number_of_samples, seed = 42 ):                    # sample it a few times
    print( _bitstring )
```

## �Ǐ��I�Ȋ��Ғl�̑���

�Ǐ��I�ȉ��Z�q���p�E�����Z�q��p���Ē�`���܂��B`&`���g���ƃe���\���ς��\���ł���悤�ł��B�ǂ̃r�b�g�ɍ�p���������̂��́A`local_expectation()` �̑�2�����Ŏw�肵�܂��B

```
quimb.pauli('X') & quimb.pauli('X')
# [[0.+0.j 0.+0.j 0.+0.j 1.+0.j]
#  [0.+0.j 0.+0.j 1.+0.j 0.+0.j]
#  [0.+0.j 1.+0.j 0.+0.j 0.+0.j]
#  [1.+0.j 0.+0.j 0.+0.j 0.+0.j]]

circuit.local_expectation( quimb.pauli('X') & quimb.pauli('X'), ( 0, 1 ))
# 0j
```

�{���ł���� GHZ��Ԃ� XXX....X �p���e�B�𑪒肵�����̂ł����A������������ȃp�E���s�񂷂��邱�Ƃ�����悤�ł��B100�ʎq�r�b�g���猩���16�̃p�E��X�̒��ς͏\���Ǐ��I���Ǝv���̂ł����A�������s�����ƃG���[�������Ă��܂��܂����B
```
circuit.local_expectation( \
    quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & \
    quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & \
    quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & \
    quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X') & quimb.pauli('X'),  \
    ( 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 ))
# Unable to allocate 64.0 GiB for an array with shape (65536, 65536) and data type complex128
```

# �����N
- [Quimb](https://quimb.readthedocs.io/en/latest/index.html)
- Optimal Quantum Circuits for General Two-Qubit Gates [arXiv:quant-ph/0308006](https://arxiv.org/abs/quant-ph/0308006)
- QiboTensornetwork ���g������ [yutaka-tabuchi/documents](./qibotn-1.md)
