# Test Plan for mkcombo_mul (SHAKTI C-Class FBox)

## 1. Overview
This document outlines the test plan for functionally verifying the `mkmbox` module of the SHAKTI C-Class FBox using Cocotb. The module performs various forms of multiplication as defined in the RISC-V ISA, particularly supporting instructions under the "M" extension (Multiply).

## 2. Design Under Test (DUT)

**Module Name**: `mkmbox`

### Interface Signals

**Inputs**:
- `ma_inputs_in1 [63:0]` – First operand
- `ma_inputs_in2 [63:0]` – Second operand
- `ma_inputs_funct3 [2:0]` – Operation selector
- `ma_inputs_wordop [0:0]` – Word operation (32-bit result expected)
- `EN_ma_inputs [0:0]` – Input enable
- `EN_mv_output [0:0]` – Output enable
- `CLK [0:0]`, `RST_N [0:0]` – Clock and reset

**Outputs**:
- `mv_output [63:0]` – Result of the multiplication
- `mv_output_valid [0:0]` – Indicates valid output
- `mv_ready [0:0]` – Indicates module ready to accept input

## 3. Features Being Verified

| Feature                  | Description                                    |
|--------------------------|------------------------------------------------|
| `MUL`                    | Signed × Signed lower 64 bits                  |
| `MULH`                   | Signed × Signed upper 64 bits                  |
| `MULHSU`                 | Signed × Unsigned upper 64 bits               |
| `MULHU`                  | Unsigned × Unsigned upper 64 bits             |
| WordOp Enabled (MULW)    | Return sign-extended 32-bit results           |
| Input Ready + Output Valid | Handshaking protocol correctness              |
| Random Operand Support   | Wide range of input values including edge cases |

## 4. Testing Methodology

- **Type**: Randomized and Directed Testing

### Random Testing:
- Randomized values for `in1`, `in2` over full 64-bit range.
- Random selection of `funct3` and `wordop` to hit all instruction variants.

### Directed Testing (Optional Extension):
- Edge cases:
  - Zero operands
  - Maximum positive and negative signed values
  - Unsigned boundaries

## 5. Functional Coverage Metrics

| Coverage Point | Bins (Values)                        | Coverage |
|----------------|--------------------------------------|----------|
| `funct3`       | 0, 1, 2, 3                           | 100%     |
| `wordop`       | 0, 1                                 | 100%     |
| `in1`          | -1, 0, 1, 2147483647, 2147483648, 4294967295 | 100% |
| `in2`          | -1, 0, 1, 2147483647, 2147483648, 4294967295 | 100% |
| `funct3 × wordop` | All combinations from above        | 100%     |

## 6. Pass/Fail Criteria

- The output value from `mv_output` must match the expected RISC-V multiplication result (based on `funct3` and `wordop`) for each random input.
- `mv_output_valid` must be asserted before reading output.
- Functional coverage file (`coverage_mkcombo_mul.yaml`) must show 100% bin hits.

## 7. Tools & Environment

| Component          | Version         |
|--------------------|------------------|
| Simulator          | Icarus Verilog   |
| Verification Tool  | Cocotb 1.9.2     |
| Coverage Tool      | cocotb-coverage 1.2.0 |
| Language           | Python 3.10      |

## 8. References

- [RISC-V Unprivileged ISA v2.2, M-extension]
- SHAKTI C-Class FBox Verilog source (`mkmbox.v`)
