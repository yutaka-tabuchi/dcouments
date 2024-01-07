# TOC
gitlab -> github
# 量子計算
- A fault-tolerant one-way quantum computer, R. Raussendorf (2008)
- Introduction to Quantum Noise, Measurement and Ampli?cation, A.A. Clerk, (2010) arXiv:0810.4729v2
- Elucidating reaction mechanisms on quantum computers, Matthias Troyer, (2016) arXiv: 1605.03590v2 \[PNAS, 114: 7555-7560 (2017)\]
    * 光合成? 
- Lowering qubit requirements for quantum simulations of fermionic systems, Delft, arXiv: 1712.07067
- How to factor 2048 bit RSA integers in 8 hours using 20 million noisy qubits, Craig Gidney, Martin Ekera, Google Inc. (2019), arXiv:1905.09749v3 
- Quantum Computing - from NISQ to PISQ, K. Bertels, A. Sarkar, I. Ashraf, arXiv:2106.11840v1 (2021)
   * 読んでない。谷本さんとの論文の文脈で出てきた論文かと思われる。
- K.Mitarai and K. Fujii. Constructing a virtual two-qubit gate by sampling single-qubit operations, New Journal of Physics, 23(2):023021, 2021. DOI: 10.1088/1367-2630/abd7bc.
    * 回路分割
- K. Mitarai and K. Fujii. Overhead for simulating a non-local channel with local channels by quasiprobability sampling. Quantum, 5:388, 2021. DOI: 10.22331/q-2021-01-28-388.
    * 回路分割
- Divide-and-conquer veri?cation method for noisy intermediate-scale quantum computation, Yuki Takeuchi, Yasuhiro Takahashi, Tomoyuki Morimae, Seiichiro Tani, arXiv:2109.14928v1 \[Quantum 6, 758 (2022)\]
- Hunting for quantum-classical crossover in condensed matter problems, 2210.14109
    * 鈴木さんと大久保さんの面白いやつ
- Circuit knitting with classical communication, IBM, arXiv: 2205.00016

## 誤り訂正符号
- Surface code quantum computing by lattice surgery, Clare Horsman, arXiv:1111.4022v3 (2011)
- Towards practical classical processing for the surface code, Austin G. Fowler (2012), arXiv:1110.5133v2 
- Coping with qubit leakage in topological codes, Austin G. Fowler (2013), arXiv: 1308.6642
    * 消失の取り扱いをデコーダの上でどのように取り扱っているのか(II節)が興味深い。3凖位を取り込むのではなくパウリエラーに帰着している。
- Minimum weight perfect matching of fault-tolerant topological quantum error correction in average O(1) parallel time, Austin G. Fowler (2014), arXiv:1307.1740v3
- Quantum computing with nearest neighbor interactions and error rates over 1%, Austin G. Fowler (2018), arXiv:1009.3686v1
- Topological and subsystem codes on low-degree graphs with flag qubits, Christopher Chamberland, Andrew W. Cross, IBM (2019), arXiv:1907.09528v2 
    * IBMが用いているLow-degree符号
- The XZZX surface code, J.P.B. Ataides, D.K. Tuckett, S.D. Bartlett, S.T. Flammia, B.J. Brown, arXiv: 2009.07851 \[Nat Commun 12, 2172 (2021)\]  
  ![image.png](/attachment/657dc855c7cac4160b2f6baa)
- Fault-tolerant thresholds for the surface code in excess of 5% under biased noise, D.K. Tuckett, S.D. Bartlett, S.T. Flammia, B.J. Brown, arXiv: 1907.02554 \[Phys. Rev. Lett. 124, 130501 (2020)\]  
  ![image.png](/attachment/657dc72dc7cac4160b2f68f8)
