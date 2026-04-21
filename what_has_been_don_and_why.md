# What Has Been Done And Why

## Purpose

This document records what was done during the April 21, 2026 AEON Writer OS session, why those decisions were made, who this work is for, what the expected outcome was, and what remains optional.

It exists to give a future reader one place to understand the real process, not just the original blueprint.

## Who This Is For

- Sourav, as the system owner and primary user.
- Any future maintainer reviewing the repository and trying to understand what actually happened on the live machine.
- Any caregiver, helper, or collaborator who needs the practical system state in plain language.

## High-Level Goal

The original goal was to move toward an AEON Writer OS style environment on an Arch-based machine with strong safety constraints:

- protect the live system
- avoid touching the internal Windows NVMe drive
- do easy and reversible work first
- prepare as much automation as possible
- adapt the plan to the real machine instead of forcing the blueprint blindly

## Reality Check Performed First

Before execution, the repository and the host system were audited.

What was discovered:

- The repository at `sourovdeb/arch_linux` contained useful scripts and design documents, but the implementation covered only part of the broader written blueprint.
- The target was not a disposable installer environment. It was the user's real running EndeavourOS system on an external SSD.
- The internal NVMe contained BitLocker Windows and had to remain untouched.
- The desktop environment was KDE Plasma, not GNOME, so the original GNOME-heavy plan could not be applied as written.
- NVIDIA existed on the machine but was explicitly deprioritized and treated as optional.

Why this mattered:

- Directly running the original install scripts would have been too risky on a live machine.
- The plan had to be adapted from install-time automation to safe, host-level package and configuration automation.
- Disk, partition, bootloader, and destructive operations had to be excluded entirely.

## Safety Decisions Taken

The session followed a safety-first approach.

Key choices:

- No partitioning.
- No formatting.
- No bootloader changes.
- No writes to the internal NVMe Windows drive.
- No automatic NVIDIA reconfiguration.
- Reversible package installs and user-level configuration only.
- Frequent Timeshift snapshots before and after major phases.

To support that, the following were done:

- sudo access was verified
- temporary automation privileges were enabled when needed
- Timeshift was installed
- a baseline snapshot was created before major AEON work began

## Repository Work Completed

The repository was first reviewed and syntax-checked.

Reviewed items included:

- `automate_arch_setup.sh`
- `partition_ssd.sh`
- `post_install.sh`
- `packages.txt`
- `BUILD_PLAN.md`
- `SOFTWARE_INVENTORY.md`
- `HARDWARE_COMPATIBILITY.md`
- `EXECUTION_GUIDE.md`
- `ANTICIPATED_ISSUES.md`
- `TOKEN_EFFICIENT_PLAN.md`

Because the repo documentation was broader than the safe live-host automation that actually existed, a separate execution framework was created outside this repo under `~/aeon/`.

## Protocol Documents Created

To keep the process explicit, safety and execution protocol documents were created under `protocols/` in this repository.

These were intended to document:

- cautious execution rules
- phased safe planning
- execution notes
- session status

Those files served as guardrails for the automation decisions taken later.

## AEON Runtime Framework Created

A new autonomous AEON framework was created under `~/aeon/` because the repository scripts were not suitable for direct live-system execution.

This included:

- a shared shell safety library
- a master orchestrator script
- phase scripts for the AEON build
- helper Python scripts
- logs, config, and services directories

Important files created there included:

- `~/aeon/lib/safety.sh`
- `~/aeon/run-aeon.sh`
- `~/aeon/phases/00-foundation.sh`
- `~/aeon/phases/01-accessibility.sh`
- `~/aeon/phases/02-writing.sh`
- `~/aeon/phases/03-podcast.sh`
- `~/aeon/phases/04-publishing.sh`
- `~/aeon/phases/05-ai.sh`
- `~/aeon/phases/06-notifications.sh`
- `~/aeon/phases/07-safety-tools.sh`
- `~/aeon/phases/08-services.sh`
- `~/aeon/phases/09-habits.sh`
- `~/aeon/phases/10-verify.sh`
- `~/aeon/phases/99-nvidia-optional.sh`

Python helpers were also created for dashboard, transcription, AI routing, notifications, publishing, habits, log translation, and verification.

## Process Followed

The actual process was:

1. Clone and audit the repository.
2. Inspect the real machine and storage layout.
3. Identify risks and reject unsafe install-time assumptions.
4. Write protocol documents to capture safety and sequencing.
5. Install Timeshift and create a rollback point.
6. Build a safer live-host AEON automation framework under `~/aeon/`.
7. Validate shell and Python syntax before execution.
8. Run the orchestrator on the live machine.
9. Monitor the build and patch helper defects when safe to do so.
10. Verify final results and create final snapshots.

## Issues Encountered During Execution

Several practical issues appeared during the live run.

### 1. Safety library arithmetic bug

An internal counter in the shared safety library produced a shell arithmetic error.

What was done:

- the counting logic was rewritten more safely using `awk`

Why:

- the failure was in the orchestration layer, not in system state
- patching it was low risk and necessary for the rest of the run to continue correctly

### 2. Flatpak progress and prompt ambiguity

Flatpak produced long-running output and the terminal sometimes appeared to be waiting for input even when no visible prompt was shown.

What was done:

- monitoring continued conservatively
- only minimal input was sent when necessary

Why:

- this avoided interrupting a valid install while still respecting the request to answer prompts quickly

### 3. AUR package availability gaps

Some packages referenced by the plan were not available exactly as expected.

Known example:

- `languagetool-bin` was not available from the configured sources during the run

Why this matters:

- it means the environment is functional but not perfectly identical to the aspirational package list in the docs

### 4. Python package install policy on Arch

System Python rejected direct user pip installs because of the externally managed environment rules.

What was done:

- the AEON helper logic was corrected to use an isolated virtual environment under `~/aeon/.venv-tools`
- `proselint` and `openai-whisper` were installed there
- user-facing launchers were exposed on the local path

Why:

- this respects Arch packaging policy
- it avoids polluting or breaking system Python
- it gives the expected tools in a safer way

### 5. Snapshot logging noise

Timeshift snapshots succeeded, but some runs printed a benign shell wrapper message after success.

What was done:

- later helper behavior was hardened to filter that noise for future runs

## What The Build Actually Achieved

The automated AEON build completed successfully on the live system.

The final result reported all core phases passed:

- `00-foundation`
- `01-accessibility`
- `02-writing`
- `03-podcast`
- `04-publishing`
- `05-ai`
- `06-notifications`
- `07-safety-tools`
- `08-services`
- `09-habits`
- `10-verify`

What this produced in practice:

- writing directory structure under `~/Writing`
- writing tools such as pandoc, hugo, ghostwriter, zathura, libreoffice, and Obsidian
- podcast tooling including Audacity and transcription support
- AI tooling with Ollama and model downloads
- notification and automation timers/services
- safety tooling such as Cockpit and recurring snapshot support
- habits and launcher scripts
- verification output confirming the expected core pieces were present

## Expected Outcome

The expected outcome of the session was not a fresh installer image. It was a safe transformation of the existing live machine into a working AEON-style creative environment without endangering the Windows disk or the currently running system.

That expected outcome was:

- a writer-first workstation
- podcast and publishing support
- offline-capable local AI support
- large, readable, low-friction configuration choices
- rollback points before and after major changes
- optional, not forced, advanced components

This outcome was substantially achieved.

## What Was Intentionally Left Optional

Some items were intentionally not forced.

- NVIDIA tuning remained manual and optional.
- Private services scaffolding was created, but some services were left opt-in rather than auto-started.
- Missing or unavailable extras such as `languagetool-bin` were not forced through unsafe workarounds.

Why:

- the priority was a safe, usable system, not maximum feature completeness at any cost

## Current Practical Status

At the end of the session:

- the AEON build completed successfully
- verification passed
- final Timeshift snapshots were created
- temporary passwordless sudo was no longer present
- the main remaining work was optional or manual follow-up only

Practical follow-up items after the build:

- reboot once so everything settles cleanly
- test the daily workflow tools
- run the optional NVIDIA script only if desired
- optionally revisit unavailable extras later

## Why This Document Exists

The repo blueprint describes a strong vision, but the real session required adaptation. This document exists so that future readers understand:

- what was planned
- what was safe to do
- what was actually done
- why the execution diverged from the original install-oriented path
- what the resulting system should now provide

## Short Conclusion

The session successfully converted the original AEON idea into a live-system-safe implementation path.

The important result is not that every aspirational item in the repository was installed exactly as written. The important result is that the live machine was upgraded into a practical AEON-style creative environment while preserving safety, reversibility, and compatibility with the actual host.