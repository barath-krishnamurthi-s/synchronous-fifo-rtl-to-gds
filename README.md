# Synchronous FIFO — RTL to GDSII

A complete RTL-to-GDSII implementation of an 8-bit × 8-depth synchronous FIFO using the SKY130 open-source Process Design Kit (PDK) and OpenLane 2.

## Project Overview:

This project demonstrates the physical implementation of a digital RTL design, starting from Verilog RTL and progressing through synthesis, floorplanning, placement, clock-tree synthesis, routing, static timing analysis, design-rule checking, layout-versus-schematic verification, and final GDSII generation.

The design is a single-clock synchronous FIFO with:

- Data width: 8 bits
- Depth: 8 entries
- Common read/write clock
- Asynchronous active-high reset
- Full and empty status flags
- Simultaneous read/write operation support

## RTL Architecture

The FIFO uses:

- 8-bit data storage
- Read and write pointers
- Occupancy counter
- Full and empty detection logic
- Synchronous read/write control with a common clock

The RTL source is located at:

`rtl/synchronous_fifo.v`

## RTL to GDSII Flow

```text
Verilog RTL
    ↓
RTL Simulation
    ↓
OpenLane 2
    ↓
Logic Synthesis
    ↓
Floorplanning
    ↓
Placement
    ↓
Clock Tree Synthesis
    ↓
Routing
    ↓
Static Timing Analysis
    ↓
DRC
    ↓
LVS
    ↓
Antenna Check
    ↓
Final GDSII
```

## Technology and Tools

| Component | Tool / Technology |
|---|---|
| HDL | Verilog |
| RTL-to-GDSII Flow | OpenLane 2 |
| PDK | SKY130A |
| Standard Cell Library | sky130_fd_sc_hd |
| Layout Format | GDSII |
| Layout Viewer | KLayout |
| Simulation | Vivado Simulator |
| Timing Analysis | OpenLane / OpenROAD flow |
| Physical Verification | OpenLane / Magic / Netgen flow |

## Implementation Results

### Synthesis

| Metric | Result |
|---|---:|
| Standard-cell instances | 269 |
| Sequential area | 49.80% |
| Mux2 cells | 74 |
| DFF cells | 64 |
| Memories | 0 |
| Memory bits | 0 |
| Estimated area | 3683.5328 µm² |

The FIFO is implemented using standard-cell logic rather than a dedicated SRAM macro.

### Physical Design

| Metric | Result |
|---|---:|
| Die width | 96.87 µm |
| Die height | 107.59 µm |
| Placement rows | 31 |
| Components | 269 |
| Port bits | 22 |

The final routed design was exported as:

`results/gds/synchronous_fifo.gds`

## Physical Verification

### Design Rule Check

Final DRC result:

```text
DRC violations: 0
```

### Layout Versus Schematic

The extracted layout and the synthesized netlist matched uniquely.

```text
Circuits match uniquely.
```

### Antenna Check

```text
Net violations: 0
Pin violations: 0
```

### Static Timing Analysis

The design was analyzed using the configured 10 ns clock period.

The final timing reports are available in:

`results/reports/sta_summary.rpt`

## Repository Structure

```text
synchronous-fifo-rtl-to-gds/
│
├── README.md
│
├── rtl/
│   └── synchronous_fifo.v
│
├── tb/
│
├── openlane/
│   └── config.yaml
│
├── results/
│   ├── gds/
│   │   ├── floorplan.gds
│   │   ├── placement.gds
│   │   └── synchronous_fifo.gds
│   │
│   ├── reports/
│   │   ├── synthesis_stat.rpt
│   │   ├── sta_summary.rpt
│   │   ├── drc_report.xml
│   │   ├── lvs_report.rpt
│   │   └── antenna_summary.rpt
│   │
│   └── screenshots/
│
└── .gitignore
```

## Key Outputs

The repository contains the main implementation and verification artifacts:

- Verilog RTL
- OpenLane configuration
- Floorplan GDSII
- Placement GDSII
- Final routed GDSII
- Synthesis report
- Static timing report
- DRC report
- LVS report
- Antenna report

The final GDSII can be opened and inspected using KLayout.

## Reproducibility

The OpenLane configuration used for the implementation is provided in:

`openlane/config.yaml`

The project can therefore be used as a reference for reproducing the RTL-to-GDSII flow using OpenLane 2 and the SKY130A PDK.

## Project Outcome

This project demonstrates the complete digital implementation flow from synthesizable Verilog RTL to a physically routed GDSII layout, including both logical and physical verification.