- Erasure conversion for fault-tolerant quantum computing in alkaline earth Rydberg atom arrays \[Nature Communications 13, 4657 (2022)\] 
    * 損失を含む訂正符号、本文中は測定エラーを考慮せずに消失したらデータ＆測定量子ビットを入れ替えることで対処している。補遺の中に測定エラーを入れた場合を検討しているが、パウリエラーを測定中に入れて計算し。復号は時空間により行われ文献49と同じ性能となっている。
    * 全体のエラーを物理エラーp_pと消失エラーp_eに分割してエラーシミュレータを動かしている。その比をReとしており、消失エラーに変換できることが閾値を押し上げていると考えられる。
    * 測定エラーは p_m = p_p なのか p_m = pなのかで大きく変化するかわると考えられる。文章では2量子ビットのエラー率と同じと書いており前者だが、数式は後者となっている。閾値はReの値がどの程度かわからないが2.8%となっている。
- ERASER: Towards Adaptive Leakage Suppression for Fault-Tolerant Qu antum Computing, Moinuddin Qureshi (2023), arXiv: 2309.13143

## デモ
- Superconducting quantum circuits at the surface code threshold for fault tolerance, R. Barends, Nature 508, 500 (2014)
   * 量子コンピュータの火付け役。断熱CZを使った量子ゲートの解説にもなっている。  
  ![image.png](/attachment/6589696ec7cac4160b2faf54)
- Observing a quantum Maxwell demon at work, B. Huard, (2017) arXiv: 1702.05161
- Demonstration of universal parametric entangling gates on a multi-qubit lattice, Rigetti (2017), arXiv:1706.06570v3
    * Rigetti 8ビット    
      ![image.png](/attachment/657a9503c2fbd0d355a077dd)
- Unsupervised machine learning on a hybrid quantum computer, Rigetti (2017) arXiv: 1712.05771 
    * Rigetti 19量子ビット  
      ![image.png](/attachment/657a9647c2fbd0d355a0793a)

### QECデモ
- Supplementary Information for “Superconducting quantum circuits at the surface code threshold for fault tolerance, R. Barends, J.M. Martinis \[Nature 508, 500?503 (2014)\] 
- Demonstration of weight-four parity measurements in the surface code architecture, Maika Takita (2016) arXiv: 1605.01351
    * 4体測定 
- Experimental demonstration of fault-tolerant state preparation with superconducting qubits, Maika Takita (2017)
    * \[4,2,2\]のデモ実装、FT状態生成
- Logical performance of 9 qubit compass codes in ion traps with crosstalk errors, Kenneth R. Brown, Duke University (2019), arXiv:1910.08495v2
    * Bacon-Shorの実装シミュレーション。イオントラップを念頭に。
- Repeated quantum error detection in a surface code, Christian Kraglund Andersen, Andreas Wallraff (2019), arXiv:1912.09410v1, \[Nature Physics volume 16, 875-880 (2020)\]  
    ![image.png](/attachment/657aa58ec2fbd0d355a08b7b)
- Realization of an Error-Correcting Surface Code with Superconducting Qubits, Xiabo Zhu, J-W. Pan, arXiv:2112.13505 \[Phys. Rev. Lett. 129, 030501(2022) \] 
- Suppressing quantum errors by scaling a surface code logical qubit, Google \[Nature volume 614, 676?681 (2023)\] 
- Logical quantum processor based on reconfigurable atom arrays, Harvard (2023)  

### NISQデモ
- Subspace variational quantum simulator, Kentaro Heya, arXiv: 1904.08566 (2023) \[Phys. Rev. Research 5, 023078 (2023)\]
- Quantum supremacy using a programmable superconducting processor, Frank Arute, Google, \[Nature 574, 505?510 (2019)\] 
- Information-to-work conversion by Maxwell’s demon in a superconducting circuit-QED system, Y. Masuyama, arXiv: 1709.00548 

# コヒーレンス
- Mitigation of quasiparticle loss in superconducting qubits by phonon scattering, QuTech, Delft  
- Improving the Coherence Time of Superconducting Coplanar Resonators, Martinis, (2009) arXiv:0909.0547v1 
    * 共振器評価によるTLSの影響を調べた論文
