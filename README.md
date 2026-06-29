# QNX-Full-Stack

Roadmap and practice repo for becoming interview-ready as a **QNX Systems Engineer (Automotive Digital Cockpit / ADAS)**, with a deliberate bridge to an existing **Android Automotive Framework** background — most production cockpit SoCs run QNX as a Type-1 hypervisor host with Android Automotive as a guest OS, so credibility on *both* sides of that boundary is the differentiator this repo is built around.

**Strategy:** Broad microkernel foundation → survey 7 tracks → specialize in 2 (bias toward the Hypervisor/Multi-OS track, which leverages existing Android framework experience) → interview prep.
**Timeline:** 5 months.

> **Why this repo exists alongside Android-Full-Stack:** Android Automotive Framework Engineer JDs increasingly assume familiarity with the host RTOS underneath the IVI guest. Being able to speak to both the AOSP HAL boundary *and* the QNX Hypervisor/vdev boundary on the same SoC is rare and directly valuable for automotive Tier-1/OEM roles (digital cockpit, ADAS gateway, mixed-criticality SoCs).

---

## Progress Tracker

### Phase 1 — Foundation (Month 1)

- [ ] Microkernel architecture (procnto, what stays in-kernel vs. what runs as a resource manager/server)
- [ ] Process & thread model (POSIX threads, priority-preemptive scheduling, Adaptive Partitioning Scheduler/APS)
- [ ] Message-passing IPC (channels/connections, `MsgSend`/`MsgReceive`/`MsgReply`, pulses, signals — the QNX analog to Binder)
- [ ] Memory model (address spaces, typed memory, shared memory objects)
- [ ] Toolchain & build (QCC/GCC 12 toolchain, `.build` buildfiles, `mkifs` image build, IFS vs. flash filesystem images)
- [ ] Debugging toolkit (`pidin`, `slogger2`, `coreinfo`, System Profiler/`tracelogger`, QNX Momentics IDE, QNX Toolkit for VS Code)

**Resources:**
- [qnx.software](https://qnx.software) — official SDP 8.0 docs, Foundry27 community
- QNX SDP 8.0 non-commercial license (free, browser-based install) — get hands-on without a corporate seat
- *Getting Started with QNX Neutrino* — QSSL/BlackBerry reference manual
- *QNX Momentics / Neutrino Programmer's Guide* (IPC, resource managers, process model chapters)

---

### Phase 2 — Survey Sprints (Month 2)

~4 days per track. Goal: find aptitude/interest and identify the strongest leverage point before committing.

| # | Track | Status | Core Components | Mini Lab |
|---|---|---|---|---|
| 1 | Resource Managers & Drivers | [ ] | `resmgr` API, `io-*` servers, devnode model (QNX's equivalent of the AOSP HAL layer) | Write a minimal character resource manager (`/dev/mydevice`) handling open/read/write |
| 2 | **Hypervisor & Multi-OS Integration** | [ ] | QNX Hypervisor 8.0 (Type-1), `vdev` framework, Guest OS bring-up (Android Automotive / Linux), virtio & shared-memory inter-VM channels | Boot an Android Automotive guest under QNX Hypervisor on a reference VM; exchange a message across the hypervisor boundary |
| 3 | BSP & Board Bring-up | [ ] | `startup` code, `.build` buildfiles, IFS image construction, bootloader handoff, board config | Bring up a reference BSP on QEMU (or a dev board); trace boot from `startup` to `procnto` |
| 4 | Functional Safety (ASIL) | [ ] | ISO 26262, IEC 61508, QNX OS for Safety, freedom-from-interference, ASIL decomposition | Read a QNX safety manual; map a freedom-from-interference argument for a hypothetical partitioned cluster/IVI design |
| 5 | Networking & Comm Middleware | [ ] | `io-pkt` network stack, POSIX sockets, SOME/IP / DDS bridging (vsomeip), CAN bus IPC | Write a simple `io-pkt` socket app; bridge a CAN signal into a QNX resource manager |
| 6 | Graphics & Multimedia (Cluster) | [ ] | Screen Graphics subsystem (`screen`/`gf`), composition manager, third-party rendering engines paired with QNX clusters (Crank Storyboard, Kanzi) | Render a simple composited scene to a display using the Screen API |
| 7 | Adaptive Partitioning & System Stability | [ ] | APS scheduler partitions, System Profiler tracing, High Availability Manager (HAM), self-healing/process restart | Configure two APS partitions, induce a fault, observe HAM detect and restart |

**Checkpoint at end of Month 2:** Pick top 2 tracks based on:
- Aptitude/interest from the sprints above
- Market demand (automotive Tier-1/OEM digital cockpit roles in the region)
- Leverage from existing experience — **Track 2 (Hypervisor & Multi-OS) has the strongest leverage** given direct Android Automotive head-unit experience; Track 5 (Comm Middleware) also leverages prior vsomeip/SOME-IP exposure

**Chosen tracks for deep dive:**
1. `____________________`
2. `____________________`

---

### Phase 3 — Deep Dive (Months 3–4)

~6–8 weeks per chosen track. For each:
- [ ] Read the relevant subsystem documentation and any available reference source top to bottom
- [ ] Build a non-trivial lab touching a real resource manager or hypervisor boundary (not a toy app)
- [ ] Be able to explain a design trade-off in the subsystem from memory (e.g., "why message-passing IPC over shared memory for this case")
- [ ] Document findings in the track's own `README.md`

---

### Phase 4 — Interview Prep (Month 5)

- [ ] Mock interviews: microkernel internals, IPC tracing, resource manager design walkthroughs
- [ ] System-design questions specific to chosen tracks (e.g., "design a fail-safe handoff between the QNX safety domain and an Android IVI guest after a cluster reset")
- [ ] Polish repo as portfolio — push all labs, notes, and writeups
- [ ] Resume tailored to chosen tracks, explicitly framing the Android Automotive + QNX Hypervisor combination
- [ ] Apply

---

## Repo Structure

```
qnx-full-stack/
├── README.md                      # this file — roadmap + progress tracker
├── 00-foundation/
│   ├── microkernel-ipc/
│   ├── process-model/
│   ├── build-toolchain/
│   └── debugging-toolkit/
├── 01-resource-managers/
├── 02-hypervisor-multi-os/
├── 03-bsp-board-bringup/
├── 04-functional-safety/
├── 05-networking-middleware/
├── 06-graphics-multimedia/
├── 07-adaptive-partitioning/
└── interview-prep/
```

Each track folder contains:
- `README.md` — theory notes + QNX documentation pointers
- `labs/` — hands-on practice projects

---

## Notes
