```python
import numpy as np
from qiskit import *
from qiskit import Aer
from qiskit.visualization import plot_state_city
from qiskit.visualization import plot_histogram
```


```python
# Création d'un circuit quantique à 2 qubits
circ = QuantumCircuit(2)
```


```python
# Porte de Hadamard sur les quatres premiers qubits pour permettre à toutes les possibilités de cohabiter
circ.h(0)
circ.h(1)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x1f21046ef20>




```python
# Apercu du circuit
circ.draw('mpl')
```




    
![png](images/output_3_0.png)
    




```python
# Inversion de la phase du premier qubit
circ.x(0)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x1f212316e00>




```python
# Porte de contrôle-Z entre les deux qubits
circ.cz(0,1)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x1f212316a70>




```python
# Inversion de la phase du premier qubit et ajout d'une barrière pour plus de clarté
circ.x(0)
circ.barrier()
```




    <qiskit.circuit.instructionset.InstructionSet at 0x1f212316aa0>




```python
circ.draw('mpl')
```




    
![png](images/output_7_0.png)
    




```python
# Porte de Hadamard sur les quatres premiers qubits (personnes)
circ.h(0)
circ.h(1)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x1f212381810>




```python
# Inversion de la phase des deux qubits
circ.z(0)
circ.z(1)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x1f2123809d0>




```python
# Porte de contrôle-Z entre les deux qubits
circ.cz(0,1)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x1f212381420>




```python
# Porte de Hadamard sur les quatres premiers qubits
circ.h(0)
circ.h(1)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x1f2123819c0>




```python
circ.draw('mpl')
```




    
![png](images/output_12_0.png)
    




```python
# Permet de mesurer tous les qubits du circuit
circ.measure_all()
circ.draw('mpl')
```




    
![png](images/output_13_0.png)
    




```python
# Utilisation du backend 'statevector_simulator' de Qiskit pour simuler le circuit
backend = Aer.get_backend('statevector_simulator')
job = backend.run(circ)
result = job.result()
outputstate = result.get_statevector(circ,decimals=3)
print(outputstate)
# Représentation graphique de l'état final
plot_state_city(outputstate)
```

    Statevector([ 0.+0.j, -0.+0.j,  1.-0.j,  0.+0.j],
                dims=(2, 2))
    




    
![png](images/output_14_1.png)
    




```python
simulator = Aer.get_backend('aer_simulator')
job = execute(circ, backend=simulator, shots=1024)
result = simulator.run(transpile(circ,simulator)).result()
counts = result.get_counts(circ)
plot_histogram(counts)
# On observe qu'il y a 100% de chance d'obtenir ce résultat
```




    
![png](images/output_15_0.png)
    