- Minimizing quasiparticle generation from stray infrared light in superconducting quantum circuits, Barends, UCSB, Appl. Phys. Lett. 99, 113507 (2011)
    * UCSB/赤外線の影響を調べた論文
- Enhancement in Quality Factor of SRF Niobium Cavities by Material Diffusion, Jefferson Lab, Newport News VA (2014), arXiv:1408.6245
    * ニオブの高温処理によりバルク中の不純物集中が小さくなり損失が改善した
- Flux trapping in superconducting accelerating cavities during cooling down with a spatial temperature gradient, Takayuki Kubo (KEK), (2016) arXiv:1601.02118
- Anomalous charge noise in superconducting qubits, A. Opremcak, L. Faoro, B. Plourde, R. McDermott, Wisconsin-Madison, Phys. Rev. B 100, 140503 (2019) 
    * 電荷分散をもつ量子ビットによりRamseyを用いて電荷雑音値を計測。スペクトル密度を求めている。ジャンプもあるが、表面電位のドリフトも考えられる。  
    ![image.png](/attachment/65897bd4c7cac4160b2fb84c)
- Correlated charge noise and relaxation errors in superconducting qubits, L. Faoro, A. Opremcak, R. McDermott, Wisconsin-Madison, Nature 594, 369?373 (2021) 
     * 電荷分散を使ってオフセット電荷をモニタすると相関する量子ビットのオフセット揺れが起きていることが分かる。ガンマ線とミュー粒子散乱による準粒子が生成されたという結論。


# 設計
## 超伝導量子ビット
- Self-shunted Al/AlOx/Al Josephson junctions, Physikalisch-Technische Bundesanstalt, Germany (2018), arXiv:cond-mat/0605532v1
- Charge- and flux-insensitive tunable superconducting qubit, Chad T. Rigetti (Berkley), arXiv: 1703.04613
- Superconducting caps for quantum integrated circuits, Rigetti (2017), arXiv:1708.02219v1
    * 量子ビットの上の上部空間を小さくすることで誘電体参加率を小さくすることを狙ったもの
- Simple impedance response formulas for the dispersive interaction rates in the effective hamiltonians of low anharmonicity superconducting qubits, Jay M. Gambetta (2017), arXiv:1712.08154v1
    * 量子ビット間や共振器との結合の方法をキャパシタンス行列から簡便に計算する方法
- Granular aluminum: A superconducting material for high impedance quantum circuits, Ioan M. Pop (2018), arXiv:1809.10646v1 \[Nature Materials **18**,816?819 (2019)\]
- Implementation of a transmon qubit using superconducting granular aluminum, Ioan M. Pop, KIT (2019), arXiv:1911.02333v2 \[Phys. Rev. X 10, 031032 (2020)\]    
    ![image.png](/attachment/657aa4e5c2fbd0d355a089a1)
- Superconducting Qubits: Current State of Play, William D. Oliver, MIT (2020), arXiv:1905.13641v3
    * 解説論文
- The superconducting quasicharge qubit, Vladimir E. Manucharya, Maryland (2021), arXiv:1907.02937v2
    * Blochnium 
- Unimon qubit, Mottonen (2022), arXiv:2203.05896v1 \[Nature Communications 13, 6895 (2022)\]

## ゲート
- Broadband population inversion, R. Tycko, \[Phys. Rev. Lett. 51, 775 (1983)\] 
- Optimal quantum control using randomized benchmarking, UCSB (2014), arXiv: 1403.0035
- Photon-mediated interactions between distant arti?cial atoms,  A. Wallraff, (2014), arXiv:1407.6747v1
- Measuring and suppressing quantum state leakage in a superconducting qubit, UCSB (2015) arXiv:1509.05470v2 
    * DRAG を使うもゲート長さを切り詰めるとリークが大きくなる
    * 3状態読み出し(補遺)
