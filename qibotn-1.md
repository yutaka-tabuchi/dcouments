2024/10/24-27

- QiboTensornetwork ���g������
    * ���s
- Hello QiboTensornetwork
- �X�s�����̗�N��ԓ`��
    * Quimb�ɂ����s (���s)
    * numpy �o�b�N�G���h�ɂ����s
- Quimb�ɂ����s
    * iSWAP�Q�[�g��1�ʎq�r�b�g�ւ̕���
    * Quimb �ɂ��X�s������XX+YY���ݍ�p�ɂ�鎞�Ԕ��W
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

�l�ł�NVIDIA�̃n�[�h�E�F�A�������Ă��Ȃ����߁A[Quimb](https://quimb.readthedocs.io/en/latest/index.html) (quantum information many-body) ���g�����Ƃɂ��܂��B
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

`computation_settings` �̓o�b�N�G���h�̓�����w�肵�܂��B`qibotn.backends.quimb` �̃\�[�X�v���O������ǂ߂Ε�����̂ł����AQuimb �ł� MPI����A[NCCL](https://developer.nvidia.com/nccl) (NVIDIA Collective Communications Library)�A���Ғl�v�Z�͎g�����Ƃ��ł����Anumpy�x�[�X��Quimb�݂̂��g�����Ƃ��ł��܂��B���̏ꍇ�ɂ̓e���\���̏k����Ƃ����Ō�� `2^num_of_qubits x 16 byte` �̏�ԃx�N�g�����K�v�ɂȂ�܂��B20�r�b�g��16 MByte�A30�r�b�g��16 GByte�ł��̂ŁA50�ʎq�r�b�g�͖��������ł��ˁB���x�N�g���\���������Ȃ����GHZ��Ԃ̕\���͑債�����ƂȂ��̂ł����A�������������ɂȂ��Ă���悤�ł��B

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
Upropagator  = scipy.linalg.expm(-1j * 2 * numpy.pi * Hinteraction * dt )

number_of_qubits = 21
number_of_rounds = 256

packets = []
for i in range( 0, number_of_rounds, 8 ):
  excitation = spin_propagation( number_of_qubits, i, Upropagator )
  packets.append( excitation )

pl.pcolor( numpy.array( packets ))
pl.savefig( 'qibotn-10.svg' )
```

2�ʎq�r�b�g��XX+YY���ݍ�p���������x�ɑ΂���1/128�������Ԕ��W������ `Upropagator` �����܂��B���� `Upropagator` ��ʎq�r�b�g�Ɍ݂��Ⴂ�ɂȂ�悤�Ɉ�����āA`H_int` ���S�X�s���ɑ΂��ē����Ɉ������銴�����؃g���b�^�[�����ɂ��������܂�(���}���Q�ƁBU��XX+YY��1/128�������Ԕ��W���鉉�Z�q)�B

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

��H���ŏ������蒼���Ȃ���X�s�����̎��Ԕ��W��ǂ�������̂ł͂Ȃ��A�k����Ƃ������x�N�g���������l�ɂ��� `H_int` �����Ԕ��W�������ق��������I�������Ɣ��Ȃ��܂����B

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

# Quimb�ɂ����s

NVidia ��GPU���g���Ȃ����� QiboTensornetwork �ւ̋����������Ă���̂ł����AQuimb�Ŏ��s�ł��Ȃ��͎̂₵�����߁A�Ō�̂������Ƃ���2�ʎq�r�b�g��XX+YY�̎��Ԕ��W���Z�q `Upropagator` �� iSWAP�Q�[�g��1�ʎq�r�b�g��]�ɕ������܂��B

## iSWAP�Q�[�g��1�ʎq�r�b�g�ւ̕���

