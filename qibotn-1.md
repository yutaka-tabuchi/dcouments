2024/10/24

- QiboTensornetwork ���g������
    * ���s
- Hello QiboTensornetwork
- �X�s�����̗�N��ԓ`��
    * Quimb�ɂ����s (���s)
    * numpy �o�b�N�G���h�ɂ����s
- �����N

# QiboTensornetwork ���g������

GitHub����ŐV�ł��N���[�����ăh�L�������g�̎w���̒ʂ�ɃC���X�g�[�����܂��B`qibo 0.0.2`���C���X�g�[������܂����B
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

�l�ł�NVIDIA�̃n�[�h�E�F�A�������Ă����ł͂Ȃ����߁A[Quimb](https://quimb.readthedocs.io/en/latest/index.html) (quantum information many-body) ���g�����Ƃɂ��܂��B
```
$ pipenv install quimb
```

## ���s

pipenv ����C���X�g�[������ꍇ�ɂ�Python 3.11�ȏ�ł͎g���Ȃ����C�u������p���Ă��邽�߁A3.10.5�̊�����蒼���K�v������܂��B���̕��@�ŃC���X�g�[������� `qibo v0.0.1`���C���X�g�[������Ă��܂��܂����B���̃o�[�W�����͌Â��A`qibo` ���� `qibotn` �o�b�N�G���h�̓ǂݍ��݂̂Ƃ���ŃG���[�𐶂��Ă��܂��܂����B
```
$ pipenv install qubotn
```


# Hello QiboTensornetwork

QiboTensornetwork �̃T���v�������Ȃ���g���Ă݂܂��B�o�b�N�G���h�� Quimb ���g���Čv�Z�����Ă݂܂��B�e���\���l�b�g���[�N�͊ȒP�Ɍv�Z���ł���͂��Ȃ̂ŁA25�ʎq�r�b�g��GHZ��Ԃ�����Ă݂܂��B

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

50�ʎq�r�b�g�ɂ���� `RuntimeError: State does not fit in /CPU:0 memory.Please switch the execution device to a different one using qibo.set_device.` �Ƃ����G���[���o�Ă��܂��܂����B�������ҊO��ł���25�ʎq�r�b�g�ł͓����Ă��܂��B

`computation_settings` �̓o�b�N�G���h�̓�����w�肵�܂��B`qibotn.backends.quimb` �̃\�[�X�R�[�h��ǂ߂Ε�����̂ł����AQuimb �ł� MPI����A[NCCL](https://developer.nvidia.com/nccl) (NVIDIA Collective Communications Library)�A���Ғl�v�Z�͎g�����Ƃ��ł����Anumpy�x�[�X��Quimb�݂̂��g�����Ƃ��ł��܂��B���̏ꍇ�ɂ̓e���\���̏k����Ƃ����Ō�� `2^num_of_qubits x 16 byte` �̏�ԃx�N�g�����K�v�ɂȂ�܂��B20�r�b�g��16 MByte�A30�r�b�g��16 GByte�ł��̂ŁA50�ʎq�r�b�g�͖��������ł��ˁB���x�N�g���\���������Ȃ����GHZ��Ԃ̕\���͑債�����ƂȂ��̂ł����A�������������ɂȂ��Ă���悤�ł��B

```
q0 : ��H��o����������������������������������������������������������������������������������������������
q1 : ������X��o������������������������������������������������������������������������������������������
q2 : ����������X��o��������������������������������������������������������������������������������������
q3 : ��������������X��o����������������������������������������������������������������������������������
q4 : ������������������X��o������������������������������������������������������������������������������
q5 : ����������������������X��o��������������������������������������������������������������������������
q6 : ��������������������������X��o����������������������������������������������������������������������
q7 : ������������������������������X��o������������������������������������������������������������������
q8 : ����������������������������������X��o��������������������������������������������������������������
q9 : ��������������������������������������X��o����������������������������������������������������������
q10: ������������������������������������������X��o������������������������������������������������������
q11: ����������������������������������������������X��o��������������������������������������������������
q12: ��������������������������������������������������X��o����������������������������������������������
q13: ������������������������������������������������������X��o������������������������������������������
q14: ����������������������������������������������������������X��o��������������������������������������
q15: ��������������������������������������������������������������X��o����������������������������������
q16: ������������������������������������������������������������������X��o������������������������������
q17: ����������������������������������������������������������������������X��o��������������������������
q18: ��������������������������������������������������������������������������X��o����������������������
q19: ������������������������������������������������������������������������������X��o������������������
q20: ����������������������������������������������������������������������������������X��o��������������
q21: ��������������������������������������������������������������������������������������X��o����������
q22: ������������������������������������������������������������������������������������������X��o������
q23: ����������������������������������������������������������������������������������������������X��o��
q24: ��������������������������������������������������������������������������������������������������X��
[0.70710678+0.j 0.        +0.j 0.        +0.j ... 0.        +0.j
 0.        +0.j 0.70710678+0.j]