- Optimized cross-resonance gate for coupled transmon systems, Frank K. Wilhelm (2017)
- Quantification and characterization of leakage errors, Jay M. Gambetta (IBM), (2017) arXiv:1704.03081v1
- Effective Hamiltonian models of the cross-resonance gate, Easwar Magesan and Jay M. Gambetta (2018), arXiv:1804.04073v2 \[Physical Review A 101, 052308 (2020)\]
    * 高次の摂動の細かいことが書いてあるが、最後は無理やりブロック対角化に持ち込んでいる。
- Quantum interference device for controlled two-qubit operations, Nikolaj T. Zinner (Aarhus, Denmark) (2018), arXiv: 1809.09049v3
    * 4量子ビット系で2制御2対象の複雑な量子ゲートを提案。シミュレーションのみ
- Demonstration of a parametrically-activated entangling gate protected from flux noise, Rigetti (2019), arXiv:1901.08035v3 
    * Rigetti 4量子ビットを用いてパラメトリックゲートの実装。4量子ビットは4,8,8カラーコードの基礎部分
- Calibration of the cross-resonance two-qubit gate between directly-coupled transmons, A. Patterson,  P. Leek, Oxford (2019), arXiv:1905.05670v1 \[Phys. Rev. Applied 12, 064013 (2019)\]
    * APS'18で聞いたやつかと。
- Cross-resonance interactions between superconducting qubits with variable detuning, B.L.T. Plourde, Syracuse (2019), arXiv:1905.11480v1
    * 交差共鳴の離調依存性, 論文としては着地せず
- Constructing a virtual two-qubit gate from single-qubit operations, Kosuke Mitarai, Keisuke Fujii (2019), arXiv:1909.07534v1 \[New J. Phys. 23 023021\]  
  ![image.png](/attachment/657dca0cc7cac4160b2f6d9a)
    * Akhil実験の元ネタ
- Demonstration of an all-microwave controlled-phase gate between far detuned qubits, A. Wallraff (2020), arXiv:2006.10639v1, Phys. Rev. Applied 14, 044039 (2020)
    * たぶん読んでない
- Quantum optimal control in quantum technologies. Strategic report on current status, visions and goals for research in Europe, C.P. Koch, U. Boscain, T. Calarco, G. Dirr, S. Filipp, S.J. Glaser, R. Kosloff, S. Montangero, T. Schulte-Herbruggen, D. Sugny, F.K. Wilhelm, EPJ Quantum Technology 9, 19 (2022)
    * 総レビュー論文。Wilhelm系列のたくさんの文献リストと思ってよい。
- High-fidelity three-qubit iToffoli gate for fixed-frequency superconducting qubits, Irfan Siddiqi (2022) 
    * 松田君が論文紹介していたネイティブに3量子ビットゲートを作るゲートのデモ。
- Demonstration of the Two-Fluxonium Cross-Resonance Gate, Maxim Vavlov, Vladimir E. Manucharyan (2022), arXiv: 2204.11829 
    * 査読で読んだ論文、磁場制御を必要としない交差共鳴ゲートを半整数フラクソニウムに適用したもの。
- ZZ-Interaction-Free Single-Qubit-Gate Optimization in Superconducting Qubits, Shu Watanabe (2023), arXiv: 2309:13927 

## 測定
- Fast Scalable State Measurement with Superconducting Qubits, UCSB (2014), arXiv:1401.0257v3 
- Resonantly phase-matched Josephson junction traveling wave parametric ampli?er, Kevin O'Brien, (2014) arXiv: 1406.2346v1
- Fast quantum non-demolition readout from longitudinal qubit-oscillator interaction, Alexandre Blais (2015), arXiv:1504.04002v1
    * zCQED
- Measurement-Induced State Transitions in a Superconducting Qubit: Beyond the Rotating Wave Approximation, Google (2016) \[Phys. Rev. Lett. 117, 190503 (2016)\]
- Realizing rapid, high-fidelity, single-shot dispersive readout of superconducting qubits, C. Eichler and A. Wallraff, arXiv: 1701.06933 \[Phys. Rev. Applied 7, 054020 (2017)\]
    * 88 ns, 99.2 %
