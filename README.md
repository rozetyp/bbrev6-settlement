# BBrev(6): the 388 holdouts are settled by the BB(6) project

All 388 BBrev(6) holdouts (Shawn Ligocki, July 31, 2025, [`BBrev6_holdouts_388.txt`](https://wiki.bbchallenge.org/w/images/8/86/BBrev6_holdouts_388.txt)) are non-halting, and every one is already covered by mxdys's BB(6) work. Together with the champion `1RB1LD_1LC1RE_0LD0LC_0RE0RF_0RA1RZ_1RF1RA`, this gives **BBrev(6) = 537,556**, assuming the July 2025 reversible enumeration is complete for halting machines.

## Evidence

| Evidence | Machines |
| --- | --- |
| Settled locally by standard deciders and also proved by name in the BB(6) Rocq files | 102 |
| Settled locally by standard deciders; not named in any BB(6) file, but settled by the decider family used in the BB(6) TNF enumeration (`verify/Enumerate62.v`) | 212 |
| Not settled locally; proved by name in the BB(6) Rocq files (`RRBAv3/4/5.v`, all 74 references checked against the source) | 74 |
| **Total** | **388** |
| A decider claiming a machine **halts** | 0 |

A cross-check that doesn't depend on any of the tools above: among all BB(6) holdout lists on the wiki, reversible machines (including L/R mirror images) appear 78 times in the June 2024 lists (12091/12325), 7 times in July 2024 (7296), and **0 times in every list since then, including `BB6_holdouts_815.txt` (Sept 24, 2026)**.

The per-machine details are in `bbrev6_settlement_table.csv`, one row per holdout: index (0-based line number), machine, local decider and parameters, and BB(6) Rocq file:line.

## Local runs

| Tool | Repo @ commit | Machines settled | Status |
| --- | --- | --- | --- |
| mxdys C++ deciders: MitM-CTL (NG, RWL_mod, CPS_LRU) and FAR | [ccz181078/TM](https://github.com/ccz181078/TM) `FAR` @ f901819 | 297 MitM-CTL (internal verifier on), 7 FAR (internal check disabled; 3 of these were run on the mirror image) | One Rocq `solve_cert` lemma per machine in `bbrev6_ctl_lemmas.v`, in the format of busycoq `BB6/verify/CTLv1.v`. **Not yet compiled.** |
| Iijil MITM-WFAR | [Iijil1/MITMWFAR](https://github.com/Iijil1/MITMWFAR) @ 3937731 | 10 | Full certificates in `mitmwfar_full_certs.txt`, re-checked with `-fc`: 10/10 pass |
| Iijil Bouncers | [Iijil1/Bouncers](https://github.com/Iijil1/Bouncers) @ cb57740 | 0 | — |

Reference database: [ccz181078/busycoq](https://github.com/ccz181078/busycoq) `BB6` @ 27b8b41 (Sept 30, 2026).

`lines.txt` holds the exact decider invocation for each of the 304 C++ results; all 304 reproduce. As a negative control, every configuration that settled anything was run on five known halting machines, and none was called non-halting.

## Caveats

- **The 304 Rocq lemmas haven't been compiled yet.** The next step is to drop `bbrev6_ctl_lemmas.v` into busycoq `BB6/verify` and build.
- **The 212 machines not named in BB(6) files** rest on two things: the same deciders settling them here, and their absence from every BB(6) holdout list. That they were settled inside `Enumerate62.v` is an inference, not checked machine by machine.
- **The value BBrev(6) = 537,556** also depends on the completeness of the reversible enumeration (`Enumerate.py --only-reversible`) for halting machines.

## Also available

An independent hand-found proof for holdout #0, `1RB1RF_1RC0LA_1RD---_1LE0RC_0LE1LA_0RF0RD`. Its tape always returns to four 1s, and the gap lengths satisfy c − a ≡ 2 (mod 4) at the checkpoints, giving five lemmas that are closed under the dynamics. There is a certificate plus a small independent checker. Available on request.