```

# �X�s�����̗�N��ԓ`��

���ɂ�邱�Ƃ��Ȃ��̂ŁA�ʎq�r�b�g���X�s���ƌ����Ăė�N��`�������Ă݂܂��B���ݍ�p�� `H_int = ��_<i,i+1> { X_i X_(i+1) + Y_i Y_(i+1) } / 2` �Ƃ��āA1�����X�s�����̒������N���܂��B��������̗�N�̓`���̗l�q�����Ă݂邱�Ƃɂ��܂��B�����������ݍ�p�͋Ǐ��I�ł�����������傫�����邱�Ƃ��Ȃ��̂ŁA�������ƂȂ�܂��B

```
import qibo
import numpy
import scipy.linalg
import matplotlib.pylab as pl

sp = numpy.array( [[ 0, 1 ], [ 0, 0 ]] )
sm = sp.T
sx = sp + sm; sz = sp @ sm - sm @ sp; sy = ( sz @ sx - sx @ sz ) / 2j

def spin_propagation( number_of_qubits : int, number_of_rounds : int, Upropagator : numpy.ndarray ) -> list:

    c = qibo.Circuit( number_of_qubits )
    c.add( qibo.gates.H( number_of_qubits // 2 ))
    for j in range( number_of_rounds ):
        for i in range( 1, number_of_qubits, 2 ):
            c.add( qibo.gates.Unitary( Upropagator, i - 1, i ))
        for i in range( 2, number_of_qubits, 2 ):
            c.add( qibo.gates.Unitary( Upropagator, i - 1, i ))
    print( c.diagram() )

    contr_axis          = [[ i for i in range( number_of_qubits ) if i != j ] for j in range( number_of_qubits )]
    excited_state_index = 1

    prob_tensor = c.execute().probabilities().reshape( (2,) * number_of_qubits )
    excitation = [ numpy.sum( prob_tensor, axis = tuple( ax ))[ excited_state_index ]  for ax in contr_axis ]

    return excitation

dt           = 1/128
Hinteraction = 0.5 * numpy.kron( sx, sx ) + 0.5 * numpy.kron( sy, sy )  # ( XX + YY ) / 2
     # equivalent to numpy.kron( sp, sm ) +       numpy.kron( sm, sp )
Upropagator  = scipy.linalg.expm( 1j * 2 * numpy.pi * Hinteraction * dt )

number_of_qubits = 21
number_of_rounds = 256

packets = []
for i in range( 0, number_of_rounds, 8 ):
  excitation = spin_propagation( number_of_qubits, i, Upropagator )
  packets.append( excitation )

pl.pcolor( numpy.array( packets ))
pl.savefig( 'qibotn-10.svg' )
```

2�ʎq�r�b�g��XX+YY���ݍ�p���������x�ɑ΂���1/128�������Ԕ��W������ `U_propagator` �����܂��B�ʎq�r�b�g�Ɍ݂��Ⴂ�ɂȂ�悤�Ɉ�����āA`H_int` ���S�X�s���ɑ΂��ē����Ɉ������銴�����؃g���b�^�[�����ɂ��������܂�(���}���Q�ƁBU��XX+YY��1/128�������Ԕ��W���鉉�Z�q)�B

