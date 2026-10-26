# crython
Crython is an experimental native-compiled programming language exploring systems-level control, Python-like productivity, deterministic memory management, and AI-first computing. Building toward Cryda, a unified CPU/GPU compute and memory abstraction. Initial release target: December 21, 2026.


# Crython


<img width="1254" height="1254" alt="Futuristic Crython Binary Gear Logo" src="https://github.com/user-attachments/assets/dea3f405-760d-4523-97c9-d88d2216d9a8" />



### A new programming language for native performance, systems control, and AI engineering.

**Write with the productivity of a high-level language. Build toward the control of a systems language. Compute across CPUs and GPUs.**

Crython is an independent programming-language research and engineering project exploring how modern language design, deterministic memory management, native compilation, and AI-oriented computing can work together in one developer experience.

The goal is not to create another syntax on top of an existing language. The goal is to investigate what a programming language built for the next generation of systems and AI workloads could look like.

**Initial public release target: December 21, 2026.**

*We are building in public. Stay tuned.*

---

## Table of contents

- [The vision](#-the-vision)
- [Why Crython?](#-why-crython)
- [Core design principles](#-core-design-principles)
- [The Crython ecosystem](#-the-crython-ecosystem)
- [Cryda: unified CPU and GPU computing](#-cryda-unified-cpu-and-gpu-computing)
- [Language design](#-language-design)
- [Architecture](#-architecture)
- [Performance philosophy](#-performance-philosophy)
- [Roadmap to the initial release](#-roadmap-to-the-initial-release)
- [What the first release aims to deliver](#-what-the-first-release-aims-to-deliver)
- [What Crython is not yet](#-what-crython-is-not-yet)
- [Getting involved](#-getting-involved)
- [Project status](#-project-status)
- [Stay tuned](#-stay-tuned)

---

## 🔭 The vision

Modern software development often forces engineers to choose between different kinds of productivity.

High-level languages make experimentation, data processing, and AI development accessible. Systems languages offer more direct control over memory, execution, and resource management. GPU programming frameworks unlock parallel computation but introduce their own programming models, memory rules, and tooling.

Crython explores a different direction: **a language and runtime designed to bring these concerns into a coherent programming model.**

The long-term vision is a native-compiled language with:

- A productive, readable programming experience.
- Predictable execution and explicit resource ownership.
- Compile-time checks for selected memory and type errors.
- Native code generation through established compiler infrastructure.
- First-class numerical and scientific computing.
- A path toward CPU and GPU programming through a unified compute interface.
- An ecosystem designed to support machine learning, simulation, inference, and systems engineering.

These are design goals, not claims that all these capabilities already exist.

Crython will be developed incrementally, with each milestone backed by working software, tests, benchmarks, and documented limitations.

## 💡 Why Crython?

AI systems increasingly involve much more than calling a model API. They involve data pipelines, tensor operations, numerical kernels, inference runtimes, memory movement, parallel execution, and deployment constraints.

We want to explore a language ecosystem in which these components can eventually work together without forcing developers to reason about an entirely different abstraction at every layer.

Crython is motivated by five questions:

1. **Can high-level productivity coexist with native compilation?**
2. **Can memory ownership and resource lifetimes be easier to reason about without requiring a tracing garbage collector?**
3. **Can scientific and AI workloads feel natural without hiding important execution costs?**
4. **Can CPU and GPU computation share a coherent programming interface while respecting their physical differences?**
5. **Can a small, independently developed language grow through measurable milestones rather than promises of instant completeness?**

Crython is our attempt to investigate these questions in an open, testable engineering project.

---

## 🧭 Core design principles

### 1. Native compilation first

Crython is intended to compile programs into native executables rather than depend entirely on an interpreter at runtime.

The initial implementation may use an established native compiler as a transitional backend. LLVM or another mature backend can be evaluated as the compiler frontend and intermediate representation mature.

The objective is to reuse proven compiler infrastructure where it makes sense, rather than reinvent every layer.

### 2. Explicit memory semantics

Memory behavior should be understandable, testable, and predictable.

Crython aims to explore:

- Ownership-aware resource management.
- Borrowing and controlled access to data.
- Compile-time validation of supported lifetime and mutation rules.
- Deterministic cleanup where applicable.
- Clear rules for buffers shared with external libraries and accelerators.

Memory safety will be introduced in stages. A small set of implemented checks must not be confused with complete memory safety.

### 3. High-level expression, low-level awareness

The language should make common operations readable without concealing the costs that matter.

Developers should be able to express numerical algorithms clearly while retaining access to relevant information about allocations, data movement, parallel execution, and backend selection.

### 4. CPU-first development, GPU-aware architecture

The CPU is the first reliable execution target for the language's foundations.

GPU support is a separate engineering milestone. It requires compatible hardware, a supported toolchain, device-specific code, synchronization, and explicit handling of memory movement.

The architecture should make future accelerator support possible without pretending that it already exists.

### 5. Evidence over marketing

Crython will not claim to be the world's fastest programming language without reproducible evidence.

Performance claims must identify the workload, hardware, compiler settings, precision, baseline, and measurement methodology.

The objective is to discover where Crython performs well, where it does not, and why.

### 6. Incremental, testable development

Every release should have a clearly defined scope.

A working lexer, a reliable parser, a native executable, and a tested numerical kernel are more valuable than a large feature list with no verified implementation.

---

## 🧱 The Crython ecosystem

Crython is the language at the center of a broader proposed ecosystem.

The following names represent planned directions, not a claim that all packages are available today.

| Component | Intended responsibility |
|---|---|
| **Crython** | Language syntax, semantics, compiler, and developer experience |
| **`cryc`** | Compiler command-line interface |
| **`crypm`** | Future package and dependency manager |
| **`cryrt`** | Runtime support, resource management, and interoperability |
| **CryMath** | Numerical and mathematical primitives |
| **CryTensor** | Tensor abstractions and operations |
| **CryML** | Classical machine-learning utilities |
| **CryTorch** | Proposed deep-learning and tensor-computation layer |
| **CryNLP** | Natural-language-processing utilities |
| **CryCV** | Computer-vision utilities |
| **CryData** | Data structures and data-processing tools |
| **CryEval** | Evaluation and benchmarking utilities |
| **CryInfer** | Model inference interfaces and runtime integration |
| **CrySolve** | Numerical solvers and scientific-computing tools |
| **CryMesh** | Distributed-computing and MeshTrain integration experiments |
| **Cryda** | CPU/GPU compute and memory abstraction |

The initial release will focus on the language foundations. The wider ecosystem will be developed only as the underlying compiler, runtime, and APIs become reliable enough to support it.

---

## ⚡ Cryda: unified CPU and GPU computing

**Cryda is the proposed compute and memory layer associated with Crython.**

Its central idea is to provide a consistent way to describe computation across CPUs and GPUs while preserving the differences between those devices.

We use **CGPU** as a conceptual name for the unified compute interface. It does not mean that the CPU and GPU become one physical processor or that system RAM and GPU VRAM become one automatically interchangeable pool.

### The problem

Traditional accelerator programming often requires developers to manage several concerns separately:

- Choosing the execution device.
- Allocating memory in the appropriate location.
- Moving data between host and device.
- Launching kernels.
- Synchronizing asynchronous work.
- Handling resource lifetimes and failures.
- Measuring the difference between kernel time and end-to-end time.

Cryda explores how these operations could fit into a more coherent interface.

### The proposed memory model

A logical buffer could have a stable identity while its data resides in different physical locations.

Potential locations include:

- **HOST** — system memory.
- **DEVICE** — accelerator memory, such as NVIDIA VRAM.
- **PINNED** — host memory allocated with properties useful for transfers.
- **UNIFIED** — supported unified or managed-memory mechanisms.
- **AUTO** — a runtime-selected placement policy where the backend supports it.
- **EXPLICIT** — developer-controlled placement and transfers.

These policies are planned design concepts. Their availability and precise behavior will depend on the selected backend.

Cryda must track enough information to handle ownership, data validity, synchronization, and transfers correctly. It must not silently assume that a CPU write is immediately visible to a GPU or that asynchronous work has already finished.

### The proposed execution model

The initial development path is:

1. Establish a working CPU compute interface.
2. Implement buffers and predictable resource lifetimes.
3. Build a standalone NVIDIA CUDA example.
4. Add a GPU backend where the available hardware and toolchain permit it.
5. Measure kernel execution, data-transfer costs, and total execution time separately.
6. Explore device-selection policies only after correctness and baseline measurements are established.

### Why this matters

A unified abstraction is useful only if it makes programs easier to reason about without hiding important costs.

Cryda's goal is not to claim that CUDA is obsolete or that an abstraction automatically makes kernels faster. The goal is to investigate whether a carefully designed interface can simplify accelerator programming and improve end-to-end workflows.

---

## 🧪 Language design

Crython's syntax and semantics will evolve through working prototypes. The following example illustrates the intended direction; it is **illustrative pseudocode, not a guarantee of currently supported syntax**.

```cry
fn sum(values: Buffer<i64>) -> i64 {
    let mut total: i64 = 0

    for value in values {
        total = total + value
    }

    return total
}

fn main() -> i32 {
    let result = sum(data)
    print(result)
    return 0
}
```

The design direction emphasizes readable functions, explicit types where useful, clear mutability, and structured access to data.

The exact grammar, standard-library APIs, and compiler behavior will be documented as they become implemented and tested.

### Type system

The initial type-system experiments will prioritize a small, understandable set of types, potentially including:

- Signed integers such as `i64`.
- Floating-point values such as `f64`.
- Booleans.
- Functions and return types.
- Arrays or buffers as the implementation matures.

The first version does not need a sophisticated generic system, trait system, or advanced type inference to prove that the compiler architecture works.

### Memory and borrowing

Crython aims to explore compile-time ownership and borrowing rules rather than require a tracing garbage collector as its primary memory-management mechanism.

The first milestone is deliberately narrower than a complete ownership system: define a small set of rules, implement them, and test both accepted and rejected programs.

A future ownership system must specify aliasing, mutability, lifetimes, resource cleanup, and interoperability. These cannot be solved merely by adding ownership-related keywords to the syntax.

---

## 🏗️ Architecture

The compiler and runtime are expected to develop as separate but coordinated components.

```text
              Crython source (.cry)
                       |
                       v
                  Lexer / Tokens
                       |
                       v
                   Parser / AST
                       |
                       v
             Semantic and Type Checks
                       |
                       v
             Intermediate Representation
                       |
                       v
             Native Code Generation
                       |
                       v
                Native Executable
                       |
                       v
                  Crython Runtime
```

Cryda is a related compute layer, not simply another name for the compiler backend:

```text
              Crython program
                     |
                     v
              Cryda interface
                     |
              +------+------+
              |             |
              v             v
          CPU backend   GPU backend
              |             |
              v             v
          System RAM    Device VRAM
```

The diagrams describe the intended architecture. Actual implementation boundaries may change as prototypes reveal what works.

### Compiler responsibilities

- Lexing and parsing source files.
- Producing an abstract syntax tree.
- Reporting syntax and semantic errors.
- Checking supported types and language rules.
- Lowering supported programs to an intermediate form or a transitional source backend.
- Producing native executables through established toolchains.

### Runtime responsibilities

- Supporting the operations that cannot be compiled away.
- Managing resources that require runtime assistance.
- Providing a stable interface for external libraries.
- Defining errors and cleanup behavior.
- Supporting future numerical and accelerator components.

### Cryda responsibilities

- Representing compute devices and buffers.
- Defining backend capabilities.
- Managing allocation and transfer operations.
- Coordinating execution and synchronization.
- Exposing profiling information needed to understand performance.

---

## 🚀 Performance philosophy

Crython is being designed with performance as a major goal. Performance, however, is not a single number.

Different workloads stress different parts of a system:

| Workload | What we need to measure |
|---|---|
| Integer and floating-point loops | Runtime, throughput, generated code |
| Array operations | Allocation overhead, memory bandwidth, cache behavior |
| Parallel workloads | Scaling with cores and threads |
| Compilation | Build time, incremental-build behavior |
| CPU numerical kernels | Runtime, correctness, peak memory |
| GPU kernels | Kernel time, transfer time, synchronization overhead |
| AI inference | End-to-end latency, throughput, precision, memory use |
| Large workloads | Peak resident memory, allocation behavior, stability |

### Benchmarking rules

Crython benchmarks should aim to:

1. Compare equivalent algorithms and outputs.
2. Use appropriate optimization settings for each baseline.
3. Record CPU, GPU, driver, compiler, and toolchain versions.
4. Separate compilation time from execution time.
5. Separate GPU kernel time from data transfer and total latency.
6. Run repeated trials and report meaningful distributions.
7. Validate numerical correctness before comparing speed.
8. Publish benchmark programs and raw results where practical.

Relevant comparisons may include C, Rust, Python implementations, and established GPU libraries. Comparisons must account for whether a Python implementation uses optimized native libraries or whether the task is actually running on the GPU.

**No performance numbers will be presented as results until they have been measured.** Targets and hypotheses will be labeled as such.

---

## 🗓️ Roadmap to the initial release

**Target date: December 21, 2026**

The roadmap is intentionally staged. The initial release is a foundation, not the completion of the long-term vision.

### Phase 1 — Foundations

**Objective:** Establish the development environment and language specification.

- Define the first supported syntax.
- Choose the initial implementation language and backend.
- Create the repository structure.
- Establish build and test commands.
- Write a minimal language specification.
- Implement tokenization.

**Exit criteria:** Source code can be tokenized, invalid characters are reported, and lexer tests pass.

### Phase 2 — A working language frontend

**Objective:** Turn source code into a meaningful program representation.

- Implement parsing and an abstract syntax tree.
- Support arithmetic expressions.
- Add variables and lexical scope.
- Add functions and return values.
- Define the initial type rules.
- Build an error-reporting and regression-test suite.

**Exit criteria:** Supported programs parse consistently, while invalid syntax and unsupported constructs produce useful diagnostics.

### Phase 3 — Native execution

**Objective:** Execute a supported Crython program as a native executable.

- Implement the first code-generation path.
- Integrate a mature native compiler.
- Introduce `cryc` commands for checking and building.
- Test generated programs against known outputs.
- Document platform and toolchain requirements.

**Exit criteria:** A small supported Crython program can be compiled and executed outside the compiler's own process.

### Phase 4 — Memory and runtime foundations

**Objective:** Begin defining the resource model.

- Specify initial mutability rules.
- Implement a narrow, testable ownership or resource-lifetime rule.
- Add positive and negative semantic tests.
- Establish a minimal runtime interface.
- Document what the compiler does and does not guarantee.

**Exit criteria:** The supported memory rule is enforced by tests. This is not yet a claim of complete memory safety.

### Phase 5 — Cryda CPU/GPU experiment

**Objective:** Validate the compute abstraction with a small numerical workload.

- Define the initial device and buffer interfaces.
- Implement a CPU vector operation.
- Verify NVIDIA GPU and CUDA-toolchain availability.
- Build a standalone CUDA vector-add program.
- Integrate a GPU path if the environment and schedule permit.
- Validate outputs and synchronization.
- Measure transfer, kernel, and end-to-end time.

**Exit criteria:** The CPU path works reliably. GPU integration is included only if it passes correctness and build tests.

### Phase 6 — Verification and release preparation

**Objective:** Deliver a small, reproducible first release.

- Add regression tests.
- Add a simple numerical demonstration.
- Publish benchmark methodology and measured results, if available.
- Document build instructions and limitations.
- Record known issues.
- Tag the initial release if the acceptance criteria are met.

**Exit criteria:** A new contributor can follow the instructions, build the supported subset, run the examples, and reproduce the basic tests.

---

## 📦 What the first release aims to deliver

The planned initial release is a **small, working foundation**.

| Area | Initial release objective |
|---|---|
| Language frontend | Lexer, parser, AST |
| Language features | A limited set of expressions, variables, functions, and types |
| Compiler | A working native compilation path for supported programs |
| CLI | Basic check/build workflow |
| Error handling | Useful syntax and semantic diagnostics |
| Testing | Automated tests for implemented language features |
| Memory model | A documented, limited initial rule set |
| Cryda | A small CPU compute interface or prototype |
| NVIDIA GPU | A CUDA vector-add demonstration if the toolchain is available and integration succeeds |
| Documentation | Setup, architecture, examples, limitations, and roadmap |
| Benchmarks | Reproducible methodology; measured results only where available |

A feature will be called implemented only when there is working code and a corresponding test or demonstration. A design document alone is not an implementation.

---

## 🚧 What Crython is not yet

To keep the project's scope honest, the following distinctions matter.

- **Not yet a replacement for Rust or C.** Those languages have mature compilers, tooling, libraries, and production ecosystems.
- **Not yet a complete memory-safe language.** A limited prototype cannot guarantee safety across every operation or foreign-function boundary.
- **Not yet a CUDA replacement.** Cryda must demonstrate correctness, usable abstractions, and measurable value before broader claims are justified.
- **Not yet a complete AI framework.** The proposed CryMath, CryTensor, CryML, and related components are ecosystem directions, not promises that all will ship in the first release.
- **Not yet proven to be faster than existing languages.** That requires fair benchmarks across clearly defined workloads.
- **Not yet a universal cross-platform toolchain.** Supported operating systems, compiler versions, GPU configurations, and backend capabilities will be documented as they are verified.

These boundaries are intentional. The goal is to make progress that other engineers can inspect, reproduce, and build upon.

---

## 🧰 Development principles

Crython's implementation will follow a few practical rules:

- Prefer a working vertical slice over a large collection of unfinished subsystems.
- Reuse mature compiler and GPU infrastructure where appropriate.
- Keep the CPU path independently testable.
- Make resource lifetimes and synchronization explicit.
- Separate compiler, runtime, and accelerator responsibilities.
- Treat tests and benchmarks as part of the implementation.
- Document design decisions and revise them when evidence warrants it.
- Avoid declaring features complete before they have reproducible acceptance tests.

The project will prioritize engineering clarity over the appearance of completeness.

---

## 🤝 Getting involved

Crython is being developed as an independent project, with the intention of making its design decisions and progress understandable to other developers.

As the repository matures, useful contributions may include:

- Reviewing language design proposals.
- Discussing compiler architecture.
- Testing lexer, parser, and type-system behavior.
- Exploring native code generation.
- Investigating ownership and lifetime models.
- Testing numerical algorithms and benchmark methodology.
- Experimenting with CUDA and accelerator abstractions.
- Improving documentation and reproducible builds.

Early feedback is most valuable when it is specific: a reproducible bug, a proposed grammar change, a benchmark with a clear baseline, or a concrete architectural trade-off.

Contribution instructions and issue labels will be added as the repository becomes ready for external development.

---

## 📍 Project status

**Current stage:** Early design and prototype development.

**Primary focus:** Build the language foundations, prove a native execution path, and establish a small, testable compute abstraction.

**Initial public release target:** December 21, 2026.

The release date is a target, not a guarantee. If a core component needs more work to meet its acceptance criteria, the implementation and documentation will reflect that honestly.

The first milestone is not to support everything. It is to demonstrate that the foundations work.

---

## 🌌 The long-term direction

Crython begins with a compiler and a small language. Its broader ambition is to grow into a coherent ecosystem for native software, numerical computing, and AI systems.

That direction may eventually include richer type and ownership systems, mature package tooling, tensor operations, scientific solvers, model inference, and distributed computing. Each addition must build on stable foundations and justify its complexity.

We are interested in the difficult engineering questions: what should happen at compile time, what belongs in the runtime, what should remain explicit to the developer, and where abstractions can simplify programming without sacrificing correctness or performance.

The answers will come from implementation, testing, and measurement—not from a roadmap alone.

---

## 🔔 Stay tuned

**Crython — initial release target: December 21, 2026.**

A new language does not become real because of its vision. It becomes real when its first programs compile, its tests pass, and other people can reproduce what it does.

That is where we are starting.

We are building the foundations one milestone at a time.

**Follow the repository for development updates, design decisions, experiments, and the first public release.**

*Small beginnings. Native ambitions. Measured progress.*

