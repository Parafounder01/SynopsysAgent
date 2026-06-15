# SynopsysAgent — AI-Powered Assistant for Chip Design

> **Making Semiconductor Design Accessible & Fast — for Universities, Research Labs, and Industry**

SynopsysAgent is an **AI assistant** that understands and automates the world's most widely used chip design tools (Synopsys EDA). Whether you are a **student learning VLSI**, a **professor teaching Advanced Digital Design**, a **dean investing in semiconductor education**, or an **expert company taping out at 3nm** — this agent speaks your language and speeds up your work.

---

## Why This Matters

| Audience | What This Means for You |
|----------|------------------------|
| **Professors & Researchers** | Automate lab setup, generate teaching scripts, explore design-space faster. Use it in VLSI courses, research projects, and publication workflows. |
| **Deans & University Leaders** | A ready-to-deploy tool that boosts your semiconductor program's hands-on capability without hiring extra EDA experts. Students learn industry-standard flows from day one. |
| **Expert Companies (Fabless, IDMs, Design Houses)** | Reduce tape-out iteration time. Get correct-by-construction Tcl scripts for synthesis, floorplanning, timing closure — from one AI that knows every Synopsys tool. |

---

## Quick Overview (For Everyone)

**What is this?**  
A file (`synopsys.md`) that turns an AI assistant into a chip design expert. Add it to [opencode](https://opencode.ai) (an open-source AI coding tool) and instantly get an engineer who knows Synopsys DC, ICC2, PrimeTime, Formality, VCS, and ICV.

**What can it do?**  
- Write correct Synopsys Tcl scripts from plain English prompts  
- Generate complete RTL-to-GDSII design flows  
- Debug timing violations, DRC/LVS errors  
- Explain tool concepts and help students learn  
- Automate repetitive EDA tasks  

**How does it work?**  
1. Install [opencode](https://opencode.ai)  
2. Add this agent (`synopsys.md`)  
3. Type `@synopsys <your request>` in any conversation  

---

## Contents of This Repository

```
SynopsysAgent/
├── README.md           ← You are here (guide for all audiences)
├── synopsys.md         ← The AI agent brain (the core file)
├── CLAUDE-FABLE-5.md   ← Reference: Anthropic Claude Fable 5 system prompt
└── LICENSE             ← Apache 2.0 — free to use and share
```

---

## Getting Started in 60 Seconds

### For Everyone

```bash
# 1. Install opencode (see opencode.ai)
# 2. Copy the agent to your global agents folder
cp synopsys.md ~/.config/opencode/agents/
# 3. Done! Now type @synopsys in any conversation
```

### For Faculty — Classroom Use

Place the agent in your course repository so all students have access:

```jsonc
// In opencode.json at your course repo root:
{
  "$schema": "https://opencode.ai/config.json",
  "agents": {
    "synopsys": {
      "description": "Synopsys EDA expert for coursework and labs",
      "path": "./agents/synopsys.md"
    }
  }
}
```

Students then run `@synopsys generate a dc_shell script for a 4-bit adder` and get a working synthesis script instantly — no manual Tcl memorization needed.

### For Companies — CI/CD Integration

Add to your design flow scripts. The agent fits into any infrastructure that supports opencode subagents (including Claude Code, Copilot, and custom LLM pipelines).

---

## Example Prompts (Try These)

| Your Role | Try Asking |
|-----------|-----------|
| **Student** | `@synopsys explain what compile_ultra does in plain English` |
| **Professor** | `@synopsys create a lab handout for synthesizing a 5-stage pipelined CPU` |
| **Researcher** | `@synopsys generate a dc_shell script for our DNN accelerator at 7nm, target 1GHz` |
| **Dean** | `@synopsys summarize how this tool helps students learn industry VLSI flows` |
| **Design Engineer** | `@synopsys write an ICC2 floorplan script with 70% utilization and 8 memory macros` |
| **TA** | `@synopsys create a .synopsys_dc.setup template with standard library paths` |

---

## What's Inside the Agent (synopsys.md)

The core file contains deep expertise across the entire Synopsys toolchain:

| Tool | Purpose | What the Agent Generates |
|------|---------|------------------------|
| **Design Compiler (dc_shell)** | Logic synthesis (RTL → gates) | Complete synthesis scripts, constraints, reports |
| **IC Compiler II (icc2_shell)** | Physical design (gates → layout) | Full P&R flow: floorplan → route → GDS |
| **PrimeTime (pt_shell)** | Static timing analysis | Timing reports, ECO guidance, constraint checks |
| **Formality (fc_shell)** | Formal verification | Equivalence checking scripts |
| **VCS** | RTL simulation | Testbenches, simulation scripts |
| **ICV / IC Validator** | Physical verification | DRC/LVS run decks and debugging |

---

## Technical Details (for Expert Companies)

### Supported Tools & Protocols

- **Synthesis**: dc_shell, Design Compiler Graphical, compile_ultra, topographical mode
- **Physical Design**: ICC2, floorplanning, power planning, placement, CTS, routing, GDS output
- **Timing**: PrimeTime STA, setup/hold/multi-corner analysis, timing closure strategies
- **Verification**: Formality (LEC), VCS (simulation), ICV (DRC/LVS)
- **Formats**: Verilog, SDC, SDF, DEF/LEF, GDSII, LEF, Milkyway, NDM

### Reference Flows

The agent documents complete Tcl scripts for:
- `.synopsys_dc.setup` library configuration
- Synthesis with `analyze → elaborate → compile_ultra → report → write`
- 13-stage ICC2 physical design flow
- PrimeTime multi-corner STA
- Formality equivalence checking setup

---

## Integration Options

| Platform | How to Use |
|----------|-----------|
| **opencode** | Copy to `~/.config/opencode/agents/` — global `@synopsys` |
| **Claude Code** | Reference `synopsys.md` in `CLAUDE.md` |
| **GitHub Copilot / Custom LLM** | Use the agent definition as a system prompt |

---

## Reference: Claude Fable 5 System Prompt

This repository includes [`CLAUDE-FABLE-5.md`](./CLAUDE-FABLE-5.md), the complete system prompt for **Anthropic's Claude Fable 5** — the most advanced generally available Claude model. It is sourced from the public [CL4R1T4S](https://github.com/elder-plinius/CL4R1T4S) repository by elder-plinius.

This document is a valuable reference for:
- **AI behavior design**: Study how safety, refusal handling, tone, and user wellbeing are encoded at the system level
- **Prompt engineering**: See how a production-grade system prompt is structured with clear sections, decision trees, and fallback behaviors
- **Agent architecture**: Understand the MCP app suggestion system, computer use skills, artifact storage patterns, and search instructions that power a state-of-the-art AI agent

While the SynopsysAgent focuses on EDA tool expertise, this system prompt represents the frontier of AI instruction design — relevant context for anyone building or studying advanced AI agents.

## License

Apache License 2.0 — free to use, modify, and share.

---

**Build By: anantha pavithra**

*Built for professors who teach, deans who invest, and companies who build the future of silicon.*