- General method for extracting the quantum effciency of dispersive qubit readout in circuit QED, L. DiCarlo (2017), arXiv: 1711.05336
- Rapid high-fidelity multiplexed readout of superconducting qubits, Andreas Wallraff (2018), arXiv:1801.07904v1, \[Phys. Rev. Applied 10, 034040 (2018) \]
    * 前回の測定に加えて多重化測定を高精度に行ったもの。同時にクロストークの評価として位相緩和レートを測定している。
- Observing the escape of a driven quantum Josephson circuit into unconfined states, Zaki Leghtas (ENS) (2018), arXiv:1805.05198v2 \[Escape of a driven quantum josephson circuit into unconfined states, Phys. Rev. Applied 11, 014030 (2019)\]
    * 量子ビットに結合する共振器を強ドライブした時に上の状態に飛んでいくイオン化を実験的に観測したもの
- Quantum microwave radiometry with a superconducting qubit, M.H. Devoret (2019), arXiv:1909.12295v2 
    * 量子ビットをツールに環境温度を測定する方法
- Superconducting Parametric Amplifiers, The State of the Art in Josephson Parametric Amplifiers, Jose Aumentado, 解説論文 (2020), \[IEEE Microwave Magazine, 1527-3342/20\]
- Breaking the trade-off between fast control and long lifetime of a superconducting qubit, Shingo Kono, \[Nature Communications 11, 3683 (2020)\] 
- High-fidelity measurement of a superconducting qubit using an on-chip microwave photon counter, Alex Opremcak, R. McDermott (2020), arXiv:2008.02346v1, \[Phys. Rev. X 11, 011027 (2021)\]
- Measurement-Induced State Transitions in a Superconducting Qubit: Within the Rotating Wave Approximation, Google (2022) \[Phys. Rev. Applied 20, 054008 (2023)\]
- Qubit sensing: A new attack model for multi-programming quantum Computing 
    * 束野さんが論文紹介。測定のクロストークを量子回路を用いてスニッフィングするテクニック
- Enhancing Dispersive Readout of Superconducting Qubits Through Dynamic Control of the Dispersive Shift: Experiment and Theory, A. Wallraff (2023), arXiv: 2307.07765 

## 集積系
- Pseudo-2D superconducting quantum computing circuit for the surface code: the proposal and preliminary tests, H. Mukai (2019), arXiv:1902.07911v3 \[New J. Phys. 22 043013(2020)\]
- Optimizing frequency allocation for ?xed-frequency superconducting quantum processors, Sidiqqi, arXiv: 2112.01634 \[Phys. Rev. Research 4, 023079 (2022)\]
- Co-Design quantum simulation of nanoscale NMR, IQM, Phys. Rev. Research 4, 043089 (2022) 
     * 特定のアプリケーションに特化した超伝導量子プロセッサの協調設計について述べている。
- Mitigation of frequency collisions in superconducting quantum processors, Jonas Bylander, arXiv: 2303.04663, \[PhysRevResearch. 5, 043001 (2023)\]


# 制御装置
- Engineering cryogenic setups for 100-qubit scale superconducting circuit systems, A. Wallraff (2018), arXiv:1806.07862v1 \[EPJ Quantum Technology **6**, 2 (2019)\]
    * 冷凍機の設計に関し熱負荷などが議論されているエンジニアーズガイド
- A Quantum Engineer's Guide to Superconducting Qubits, W. D. Oliver (2019), arXiv:1904.06560v5
    * Willさんのエンジニアーズガイド
- Cryogenic data-based one-port calibration for superconducting microwave resonator measurement, D. Papas, NIST (2021)  
- Experimental advances with the QICK (Quantum Instrumentation Control Kit) for superconducting quantum hardware, (2023)  
- Digital Readout and Control of a Superconducting Qubit  Digital Readout and Control of a Superconducting Q, 博士論文 (Syracuse),   

## I/F
- Quantum transduction of optical photons from a superconducting qubit, Oskar Painter, Caltech (2020), arXiv:2004.04838v1 \[Superconducting qubit to optical photon transduction, Nature 588, 599-603 (2020)\]
    * 光読み出し量子ビット