### iSWAP�Q�[�g�̒�`�̊m�F
�܂��� iSWAP �Q�[�g�� qibo �ł�����ƒ�`����Ă��邩�m�F���܂��B��Ԃ̌v�Z�����ł��Ȃ������ȃV�~�����[�^��p���Ď��Ԕ��W���Z�q(���j�^���s��)���m�F�������ꍇ�ɂ́A�ő�G���^���O����� (MES)�܂��̓x���΂��g���ă��x����t����ƕ֗��ł��B�ő�G���^���O����Ԃ̓e���\���l�b�g���[�N�ł͂����̖_���Ȃ̂ŁA�s��̓��͑��̃C���f�b�N�X���x���Ƃ��ėp���邱�Ƃ��ł��܂��B�e���\���l�b�g���[�N�ł͗ʎq�r�b�g���͂��܂�C�ɂȂ�Ȃ��̂�(?)�A�V�X�e���T�C�Y��2�{�ɂȂ낤���֗��ɉz�������Ƃ͂���܂���B
```
c = qibo.Circuit( 4 )
c.add( qibo.gates.H( 0 ))
c.add( qibo.gates.H( 1 ))
c.add( qibo.gates.CNOT( 0, 2 ))
c.add( qibo.gates.CNOT( 1, 3 ))
c.add( qibo.gates.iSWAP( 0, 1 )) # <- TARGET UNITARY OP
c().state().reshape( 4, 4 ) * 2

#           +-----+
#   +--0 -- |  U  |---
# +-| -1 -- |     |---
# | |       +-----+
# | |
# | +--2--------------
# +----3--------------
```

iSWAP�̍s��ł���(�s��̒��̕�����+i�Ȃ̂�-i�Ȃ̂��C�ɂȂ��Ă��܂���)�B
```
array([[1.+0.j, 0.+0.j, 0.+0.j, 0.+0.j],
       [0.+0.j, 0.+0.j, 0.+1.j, 0.+0.j],
       [0.+0.j, 0.+1.j, 0.+0.j, 0.+0.j],
       [0.+0.j, 0.+0.j, 0.+0.j, 1.+0.j]])
```

### iSWAP�Q�[�g�̃G�R�[����

�Q�[�g�E�G(�j���C����)�̊��ł�iSWAP�́A���X��iSWAP��Z���]���T���h�C�b�`����iSWAP�ŏ�����͂��B
```
c = qibo.Circuit( 4 )
c.add( qibo.gates.H( 0 ))
c.add( qibo.gates.H( 1 ))
c.add( qibo.gates.CNOT( 0, 2 ))
c.add( qibo.gates.CNOT( 1, 3 ))
c.add( qibo.gates.iSWAP( 0, 1 )) # <- TARGET
c.add( qibo.gates.Z( 0 ))        # <- TARGET
c.add( qibo.gates.iSWAP( 0, 1 )) # <- TARGET
c.add( qibo.gates.Z( 0 ))        # <- TARGET
c().state().reshape( 4, 4 ) * 2

#
#   +--0 -- x---Z-x-Z---
#   |       |     |
# +-| -1 -- x-----x-----
# | |
# | |
# | +--2----------------
# +----3----------------
```

�����܂����B
```
array([[1.+0.j, 0.+0.j, 0.+0.j, 0.+0.j],
       [0.+0.j, 1.+0.j, 0.+0.j, 0.+0.j],
       [0.+0.j, 0.+0.j, 1.+0.j, 0.+0.j],
       [0.+0.j, 0.+0.j, 0.+0.j, 1.+0.j]])
```

### ����iSWAP���Ԕ��W

���Ƃ�iSWAP��1��̏ꍇ�ƁA�ʑ����]�ŋ��ݍ���iSwap��p���ăL�����Z�������ꍇ�Ƃ̒��ԏ�Ԃ��l���܂��BXX+YY�����ꂼ��Z�ɐQ������悤�Ɋ������A�ŏ��ƍŌ�̈ʑ��̈ʑ��𒲐�����Ǝ��̂悤�ȉ�H�ŔC�ӂ�Identity �` iSwap��⊮���邱�Ƃ��ł��܂��B������ x = 0.5 ��iSwap�A0.25��sqrt(iSwap)�ƂȂ�܂��B
```
    -- sqrtY' --x - Uy(  x ) - Z - x - Z - sqrtY --
                |                  |
    -- sqrtX  --x --Ux( -x )------ x ----- sqrtX'--
