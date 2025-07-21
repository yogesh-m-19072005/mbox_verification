# Cocotb Verification: mkmbox (SHAKTI C-CLASS MBox)

This repository contains the functional verification of the `mkmbox` module from the SHAKTI C-Class MBox using Cocotb.

---

## 📁 Contents

- `test_mkmbox.py` – The Cocotb testbench.
- `Makefile` – Used to run the simulation with Icarus Verilog.
- `mkmbox_mul_coverage.yaml` – Functional coverage results.
- `testplan.md` – Detailed verification test plan.
- `results.xml` – Cocotb regression report.

---

## ▶️ Running the Simulation

Activate your Python environment and install dependencies:

```bash
pip install cocotb cocotb-coverage==1.2.0
```

Then, run the testbench using:

```bash
make
```

Ensure you have Icarus Verilog installed and available in your system's PATH.

---
