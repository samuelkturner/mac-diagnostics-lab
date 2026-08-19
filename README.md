# Mac Hardware Troubleshooting & Display Diagnostics Lab

## Overview

This project documents a real-world hardware diagnostic investigation and repair performed on a **MacBook Pro (Retina, 13-inch, Early 2015)** presenting with a complete black screen on boot. Using a systematic troubleshooting methodology, I identified the root cause, confirmed core hardware integrity, isolated the fault to the internal display flex cable, and performed the physical repair — mirroring the full diagnose-and-resolve workflow used in professional IT support environments.

---

## Device Specifications

| Property | Details |
| ----------------- | ------------------------------------------ |
| **Model** | MacBook Pro (Retina, 13-inch, Early 2015) |
| **OS** | macOS Monterey 12.7.6 |
| **Processor** | 2.7 GHz Dual-Core Intel Core i5 |
| **Memory** | 8 GB 1867 MHz DDR3 |
| **Graphics** | Intel Iris Graphics 6100 — 1536 MB |
| **Serial Number** | C02RX63YFVH5 |

---

## Problem Statement

The MacBook powered on — keyboard backlight illuminated and the system appeared to be running — but the internal display remained completely black. No Apple logo, no login screen, and no visible output of any kind on the built-in screen.

**Goal:** Determine whether the fault was caused by a software issue, core hardware failure, or an isolated display hardware problem — then resolve it.

---

## Tools & Technologies Used

- macOS Monterey
- Apple Diagnostics (built-in hardware test utility)
- External display via HDMI (Hisense 65” 4K TV)
- Mini DisplayPort to HDMI adapter
- SMC Reset (System Management Controller)
- NVRAM Reset (Non-Volatile RAM)
- Precision screwdriver set (Pentalobe/Torx)
- Plastic spudger / opening tools
- Anti-static tweezers
- iFixit Display LVDS Cable (MacBook Pro Retina, 2012–2015, complete assembly)

---

## Troubleshooting Methodology

### Step 1 — Document the Symptom

Observed and photographed the MacBook powered on with a completely black internal display. Keyboard backlight confirmed the system was receiving power and attempting to boot.

[![Black screen symptom](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/01-black-screen.jpg)](/samuelkturner/mac-diagnostics-lab/blob/main/01-black-screen.jpg)

---

### Step 2 — Attempt SMC Reset

The **System Management Controller (SMC)** manages low-level hardware functions including display output and power management. Resetting it can resolve black screen issues caused by firmware glitches.

**Procedure:**

- Shut down the MacBook completely
- Held **Shift + Control + Option + Power** simultaneously for 10 seconds
- Released all keys and powered the MacBook back on

**Result:** No change. Internal display remained black.

---

### Step 3 — Attempt NVRAM Reset

**NVRAM** stores system settings including display configuration and resolution preferences. A corrupted NVRAM entry can sometimes cause display output failures.

**Procedure:**

- Powered off the MacBook
- Held **Command + Option + P + R** immediately after pressing the power button
- Held the keys for approximately 20 seconds until the startup chime sounded twice

**Result:** No change. Internal display remained black.

---

### Step 4 — External Display Test (HDMI 1)

Connected the MacBook to an external display via Mini DisplayPort to HDMI adapter to determine whether the system was outputting video at all.

**Initial result:** TV displayed **“Weak or no signal”** on HDMI 1 — no video output detected.

