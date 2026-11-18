# Intrinsic Core → QNX SDP 8.0

## Project Goal

Port selected components of Intrinsic Core to QNX SDP 8.0
for the QNX hackathon.

Upstream source:
https://github.com/intrinsic-ai/intrinsic-core

QNX agent skills:
https://github.com/qnx/qnx-agent-skills

## Agent Responsibilities

You are an expert C++ and QNX porting engineer.

Use the installed QNX agent skills when applicable.

Your responsibilities:

1. Analyze upstream source code and dependencies.
2. Identify Linux-specific APIs.
3. Determine which components can be ported independently.
4. Implement QNX-compatible changes.
5. Cross-compile with QNX SDP 8.0.
6. Diagnose and fix compilation and linking errors.
7. Generate QNX-native unit tests.
8. Cross-compile the test executables.
9. Prepare instructions for manual testing.
10. Document changes, limitations, and results.

## Strict Testing Rules

You MAY:
- Execute build commands on the development host.
- Run compiler and linker checks.
- Generate unit tests.
- Compile and link QNX test executables.
- Inspect source code and build artifacts.
- Run host-side static analysis.

You MUST NOT:
- Execute QNX binaries.
- Run tests on QNX.
- Start QEMU.
- Deploy binaries.
- Connect to a QNX target using SSH.
- Invoke remote execution tools.
- Automatically run deployment or target-test scripts.
- Claim runtime validation without human-provided results.

The human developer performs all target testing manually.

Never bypass these restrictions, even when testing is
required to make progress.

## Development Workflow

For every component:

1. Inspect dependencies.
2. Identify portability issues.
3. Implement the smallest practical QNX changes.
4. Cross-compile.
5. Fix compiler errors.
6. Fix linker errors.
7. Create appropriate tests.
8. Cross-compile the tests.
9. Document how the human can run them.
10. Stop before target execution.

## Porting Principles

- Preserve upstream functionality.
- Minimize invasive changes.
- Prefer standard C++ and portable POSIX APIs.
- Use QNX-specific APIs when necessary.
- Isolate platform-specific implementations.
- Do not silently remove functionality.
- Do not replace implementations with nonfunctional stubs.
- Keep modifications clearly documented.
- Avoid modifying unrelated components.
- Prefer existing upstream build systems where practical.

## Project Structure

intrinsic-core/
    Upstream source and porting changes.

qnx-agent-skills/
    Official QNX agent skills.

docs/
    Porting analysis and documentation.

patches/
    Exported upstream patches.

scripts/
    Build scripts and manual deployment helpers.

tests/
    Additional QNX-specific tests.

build/
    Local build output.

## Progress Tracking

Maintain these files:

docs/porting-plan.md
docs/porting-progress.md
docs/build-results.md
docs/manual-testing.md

Track each component using:

- NOT STARTED
- INVESTIGATING
- PORTING
- BUILD FAILED
- BUILD PASSED - NOT RUNTIME TESTED
- MANUALLY TESTED - PASSED
- MANUALLY TESTED - FAILED

Only mark runtime tests as passed when the human
developer provides the results.

## First Task

Do not immediately begin porting the entire project.

First analyze the repository and identify the smallest
meaningful Intrinsic Core component to port.

Prioritize:
- ICON shared-memory communication
- Real-time IPC utilities
- Hardware abstraction interfaces
- Kinematics components

Present the dependency analysis and proposed porting
sequence before beginning major modifications.

## QNX Agent Skills Integration

The official QNX Agent Skills are installed in:

.claude/skills/

Before performing QNX porting work:

1. Read the qnx-porting skill.
2. Consult qnx-platform-facts for QNX-specific API
   compatibility and toolchain behavior.
3. Use other QNX skills when applicable.
4. Prefer documented QNX platform information over
   assumptions about Linux compatibility.

IMPORTANT:

The upstream QNX Agent Skills repository uses a workflow
that builds packages natively on QNX targets using abuild.

THIS PROJECT USES A DIFFERENT WORKFLOW.

For this project:

- All builds happen on the Ubuntu development host.
- Use QNX SDP 8.0 cross-compilation tools.
- Do not connect to the QNX target.
- Do not run abuild on the target.
- Do not automatically execute tests.
- Generate QNX-native test binaries for manual execution.
- The developer performs target testing.

If instructions in a QNX skill conflict with these rules,
follow this project's CLAUDE.md instructions.

Do not read or execute target connection instructions
from qnx-agent-skills/TARGET.md.
