# CORE-V ELF psABI specification

## Table of Contents
1. [ELF Object Files](#elf-object-file)
	* [Relocations](#relocations)

## Copyright and license information

This CORE-V ELF psABI specification document is

 &copy; 2020 Simon Cook <simon.cook@embecosm.com>

It is licensed under the Creative Commons Attribution 4.0 International License
(CC-BY 4.0).  The full license text is available at
https://creativecommons.org/licenses/by/4.0/.

# Introduction

This document is intended to be a suppliment to the RISC-V psABI document,
available at https://github.com/riscv/riscv-elf-psabi-doc. This document only
describes differences between that specification required for a functioning
CORE-V system.

Where possible, sections of this document will be placed in the same order as
the RISC-V psABI document.

# <a name=elf-object-file></a> ELF Object Files

## <a name=relocations></a> Relocations

Relocations needed for CORE-V instructions use the upper half of the "Reserved
for nonstandard ABI extensions block" (224-255). The lower half of the block
(192-253) continue to be reserved for nonstandard extensions which may still
conflict with each other.

The following table describes the CORE-V ELF relocations.

Enum | ELF Reloc Type       | Description                    | Field      | Calculation
:--- | :---------------     | :----------                    | :----      | :----------
224  | R_RISCV_CVPCREL_UI12 | Unsigned pc-relative reference | _I-type_   | S + A - P
225  | R_RISCV_CVPCREL_URS1 | Unsigned pc-relative reference | _RS1-type_ | S + A - P
226-255 | *Reserved*        | Reserved for future CORE-V use

### Field symbols

The following table describes the fields used in the above table:

Variable   | Description
:-------   | :----------
_I-Type_   | Specifies the immediate field in the I-type instruction
_RS1-Type_ | Specifies an immediate in the RS1 location of an I-type instruction

### Unsigned pc-relative reference

These are pc-relative references analogous to relocations such as
R_RISCV_PCREL_LO12, with the difference that these fields are unsigned and the
instruction must reach the target address (i.e. the destination must be within
the reach of that instruction).