- On-chip single-pump interferometric Josephson isolator for quantum measurements, Markus Brink, IBM (2020), arXiv:2006.01918v1, \[High-Fidelity Qubit Readout Using Interferometric Directional Josephson Devices, PRX Quantum 2, 040360 (2021)\]
- Flexible coaxial ribbon cable for high-density superconducting microwave device arrays, UCSB (2020), arXiv:2007.06496v1, \[IEEE Transactions on Applied Superconductivity, vol. 31, no. 1, pp. 1-5, 2021]
- Microwave quantum link between superconducting circuits housed in spatially separated cryogenic systems, A. Wallraff (2020), arXiv:2008.01642v1, \[Phys. Rev. Lett. 125, 260502 (2020)\]
- Fiber-integrated microwave-to-optical quantum transducer, Wenfang Li, Waterloo, Phys. Rev. Appl. 20, 044031 (2023) 

## 復号器
- Deep neural decoders for near term fault-tolerant experiments, Christopher Chamberland and Pooya Ronagh, Waterloo (2018), arXiv:1802.06441v2
- NISQ+: Boosting quantum computing power by approximating quantum error correction,  Frederic T. Chong (2020), arXiv:2004.04794v2
- Tensor Network Decoding Beyond 2D, Christophe Piveteau, Christopher T. Chubb, Joseph M. Renes (2023), arXiv:2310.10722 

## ミドルウェア
- NMR Techniques for Quantum Control and Computation, Lieven Vanderspen, arXiv:quant-ph/0404064v2 (2004) 
- Physical qubit calibration on a directed acyclic graph, J. Kelly, arXiv: 1803.03226 
    * Optimus: 量子ビットの較正方法をうまくやるソフトウェアについて述べたもの。
- Learning the quantum algorithm for state overlap (2018), Los Alamos National Laboratory, arXiv:1803.04114v1 
    * ある意味分割コンパイラのようなもの
    * 最初に回路の形をある程度決めておき、上手く行くように最適化をしたもの。例題としてSWAPテストを取り上げている。
- Tackling systematic errors in quantum logic gates with composite rotations, Jonathan A. Jones, arXiv:quant-ph/0208092v1 (2018) 
- A Case for Multi-Programming Qantum Computers, Poulami Das, Swamit Tannu, Prashant Nair, Moinuddin Qureshi, MICRO52 (2019) 
    * 複数の量子ビットがあった時にどうプログラムすべきかを議論したアーキ論文。
- A quantum-classical cloud platform optimized for variational hybrid algorithms, Rigetti (2020), arXiv:2001.04449
- Optimized quantum compilation for near-term algorithms with OpenPulse, Frederic T. Chong, Chicago (2020), arXiv:2004.11205v2 \[53rd Annual IEEE/ACM International Symposium on Microarchitecture (MICRO), Athens, Greece, 2020 pp. 186-200.\]
- A Serverless Cloud Integration For Quantum Computing, IBM (Italia),2021  

# 接合
- Modified Diffusion Bonding of Chemical Mechanical Polishing Cu at 150 degC at Ambient Pressure,  Akitsu Shigetou and Tadatomo Suga, Appl. Phys. Express, 2, 056501 (2009)  
- 3次元実装に用いるチップ貫通電極形成技術 (2001)  
- Fabrication of feedhorn-coupled transition edge sensor arrays for measurement of the cosmic microwave background polarization, NASA (2015), arXiv: 1511.05036
    * TES分野の人がIn バンプを用いて積層構造を作る例
- Silicon-based antenna-coupled polarization-sensitive millimeter-wave bolometer arrays for cosmic microwave background instruments, 
Johns Hopkins, (2016) arXiv 1608.08891
    * 天文分野: 5umのインジウムバンプを使って積層構造を形成
- Bondability investigation of thermosonic flip chip bonding using ultrasonic perpendicular to the interface, 東芝 (2019)  