```

��̉�H�̂悤�� iSWAP��p����`Upropagator` ( `Hinteraction` �̔������Ԕ��W) �̕����ɂ����āA1�ʎq�r�b�g�Q�[�g�̉�]�p�𒲂ׂ�葱�� `find_tuning_angle()`���`���Ă����܂��B�܂���H�� `Upropagator` ����������葱�� `add_small_iSwap()` ���L�q���Ă����܂��B`RX`�̉�]�p�� `pi/2` ��^�����Z����-Y���ɓ|���悤�ȉ�]�̂悤�ł��B
```
def find_tuning_angle( Utarget : numpy.ndarray, Uisw : numpy.ndarray ) -> float:

    def costf( x ):

        #  -- sqrtY' --x - Uy(  x ) - Z - x - Z - sqrtY -->
        #              |                  |
        #  -- sqrtX  --x --Ux( -x )------ x ----- sqrtX'-->

        Ut =   numpy.kron(       Uy( 0.5 ) @ sz,  Ux( -0.5 )) @ Uisw \
             @ numpy.kron( sz  @ Uy(  x  )     ,  Ux(  -x  )) @ Uisw \
             @ numpy.kron(       Uy(-0.5 )     ,  Ux(  0.5 ))
        return -numpy.real( numpy.trace( Ut @ numpy.conj( Utarget )))

    Ux = lambda phi :  scipy.linalg.expm( -0.5j * numpy.pi * phi * sx )
    Uy = lambda phi :  scipy.linalg.expm( -0.5j * numpy.pi * phi * sy )

    while True:
        x0 = numpy.random.rand()
        result = scipy.optimize.minimize( costf, x0 )
        check  = costf( x0 )
        if abs( check + 4.0 ) < 0.001:
            break
    return result.x

def add_small_iSwap( circuit : qibo.Circuit, qubit_i : int, qubit_j : int, angle : float ) -> qibo.Circuit:

    circuit.add( qibo.gates.RY( qubit_i, -0.5 * numpy.pi ))
    circuit.add( qibo.gates.RX( qubit_j,  0.5 * numpy.pi ))
    circuit.add( qibo.gates.iSWAP( qubit_i, qubit_j ))

    circuit.add( qibo.gates.RY( qubit_i,  angle * numpy.pi ))
    circuit.add( qibo.gates.RX( qubit_j, -angle * numpy.pi ))

    circuit.add( qibo.gates.Z( qubit_i ))
    circuit.add( qibo.gates.iSWAP( qubit_i, qubit_j ))
    circuit.add( qibo.gates.Z( qubit_i ))

    circuit.add( qibo.gates.RY( qubit_i,  0.5 * numpy.pi ))
    circuit.add( qibo.gates.RX( qubit_j, -0.5 * numpy.pi ))

    return circuit
```

