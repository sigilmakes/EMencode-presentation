---
title: EMencode
info: |
  Data compression for cryoEM

theme: seriph

themeConfig:
  primary: "#2E2D62"
  secondary: "#1E5DF8"
  accent: "#00A788"
  background: "#FFFFFF"
  backgroundDark: "#2E2D62"
  text: "#1A1A1A"
  textLight: "#1A1A1A"

colorSchema: 'light'

class: text-center
layout: cover
hideInToc: true

download: true
---


<style>
:root {
  --slidev-theme-primary: #2E2D62;
  --slidev-theme-secondary: #1E5DF8;
  --slidev-theme-accent: #00A788;
}

.slidev-layout.cover  {
  background-color: #2E2D62;
  color: #FFFFFF;
}

h1 {
  color: #00A788; /* Using your Accent color for the Title */
}



</style>

# EMencode - March 2026

Data compression and archival workflows for cryoEM datasets


---
layout: center
---

<Toc minDepth="1" maxDepth="1" />

---

# EMencode Project


---

# Data Compression

---

# Prior benchmarking work


---

# EMencode


---

# High-level Package Overview

```mermaid

flowchart TD
  subgraph "Frontend Entrypoints"
    CLI["CLI Scripts<br/>emencode_compress, emencode_archive, ..."]
    GUI["GUI Application<br/>emencode_gui (PyQt6)"]
    MPI["MPI Runner<br/>python -m emencode.jobs.mpi_entry"]
    API["Python API<br/>from emencode.jobs import CompressJob"]
  end

  subgraph "Job Layer"
    Jobs["Job System<br/>Declarative options w/ standardised runtime"]
  end

  subgraph "Core Subsystems"
    Compressors["Compressors<br/>8 compressors + registry"]
    Archive["Archive<br/>HDF5 + format-aware entries"]
    Analysis["Analysis<br/>Metrics, FRC, plotting"]
    Convert["Format Conversion<br/>.tiff -> .mrc, Ome-Zarr"]
  end

CLI --> Jobs
GUI --> Jobs
MPI --> Jobs
API --> Jobs
Jobs --> Compressors
Jobs --> Archive
Jobs --> Analysis
Jobs --> Convert

```

---

# Interface (1)

All interfaces in EMencode are wrappers around jobs. All error handling, data validation, MPI ranking, and logging follows a consistent pattern. Hooking new functionality into the GUI/CLI/API just requires the job and some boilerplate. 

```mermaid
graph TD
    subgraph "Job Architecture"
        JobBase["Job base class<br/><i>w/ optional hooks for MPI</i>"]
        Options["Option types<br/><i></i>"]
        ResultCls["Result<br/><i>Job Outputs + Error Handling</i>"]
        ProgressCls["Progress callbacks<br/><i></i>"]
        MPIRunner["JobRunner<br/><i>Per-file MPI process allocator</i>"]
    end

    JobBase --> Options
    JobBase --> ResultCls
    JobBase --> ProgressCls
    MPIRunner --> JobBase
```

---

# Interface (2)



---

# HDF5 Archival


---

# Format Conversion

---

# Lossy Compression

---

# Feature Analysis

---

# Future Work

---
layout: center
hideInToc: True
---

# **Any questions?**

Links:
- EMencode Repository: https://gitlab.com/ccpem/data-compression-framework
- Toy version in rust: https://gitlab.com/willow-sparks/emencode-rs


