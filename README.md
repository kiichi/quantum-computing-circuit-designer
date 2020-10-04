# quantum-computing-circuit-designer
Drag and Drop to Generate Q# Code or vice versa (in the future)

[Demo - Quantum Computing Circuit Designer for Q#](https://kiichi.github.io/quantum-computing-circuit-designer/)

Still work in progress.

```
let circuit = {
    qubits: 2,
    gates:[
        {type:"Q",q:0, t:0},
        {type:"Q",q:1, t:0},
        // Deutch's Algorithm
        // Setup
        {type:"H",q:0, t:2},
        {type:"X",q:1, t:1},
        {type:"H",q:1, t:2},
        // Oracle e.g. Identity, balanced function
        {type:"CNOT",q:0, t:3, target:1},
        // Measure
        {type:"M",q:0, t:4},
        {type:"M",q:1, t:4}
    ]
};
```

```
exportQSharp(circuit);
```

generates

```
namespace MyCircuit {
    open Microsoft.Quantum.Canon;
    open Microsoft.Quantum.Intrinsic;
    open Microsoft.Quantum.Convert;
    open Microsoft.Quantum.Math;

    @EntryPoint()
    operation Main(): Unit{

        using(qubits = Qubit[2]){
            // t=1
			X(qubits[1]);

			// t=2
			H(qubits[0]);
			H(qubits[1]);

			// t=3
			CNOT(qubits[0],qubits[1]);

			// t=4
			M(qubits[0]);
			M(qubits[1]);
        }
            
    }
}
```


## TODO - SELF MEMO

Integrate them? 
- [quantastica/quantum-circuit: Quantum Circuit Simulator implemented in JavaScript](https://github.com/quantastica/quantum-circuit)
- [Quantum Programming Studio](https://quantum-circuit.com/qconvert)


Plan - the above json is simple t vs qubits simply for drawing purpose -> first export it to QASM 2.0 then convert it to any languages ?