[![Weak or no signal on HDMI 1](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/02-hdmi-no-signal.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/02-hdmi-no-signal.jpeg)

---

### Step 5 — External Display Test (HDMI 2 — Reseated Connection)

Switched the HDMI cable to **HDMI 2** on the TV and reseated the adapter connection on the MacBook.

**Result:** macOS login screen appeared on the external display — system confirmed fully operational.

[![Successful external display — macOS login screen](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/03-successful-display.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/03-successful-display.jpeg)

**Significance:** This confirmed the MacBook’s logic board, GPU, and operating system were all functioning correctly. The fault was isolated to the internal display hardware.

---

### Step 6 — System Verification

After logging in, verified full system functionality by navigating macOS, opening applications, and confirming normal operation.

[![macOS desktop fully functional](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/04-macos-desktop.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/04-macos-desktop.jpeg)

Checked **About This Mac** to document exact device specifications.

[![About This Mac — device specs](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/05-about-this-mac.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/05-about-this-mac.jpeg)

---

### Step 7 — Apple Diagnostics

Ran **Apple Diagnostics** to perform a comprehensive hardware test of all core system components including the logic board, memory, storage, and GPU.

**Procedure:**

- Shut down the MacBook
- Held the **D key** while pressing the power button
- Selected language and agreed to diagnostic terms
- Allowed the diagnostic to complete (~3 minutes)

[![Diagnostics language selection](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/06-diagnostics-language.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/06-diagnostics-language.jpeg)

[![Run Diagnostics agreement screen](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/07-diagnostics-agreement.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/07-diagnostics-agreement.jpeg)

[![Checking your Mac — progress bar](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/08-diagnostics-running.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/08-diagnostics-running.jpeg)

**Result:** ✅ **No issues found. Reference Code: ADP000**

[![Apple Diagnostics — No issues found ADP000](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/09-diagnostics-result.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/09-diagnostics-result.jpeg)

**Significance:** ADP000 confirms all tested hardware components passed. The black screen fault is definitively isolated to the internal display panel or display flex cable — not the logic board, GPU, RAM, or storage.

---

## Repair: Display Flex Cable (LVDS) Replacement

With the fault isolated to the internal display cable, I sourced a replacement part and performed the physical teardown and repair.

**Part used:** iFixit Display LVDS Cable — compatible with MacBook Pro Retina (2012–2015), complete assembly

### Step 8 — Bottom Case Removal & Internal Access

Removed the Pentalobe screws along the bottom case perimeter and lifted off the lower case to expose the battery, fan, and logic board. Disconnected the battery from the logic board first to prevent any short circuits while working near the board.

[![Bottom case removed, internals exposed](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/10-internals-exposed.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/10-internals-exposed.jpeg)

---

### Step 9 — Locating and Freeing the Display Cable Routing

Traced the LVDS cable path from the logic board connector, along the left hinge, up through the display clutch assembly, and into the back of the LCD panel. Removed the screws securing the rear housing bracket near the hinges to access the full cable run.

[![Tracing LVDS cable routing near the hinge](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/11-cable-routing.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/11-cable-routing.jpeg)

---

### Step 10 — Removing the Failed Cable

Used a plastic spudger to work the old flex cable free from its adhesive/foam channel along the hinge without stressing either connector end, then unlatched the ZIF connectors at the logic board and display panel to fully remove the failed cable.

[![Old and new LVDS cables removed for comparison](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/12-old-cable-removed.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/12-old-cable-removed.jpeg)

---

### Step 11 — Installing the Replacement Cable

Routed the new iFixit LVDS cable along the original path through the hinge assembly, seated the display-panel-end connector first, then the logic board ZIF connector — confirming each latch was fully closed and the cable sat flush. Pressed the cable back into its foam channel to prevent strain during normal lid open/close cycles.

[![New LVDS cable connected and routed](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/13-new-cable-installed.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/13-new-cable-installed.jpeg)

---

### Step 12 — Reassembly

Reinstalled the rear housing bracket and hinge-area screws, reconnected the battery, and closed up the bottom case, tightening screws in a center-out pattern to avoid warping the case.

---

### Step 13 — Post-Repair Verification

Powered on the unit and confirmed successful boot directly to the internal display, with the macOS login screen rendering correctly for both user profiles — no flicker, dead pixels, or backlight issues observed.

[![Successful boot to internal display post-repair](https://github.com/samuelkturner/mac-diagnostics-lab/raw/main/14-repair-verified.jpeg)](/samuelkturner/mac-diagnostics-lab/blob/main/14-repair-verified.jpeg)

**Result:** ✅ Repair successful. Internal display fully restored.

---

## Root Cause Analysis

| Component | Status |
| ----------------------- | ---------------------------------------------- |
| Logic Board | ✅ Passed |
| GPU / Graphics | ✅ Passed |
| RAM | ✅ Passed |
| Storage | ✅ Passed |
| External Video Output | ✅ Functional |
| Internal Display (pre-repair) | ❌ Black screen — hardware fault confirmed |
| Internal Display (post-repair) | ✅ Fully restored |

**Conclusion:** The MacBook Pro's black screen was caused by a failed internal display flex (LVDS) cable — a known issue on Early 2015 MacBook Pro models. All other core hardware (logic board, GPU, RAM, storage) tested and functioned normally throughout. Replacing the LVDS cable fully resolved the issue.

---

## Key Takeaways

- Applied a structured, layered diagnostic approach — ruling out software causes before escalating to hardware investigation
- Used external display testing to isolate the fault to a specific subsystem without disassembling the device
- Leveraged Apple’s built-in diagnostic utility to confirm hardware integrity and generate a reference code for documentation
- Performed a full internal teardown, connector-level cable replacement, and reassembly following the diagnostic findings
- Verified repair success through direct hardware testing rather than assumption
- Documented all steps, results, and findings in a format consistent with professional IT ticketing and hardware triage workflows

---

## Project Media

📹 [Watch the full troubleshooting walkthrough](https://youtu.be/O2fswLUSTfQ?is=i4KtEyxC27f_i7an)

---

## Connect

**Samuel K. Turner**
[LinkedIn](https://linkedin.com/in/samuelkturner) | [GitHub](https://github.com/samuelkturner)

Attachments area
Preview YouTube video MacBook Pro Hardware Diagnostics & Display Repair LabPreview YouTube video MacBook Pro Hardware Diagnostics & Display Repair Lab