`Upropagator` �ƕ���������H���r���ĊȒP�Ɋm�F�����Ă����܂��B�ŏ��̐��s�ł́A�������s���葱�� `find_tuning_angle()` �ɕK�v�� iSWAP�Q�[�g�̃��j�^���\���𐶐����Ă��܂��B
```
c = qibo.Circuit( 4 )                                       # define UiSwap
c.add( qibo.gates.H( 0 ))                                   # through a set of 
c.add( qibo.gates.H( 1 ))                                   # Bell pairs
c.add( qibo.gates.CNOT( 0, 2 ))
c.add( qibo.gates.CNOT( 1, 3 ))
c.add( qibo.gates.iSWAP( 0, 1 ))
UiSwap       = c().state().reshape( 4, 4 ) * 2.0
                                                            # define Upropagator
Upropagator  = scipy.linalg.expm(-1j * 2 * numpy.pi * Hinteraction * dt ) 
angle        = find_tuning_angle( Upropagator, UiSwap )

c = qibo.Circuit( 4 )                                       # Bell pair creation
c.add(qibo.gates.H(0))
c.add(qibo.gates.H(1))
c.add(qibo.gates.CNOT(0,2))
c.add(qibo.gates.CNOT(1,3))

c = add_small_iSwap( c, 0, 1, angle )                       # Upropagator implementation
                                                            # using decomposed gates
print( c.diagram() )
print( c().state().reshape((4,4)) * 2 @ numpy.conj( Upropagator.T ))
```

���ʂ͎��̒ʂ�ł��B�ŏ��̃A�_�}�[����CNOT�̓x���΂𐶐����Ă��镔���ł��B���̉�H�}���� `Upropagator` ������RX(RY)����\������Ă���l�q���킩��܂��B�܂�����O��̎��Ԕ��W���Z�q�� `Udecomposed Upropagator^dagger` �͍P�����Z�q�ƂȂ��Ă��邱�Ƃ��炤�܂��������ł��Ă���悤�ł��B
```
q0: --H--o-------RY--i--RY--Z--i--Z----RY---
q1: --H--|---o---RX--i--RX-----i-------RX---
q2: -----X---|------------------------------
q3: ---------X------------------------------

[[1.+0.00000000e+00j 0.+0.00000000e+00j 0.+0.00000000e+00j  0.+0.00000000e+00j]
 [0.+0.00000000e+00j 1.+0.00000000e+00j 0.+1.84198454e-08j  0.+0.00000000e+00j]
 [0.+0.00000000e+00j 0.+1.84198454e-08j 1.+0.00000000e+00j  0.+0.00000000e+00j]
 [0.+0.00000000e+00j 0.+0.00000000e+00j 0.+0.00000000e+00j  1.+0.00000000e+00j]]
```

## Quimb �ɂ��X�s������XX+YY���ݍ�p�ɂ�鎞�Ԕ��W

