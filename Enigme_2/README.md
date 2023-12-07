# Exercice 2 : Le problème des cheveux indigo

```python
import numpy as np
from qiskit import *
from qiskit import Aer
from qiskit.visualization import plot_state_city
```


```python
# Création d'un circuit quantique à 8 qubits représentant les 4 personnes et les 4 raisonnements
circ = QuantumCircuit(8)
```


```python
# Porte de Hadamard sur les quatres premiers qubits (personnes) pour permettre à toutes les possibilités de cohabiter
circ.h(0)
circ.h(1)
circ.h(2)
circ.h(3)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291a8d33fd0>




```python
# Apercu du circuit
circ.draw('mpl')
```




    
![png](images/output_3_0.png)
    




```python
# Ajout d'une séparation pour séparer les étapes
circ.barrier()
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291aac3bd00>




```python
# Ajout de 3 portes CNOT permettant de calculer si il y a un nombre pair ou impair de cheveux indigo (1)
circ.cx(1,4)
circ.cx(2,4)
circ.cx(3,4)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291aac00250>




```python
circ.barrier()
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291aac00580>




```python
# Apercu du circuit après l'ajout des 3 portes
circ.draw('mpl')
```




    
![png](images/output_7_0.png)
    




```python
# Ajout de 3 portes CNOT permettant de calculer la parité des cheveux indigo (1)
circ.cx(4,5)
circ.cx(4,6)
circ.cx(4,7)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291aac02c20>




```python
circ.barrier()
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291aac03820>




```python
circ.draw('mpl')
```




    
![png](images/output_10_0.png)
    




```python
# Ces deux portes permettent à Bob de deviner la couleur de ses cheveux en voyant les cheveux de la personne de devant
circ.cx(2,5)
circ.cx(3,5)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291aaf11390>




```python
circ.barrier()
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291aaf11960>




```python
circ.draw('mpl')
```




    
![png](images/output_13_0.png)
    




```python
# Permet aux deux participants restants de prendre en note la couleur des cheveux de Bob
circ.cx(5,6)
circ.cx(5,7)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291ab749ea0>




```python
circ.barrier()
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291ab74aa40>




```python
circ.draw('mpl')
```




    
![png](images/output_16_0.png)
    




```python
# Permet à Charlie de noter la couleur des cheveux de la personne en face de lui et lui permet d'annoncer la couleur de ses propres cheveux
circ.cx(3,6)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291a49802e0>




```python
circ.barrier()
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291aaf12020>




```python
circ.draw('mpl')
```




    
![png](images/output_19_0.png)
    




```python
# Enfin c'est au tour de Dalia d'annoncer la couleur de ses cheveux
circ.cx(6,7)
```




    <qiskit.circuit.instructionset.InstructionSet at 0x291ab749900>




```python
circ.draw('mpl')
```




    
![png](images/output_21_0.png)
    




```python
# Permet de mesurer tous les qubits du circuit donc de connaître 3 fois sur 4 les couleurs des cheveux
circ.measure_all()
circ.draw('mpl')
```




    
![png](images/output_22_0.png)
    




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

    Statevector([0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 1.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j,
                 0.+0.j, 0.+0.j, 0.+0.j, 0.+0.j],
                dims=(2, 2, 2, 2, 2, 2, 2, 2))
    




    
![png](images/output_23_1.png)
    


