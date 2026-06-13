# SynopsysAgent — Synopsys EDA AI Subagent

An AI agent specialized in **Synopsys EDA tools** for ASIC RTL-to-GDSII design flow. Covers `dc_shell` (synthesis), `icc2_shell` (physical design), PrimeTime (STA), Formality (formal verification), VCS (simulation), and ICV (DRC/LVS).

## Repository Structure

```
SynopsysAgent/
├── README.md          # This file — usage guide
├── synopsys.md        # Agent definition file (copy for opencode global agents)
└── LICENSE            # Apache 2.0
```

---

## Using as an opencode Subagent

### Option 1: Global Agent (Automatic @synopsys)

The agent is already installed globally at `~/.config/opencode/agents/synopsys.md`.  
This means **`@synopsys` is available in any opencode session** with no per-project configuration needed.

**Invoke it from any conversation:**

```
@synopsys synthesize this RTL for best PPA

@synopsys write an ICC2 floorplan script with 70% utilization

@synopsys help me fix setup timing violations on clock clk

@synopsys write a dc_shell Tcl script to synthesize a 32-bit RISC-V core at 500MHz

@synopsys generate an ICC2 power planning script with M7/M8 stripes

@synopsys run PrimeTime STA on this netlist and report setup/hold violations

@synopsys debug this DRC error: short between M2 and M3 at coordinates (100,200)

@synopsys create a clock tree synthesis script targeting 50ps skew

@synopsys write a Formality script to verify equivalence after synthesis

@synopsys optimize this path: regA -> AND2 -> regB has 150ps negative slack

@synopsys generate a complete synthesis-to-GDS flow for a 7nm design with 8 SRAM macros

@synopsys fix the LVS error: missing VDD connection on instance INV_X1_123

@synopsys what's the difference between compile_ultra and compile -incremental_mapping?

@synopsys generate a .synopsys_dc.setup template for SAED32 library
```

### Option 2: Per-Project Registration

Add to your project's `opencode.json` or `opencode.jsonc`:

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "agents": {
    "synopsys": {
      "description": "Synopsys EDA expert for ASIC Design Flow. Covers dc_shell (synthesis) and icc2_shell (physical design) flows. Expert in RTL-to-GDSII implementation including synthesis, floorplanning, placement, CTS, routing, STA, DRC/LVS closure.",
      "path": "./agents/synopsys.md"
    }
  }
}
```

Then place `synopsys.md` in your project at `./agents/synopsys.md` (copy from this repo).

### Trigger Keywords

| Category | Keywords |
|----------|----------|
| **Synthesis** | `synopsys`, `dc_shell`, `design compiler`, `compile_ultra`, `synthesis` |
| **Physical Design** | `icc2`, `icc2_shell`, `physical design`, `floorplan`, `placement`, `cts`, `clock tree`, `routing`, `route_auto`, `place_opt`, `clock_opt` |
| **Timing** | `sta`, `primetime`, `pt_shell`, `timing closure`, `setup time`, `hold time`, `report_timing` |
| **Verification** | `formality`, `formal verification`, `vcs`, `simulation`, `icv`, `drc`, `lvs` |
| **General** | `ppa`, `qor`, `power`, `area`, `gds`, `ndm`, `tlu+`, `standard cell` |

---

## Using with Claude Code (claude.ai / Claude Code CLI)

### Option A: CLAUDE.md Configuration

Add to your project's `CLAUDE.md`:

```markdown
# Synopsys EDA Agent

When the user mentions Synopsys tools (dc_shell, icc2_shell, PrimeTime, Formality, VCS),
load the specialized agent context from `synopsys.md`:

- **synthesis** — DC: analyze, elaborate, compile_ultra, report_timing/power/qor, write_file
- **physical design** — ICC2: floorplan, pin/macro placement, power planning, place_opt, clock_opt, route_auto, post-route opt, GDS output
- **timing** — PrimeTime: STA, setup/hold analysis, timing closure strategies
- **verification** — Formality (formal), VCS (simulation), ICV (DRC/LVS)