`numpy` �o�b�N�G���h�̍ۂɗp�����葱�� `spin_propagation()` ���� `Upropagator` �𕪉������Q�[�g��ɒu�������܂��B���Ԕ��W���Z�q `Upropagator` �╪���ɗp����p�x `angle` �̒�`�͑O�߂Ɠ����ł��B�����ł̓o�b�N�G���h�Ƃ���Quimb��ݒ肵�܂����B
```
import os

os.environ["QUIMB_NUM_PROCS"] = str( os.cpu_count() // 2 )
qibo.set_backend(backend = 'qibotn', platform = 'qutensornet' )

def spin_propagation( number_of_qubits : int, number_of_rounds : int, angle : float ) -> list:

    c = qibo.Circuit( number_of_qubits )
    c.add( qibo.gates.H( number_of_qubits // 2 ))
    for j in range( number_of_rounds ):
        for i in range( 1, number_of_qubits, 2 ):
            c = add_small_iSwap( c, i - 1, i, angle )
        for i in range( 2, number_of_qubits, 2 ):
            c = add_small_iSwap( c, i - 1, i, angle )
    print( c.diagram() )

    contr_axis          = [[ i for i in range( number_of_qubits ) if i != j ] for j in range( number_of_qubits )]
    excited_state_index = 1
    prob_tensor = c.execute().probabilities().reshape( (2,) * number_of_qubits )
    excitation = [ numpy.sum( prob_tensor, axis = tuple( ax ))[ excited_state_index ]  for ax in contr_axis ]

    return excitation

number_of_qubits = 21
number_of_rounds = 256

packets = []
for _rounds in range( 0, number_of_rounds, 8 ):
    excitation = spin_propagation( number_of_qubits, _rounds, angle )
    packets.append( excitation )

pl.pcolor( numpy.array( packets ))
pl.savefig( 'qibotn-11.svg' )
```

���x�̓Q�[�g�̎�ނȂǂŃG���[�������邱�ƂȂ����s����܂����B`numpy` �o�b�N�G���h�ɔ�׎��s���Ԃ͑����Ȃ����悤�ȋC�����܂��B�e���\���l�b�g���[�N�ɂ͑��������߂Ă���킯�ł͂Ȃ��̂ŁA����ŗǂ��Ƃ��܂��B
```
[Qibo 0.2.12|INFO|2024-10-xx xx:13:26]: Using qibotn (QuimbBackend) backend on /CPU:0
...(snip)...
q0 : ... --------------------------------------------------------------------------------------------------------------------------------------- ...
q1 : ... --------------------------------------------------------------------------------------------------------------------------------------- ...
q2 : ... --------------------------------------------------------------------------------------------------------------------------------------- ...
q3 : ... --------------------------------------------------------------------------------------------------------------------------------------- ...
q4 : ... --------------------------------------------------------------------------------------------------------------------------------------- ...
q5 : ... --------------------------------------------------------------------------------------------------------------------------------------- ...
q6 : ... --RY----------------------------------------------------------------------------------------------------------------------------------- ...
q7 : ... --------------------------------------------------------------------------------------------------------------------------------------- ...
q8 : ... --------i--RY--Z--i--Z----RY----------------------------------------------------------------------------------------------------------- ...
q9 : ... --------i--RX-----i-------RX----------------------------------------------------------------------------------------------------------- ...
q10: ... --------------------------RY--------i--RY--Z--i--Z----RY------------------------------------------------------------------------------- ...
q11: ... --------------------------RX--------i--RX------i------RX------------------------------------------------------------------------------- ...
q12: ... --------------------------------------------------------RY--------i--RY--Z--i--Z----RY------------------------------------------------- ...
q13: ... --------------------------------------------------------RX--------i--RX------i--RX----------------------------------------------------- ...
q14: ... --------------------------------------------------------------------------------------RY--------i--RY--Z--i--Z----RY------------------- ...
q15: ... --------------------------------------------------------------------------------------RX--------i--RX------i--RX----------------------- ...
q16: ... --------------------------------------------------------------------------------------------------------------------RY--------i--RY--Z- ...
q17: ... --------------------------------------------------------------------------------------------------------------------RX--------i--RX---- ...
q18: ... --------------------------------------------------------------------------------------------------------------------------------------- ...
q19: ... --------------------------------------------------------------------------------------------------------------------------------------- ...
q20: ... --------------------------------------------------------------------------------------------------------------------------------------- ...
```
![](./qibotn-11.svg)

# �܂Ƃ�

�����l�K�e�B�u�Ȃ܂Ƃ߂ƂȂ�܂����A���̒ʂ�ł��B

- NVIDIA �̃A�N�Z�����[�^��p���Ȃ��Ƃ��܂胁���b�g�������Ȃ��ł��B�d�Ԃ̒���o��Ńv���O���~���O������l�ɂ͕s�������Ǝv���܂��B
- Quimb�̃��b�p�[(Wrapper)�̂悤�ɂȂ��Ă��邽�߁A�e���\���̕\���⌋������(�{���h����)���ǂ��Ȃ��Ă���̂��m�F���邱�Ƃ��ł��܂���B�������x�N�g�������o�͂���Ȃ����߁A�璷�ȕ\���ɂ��g����ʎq�r�b�g�����z���菭�Ȃ��\��������܂��B���������჌�x���ő��삵�����l�ɂ͕s�����ł��B
- Qibo���g���K�v�͂Ȃ��AQuimb �� Tensornetwork �𒼐ڑ��삵���ق����ǂ��C�����Ă��܂��B
- Tensornetwork �̂悤�Ɏ����ō\����݌v����K�v���Ȃ��_�ɂ��Ă͕֗��ł��B

# �����N

- [Qibotn](https://github.com/qiboteam/qibotn)
- [Quimb](https://quimb.readthedocs.io/en/latest/index.html) (quantum information many-body)
- NVIDIA Collective Communications Library: [NCCL](https://developer.nvidia.com/nccl)
