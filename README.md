# Model2RTL Lab

Model2RTL Lab is a small, frontend-only research prototype that illustrates how a neural-network compiler might lower PyTorch models into parameterized RTL for FPGA or ASIC targets. It is an architectural demonstrator, not a synthesis or deployment tool.

## The AI → RTL problem

Neural-network frameworks describe computation with high-level tensor operators, dynamic runtime conventions, and software-oriented data layouts. Hardware implementation needs explicit bit widths, streaming interfaces, resource allocation, pipeline schedules, memory organization, and cycle-accurate control. An AI-to-RTL compiler must bridge those representations while keeping the result traceable to the source model.

## Demonstrated flow

1. **Model graph** — a PyTorch-like layer graph captures operators, tensor shapes, and parameter counts.
2. **Operator normalization** — framework-specific nodes are converted into a small canonical IR such as `DENSE`, `CONV_2D`, `RELU`, `RESHAPE`, and `MAX_POOL`.
3. **Hardware planning** — target, numeric precision, parallelism, and clock settings feed a deterministic illustrative cost model for DSPs, BRAM, LUTs, latency, and throughput.
4. **RTL generation** — normalized operators map to simplified hardware primitives and a parameterized SystemVerilog preview.
5. **Validation** — the prototype animates a validation stage to communicate the intended compiler architecture. It does not execute RTL simulation or equivalence checking.

Traceability is preserved from a source operator through normalized IR and hardware primitive to an output file, for example: `PyTorch Linear → DENSE → MAC_ARRAY → linear_0.sv`.

## Run locally

```bash
npm install
npm run dev
```

## Limitations

- All hardware estimates are deterministic synthetic calculations for demonstration only.
- Generated SystemVerilog is a simplified preview and is not production-ready RTL.
- LSTM/recurrent lowering is intentionally unsupported.
- There is no backend, database, authentication, model upload, real PyTorch parsing, synthesis, place-and-route, bitstream generation, FPGA deployment, or proprietary vendor integration.
- The synthesis plan is explanatory only; the project does not call Vivado, Quartus, or foundry tools.

## Extending this into a thesis

A full thesis implementation could add Torch FX or ONNX graph ingestion, shape and quantization analysis, a formally specified intermediate representation, schedule and resource-allocation algorithms, reusable RTL operator libraries, memory/bandwidth modeling, automated testbench generation, software-versus-RTL equivalence tests, and design-space exploration. The final evaluation could integrate a real synthesis flow, collect post-synthesis timing and utilization, deploy selected designs to an FPGA development board, and compare measured throughput, latency, power, and accuracy against the compiler's predictions.

## Stack

React, TypeScript, Vite/Vinext, Tailwind CSS, and accessible UI primitives. The application is a single responsive page with no persistence.