```
q0 :  ------U------------------------
q1 :  ------U----------------U-------
q2 :  ----------U------------U-------
q3 :  ----------U----------------U---
q4 :  ------U--------------------U---
q5 :  ------U----------------U-------
q6 :  ----------U------------U-------
q7 :  ----------U----------------U---
q8 :  ------U--------------------U---
q9 :  ------U----------------U-------
q10:  --H-------U------------U-------
q11:  ----------U----------------U---
q12:  ------U--------------------U---
q13:  ------U----------------U-------
q14:  ----------U------------U-------
q15:  ----------U----------------U---
q16:  ------U--------------------U---
q17:  ------U----------------U-------
q18:  ----------U------------U-------
q19:  ----------U----------------U---
q20:  ---------------------------U---
```

`c.execute()`�ɂ���H�����s����A`.probabilities()`�ɂ��`2^number_of_qubits`�����̐�L���̃x�N�g���������܂��B�ʎq�r�b�g���Ƃ̐�L���𓾂邽�߂ɁA���̃x�N�g���� `number_of_qubits` �K�̃e���\���� `reshape()` ���Ă����܂��B`prob_tensor[i0, i1, ..., i_(number_of_qubits-1)]` �̃e���\���́A�������Ȃ������ɑ΂��Ęa���Ƃ�Ƃ��̎��ӊm�����z�𓾂܂��B�g���[�X�A�E�g���ׂ��e���\���̑� `contr_axis` ���g���āA�e�ʎq�r�b�g�̐�L���𓾂�v���O�����ƂȂ��Ă��܂��B

��H���ŏ������蒼���Ȃ���X�s�����̎��Ԕ��W��ǂ�������̂ł͂Ȃ��A�k����Ƃ������x�N�g���������l�ɂ��� `H_int` �����Ԕ��W�������ق��������I���������Ȃ��܂����B

## Quimb�ɂ����s (���s)

���̃v���O���������s���悤�Ƃ����Ƃ���A`qibo.gates.Unitary` �ɃG���[���o�Ă��܂��܂����B�ǂ���� Quimb �̎��s�� `quimb.tensor.circuit.Circuit.from_openqasm2_str()` �ɗ����Ă���悤�ŁAQASM��`qibo.gates.Unitary` �� `qibo.gates.fSim` �Ȃǂ��T�|�[�g���Ă��Ȃ��ƌ����Ă��܂��܂��B2�ʎq�r�b�g�Q�[�g�̕\���Ƃ��āA���Ȃ�n��ł��ˁB�l�C�e�B�u�Q�[�g�̃V�~�����[�V�����Ɏg�����Ǝv�����̂ŁA��������ł��B

```
[Qibo 0.2.12|INFO|2024-10-xx xx:16:45]: Using qibotn (QuimbBackend) backend on /CPU:0
[Qibo 0.2.12|ERROR|2024-10-xx xx:17:52]: Unitary is not supported by OpenQASM

NotImplementedError: Unitary is not supported by OpenQASM
```

## numpy �o�b�N�G���h�ɂ����s

�Ë����� numpy �o�b�N�G���h�ɂ����s���Ă݂܂��B
```
qibo.set_backend(backend = 'numpy')
```

```
[Qibo 0.2.12|INFO|2024-10-xx xx:18:40]: Using numpy backend on /CPU:0
```

![](./qibotn-10.svg)

�����ɃX�s�����̔ԍ��A�c���Ɏ��ԃX�e�b�v �� 8�A�F���ɐ�L����\�����Ă��܂��B���ԃX�e�b�v�͕ω����ɂ₩�Ȃ̂�1/8���x�ɊԈ����ĕ\�����Ă��܂��B�����ɗ�N���ꂽ�X�s�������Ԕ��W�ɂ����͂ɍL�����Ă����̂��悭�킩��܂��B

## Quimb�ɂ����s




# �����N

- [Qibotn](https://github.com/qiboteam/qibotn)
- [Quimb](https://quimb.readthedocs.io/en/latest/index.html) (quantum information many-body)
- NVIDIA Collective Communications Library: [NCCL](https://developer.nvidia.com/nccl)