Reference file: `./synopsys.md` (included in this repo)
```

### Option B: Custom Agent (Claude Code)

Claude Code supports custom agent definitions. Place the `synopsys.md` content in your agent registry:

```json
{
  "name": "synopsys",
  "description": "Synopsys EDA expert for ASIC RTL-to-GDSII design flow",
  "instructions": "You are an expert in Synopsys EDA tools...",
  "triggers": ["synopsys", "dc_shell", "icc2", "synthesis", "physical design"]
}
```

Then invoke with:

```
@synopsys write a dc_shell synthesis script for a 32-bit RISC-V core
```

---

## Capabilities

### 1. Design Compiler (dc_shell) — Synthesis

| Area | Details |
|------|---------|
| **Flow** | analyze → elaborate → constrain → compile_ultra → report → write_outputs |
| **Commands** | `analyze`, `elaborate`, `compile_ultra`, `compile -incremental_mapping`, `set_max_delay`, `set_input/output_delay`, `set_false_path`, `set_multicycle_path`, `set_dont_touch`, `set_clock_gating_style` |
| **Reports** | `report_timing`, `report_power`, `report_area`, `report_qor`, `report_clock_gating`, `check_design` |
| **Outputs** | Verilog netlist, SDC, SDF, DB |
| **Setup** | `.synopsys_dc.setup` with `search_path`, `target_library`, `link_library`, `symbol_library` |

### 2. IC Compiler II (icc2_shell) — Physical Design

| Stage | Key Commands |
|-------|-------------|
| **Library Setup** | `create_lib`, `read_verilog`, `read_parasitic_tech` |
| **Floorplanning** | `initialize_floorplan`, `set_block_pin_constraints`, `place_pins` |
| **Macro Placement** | `create_keepout_margin`, `set_fixed_objects`, `derive_placement_blockages` |
| **Power Planning** | `check_pg_connectivity`, `set_pg_strategy` |
| **Placement** | `create_placement`, `legalize_placement`, `place_opt` |
| **CTS** | `set_clock_tree_options`, `clock_opt`, `report_clock_qor` |
| **Routing** | `set_ignored_layers`, `route_auto`, `optimize_routes` |
| **Verification** | `check_routes`, `check_lvs` |
| **Output** | `write_gds`, `write_verilog` |

### 3. PrimeTime (pt_shell) — Static Timing Analysis

Setup/hold analysis, timing closure guidance, constraint validation, report generation.

### 4. Formality — Formal Verification

Equivalence checking between RTL and gate-level netlist.

### 5. VCS — Simulation

RTL simulation, testbench generation, waveform analysis.

### 6. ICV — Physical Verification

DRC (design rule checking) and LVS (layout vs. schematic).

---

## Example Use Cases

### Synthesis Script Generation

> @synopsys write a dc_shell script to synthesize a 32-bit RISC-V core with compile_ultra, targeting 500 MHz at 0.95V nominal corner. Output reports for timing, power, and area.

### ICC2 Floorplan Setup

> @synopsys create an ICC2 floorplan script with 70% core utilization, 5um core offset, keepout margins around 8 macros, and pin placement on M5/M6 layers.

### Timing Fix Guidance

> @synopsys I have a setup violation on path from regA/Q to regB/D with 150ps of negative slack. The path goes through a 2-input AND gate. What strategies should I try?

### Formal Verification

> @synopsys write a Formality script to verify equivalence between my RTL and the synthesized netlist for the top module.

### Full RTL-to-GDSII Flow

> @synopsys walk me through the complete RTL-to-GDSII flow for a design with 8 SRAM macros, target frequency 1GHz, 7nm technology. Include all synthesis, floorplan, and routing steps.

---

## Configuration File: synopsys.md

The file `synopsys.md` in this repo is the **opencode agent definition**. It contains:

- **Frontmatter** — description, permission model, trigger metadata
- **Tool invocation table** — dc_shell, icc2_shell, pt_shell, starrc_shell, ICV, fc_shell
- **DC synthesis flow** — full step-by-step Tcl with library setup, compile, reports, outputs
- **ICC2 physical design flow** — complete 13-stage flow from library setup to GDS output
- **Tcl scripting patterns** — collection queries, attribute handling, loops, filtering
- **Project file structure** — recommended directory layout for synthesis and PD
- **Technology references** — SAED32 library, metal layer stack, standard checks
- **Parameter summary** — typical values for utilization, offset, skew, transition, etc.

To use it as a global opencode agent, copy to `~/.config/opencode/agents/synopsys.md` (already installed).

---

## License

Apache License 2.0
