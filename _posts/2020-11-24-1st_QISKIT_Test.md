```python
%matplotlib inline
# Importing standard Qiskit libraries
from qiskit import QuantumCircuit, execute, Aer, IBMQ
from qiskit.compiler import transpile, assemble
from qiskit.tools.jupyter import *
from qiskit.visualization import *
from ibm_quantum_widgets import *

# Loading your IBM Q account(s)
provider = IBMQ.load_account()
```

    /opt/conda/lib/python3.8/site-packages/qiskit/providers/ibmq/ibmqfactory.py:192: UserWarning: Timestamps in IBMQ backend properties, jobs, and job results are all now in local time instead of UTC.
      warnings.warn('Timestamps in IBMQ backend properties, jobs, and job results '



```python
from qiskit import QuantumRegister, ClassicalRegister, QuantumCircuit
from numpy import pi

qreg_q = QuantumRegister(3, 'q')
creg_c = ClassicalRegister(3, 'c')
circuit = QuantumCircuit(qreg_q, creg_c)

circuit.u(pi/4, pi/2, pi/6, qreg_q[0])
circuit.t(qreg_q[1])
circuit.ccx(qreg_q[0], qreg_q[2], qreg_q[1])
circuit.h(qreg_q[1])
circuit.x(qreg_q[2])
circuit.measure(qreg_q[2], creg_c[2])
circuit.measure(qreg_q[1], creg_c[1])
circuit.rxx(pi/4, qreg_q[0], qreg_q[1]).c_if(creg_c, 1)
circuit.h(qreg_q[1])
circuit.swap(qreg_q[0], qreg_q[1])

editor = CircuitComposer(circuit=circuit)
editor
```
