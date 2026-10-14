# LLM

![license](https://img.shields.io/badge/license-license-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![category](https://img.shields.io/badge/category-chip_quantization-lightgrey)

> Anticloud-hardened packaging of the upstream project `LLM` in category **CHIP QUANTIZATION**. Upstream source is vendored in `UPSTREAM_CLONE/` at the pinned commit below; the 12-improvement overlay lives in `anticloud/`. Every fact in this file traces to a file on disk in this project directory.

**Category:** CHIP QUANTIZATION · **Upstream:** https://github.com/simonw/llm · **Upstream pin:** `05d7ae7dedc524b024ab463b063854e7c43fee01` · **Vendor:** Anticloud FZ LLE

---

## What This Project Does

<!-- [[[cog
# README.md is generated from docs/index.md using sphinx_markdown_builder
import tempfile
import subprocess
from pathlib import Path

readme_markdown = ''

with tempfile.TemporaryDirectory() as tmpdir:
    tmp_path = Path(tmpdir)
    # Run: sphinx-build -M markdown ./docs ./tmpdir
    subprocess.run([
        "sphinx-build",
        "-M", "markdown",
        "./docs",
        str(tmp_path)
    ], check=True)
    index_file = tmp_path / "markdown" / "index.md"
    readme_markdown = index_file.read_text(encoding="utf-8")

cog.out(readme_markdown)
]]] -->
# LLM

[![GitHub project](https://img.shields.io/badge/github-project-green)](https://github.com/simonw/llm)
[![PyPI](https://img.shields.io/pypi/v/llm.svg)](https://pypi.org/project/llm/)
[![Changelog](https://img.shields.io/github/v/release/simonw/llm?include_prereleases&label=changelog)](https://llm.datasette.io/en/stable/changelog.html)
[![Tests](https://github.com/simonw/llm/workflows/Test/badge.svg)](https://github.com/simonw/llm/actions?query=workflow%3ATest)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://github.com/simonw/llm/blob/main/LICENSE)
[![Discord](https://img.shields.io/discord/823971286308356157?label=discord)](https://datasette.io/discord-llm)
[![Homebrew](https://img.shields.io/homebrew/installs/dy/llm?color=yellow&label=homebrew&logo=homebrew)](https://formulae.brew.sh/formula/llm)

A CLI tool and Python library for interacting with **OpenAI**, **Anthropic’s Claude**, **Google’s Gemini**, **Qwen**, **Gemma**, **Kimi**, **DeepSeek**, **Mistral**, and dozens of other Large Language Models, both via remote APIs and with models that can be installed and run on your own machine.

Watch **[Language models on the command-line](https://www.youtube.com/watch?v=QUXQNi6jQ30)** on YouTube for a demo or [read the accompanying detailed notes](https://simonwillison.net/2024/Jun/17/cli-language-models/).

With LLM you can:

- [Run prompts from the command-line](https://llm.datasette.io/en/stable/usage.html#usage-executing-prompts)
- [Store prompts and responses in SQLite](https://llm.datasette.io/en/stable/logging.html#logging)
- [Generate and store embeddings](https://llm.datasette.io/en/stable/embeddings/index.html#embeddings)
- [Extract structured content from text and images](https://llm.datasette.io/en/stable/schemas.html#schemas)
- [Grant models the ability to execute tools](https://llm.datasette.io/en/stable/tools.html#tools)
- … and much, much more

## Quick start

First, install LLM using `pip` or Homebrew or `pipx` or `uv`:

```bash
pip install llm
```

Or with Homebrew (see [warning note](https://llm.datasette.io/en/stable/setup.html#homebrew-warning)):

```bash
brew install llm
```

Or with [pipx](https://pipx.pypa.io/):

```bash
pipx install llm
```

Or with [uv](https://docs.astral.sh/uv/guides/tools/)

```bash
uv tool install llm
```

Use LLM to run prompts or start chats against an arbitrary OpenAI-compatible Chat Completions endpoint, such as [LM Studio](https://lmstudio.ai). With `uvx`, you can do this without installing LLM first:

```bash
uvx llm openai endpoint http://localhost:1234/v1 \
  -m google/gemma-4-12b \
  "What is the capital of France?"

uvx llm openai endpoint http://localhost:1234/v1 \
  -m google/gemma-4-12b \
  --chat
```

Add `--key your-api-key` if the endpoint requires authentication. See [Run against an endpoint without configuring it](https://llm.datasette.io/en/stable/other-models.html#openai-endpoint) for more options.

If you have an [OpenAI API key](https://platform.openai.com/api-keys) key you can run this:

```bash
# Paste your OpenAI API key into this
llm keys set openai

# Run a prompt (with the default gpt-5.6-luna model)
llm "Ten fun names for a pet pelican"

# Extract text from an image
llm "extract text" -a scanned-document.jpg

# Use a system prompt against a file
cat myfile.py | llm -s "Explain this code"
```

Run prompts against [Gemini](https://aistudio.google.com/apikey) or [Anthropic](https://console.anthropic.com/) with their respective plugins:

```bash
llm install llm-gemini
llm keys set gemini
# Paste Gemini API key here
llm -m gemini-3.5-flash 'Tell me fun facts about Mountain View'

llm install llm-anthropic
llm keys set anthropic
# Paste Anthropic API key here
llm -m claude-sonnet-5 'Impress me with wild facts about turnips'
```

You can also [install a plugin](https://llm.datasette.io/en/stable/plugins/installing-plugins.html#installing-plugins) to access models that can run on your local device. If you use [Ollama](https://ollama.com/):

```bash
# Install the plugin
llm install llm-ollama

# Download and run a prompt against the Orca Mini 7B model
ollama pull llama3.2:latest
llm -m llama3.2:latest 'What is the capital of France?'
```

To start [an interactive chat](https://llm.datasette.io/en/stable/usage.html#usage-chat) with a model, use `llm chat`:

```bash
llm chat -m gpt-4.1
```

```default
Chatting with gpt-4.1
Type 'exit' or 'quit' to exit
Type '!multi' to enter multiple lines, then '!end' to finish
Type '!edit' to open your default editor and modify the prompt.
Type '!fragment <my_fragment> [<another_fragment> ...]' to insert one or more fragments
> Tell me a joke about a pelican
Why don't pelicans like to tip waiters?

Because they always have a big bill!
```

## Project news

- 29th April 2026: [LLM 0.32a0 is a major backwards-compatible refactor](https://simonwillison.net/2026/Apr/29/llm/)
- 11th August 2025: [LLM 0.27, the annotated release notes: GPT-5 and improved tool calling](https://simonwillison.net/2025/Aug/11/llm-027/)
- 27th May 2025: [Large Language Models can run tools in your terminal with LLM 0.26](https://simonwillison.net/2025/May/27/llm-tools/)
- 5th May 2025: [Feed a video to a vision LLM as a sequence of JPEG frames on the CLI (also LLM 0.25)](https://simonwillison.net/2025/May/5/llm-video-frames/)
- 7th April 2025: [Long context support in LLM 0.24 using fragments and template plugins](https://simo

*(excerpt; full text in `UPSTREAM_CLONE/`)*

*Quoted from the upstream `README.md` file in `UPSTREAM_CLONE/`.*
Project-specific facts detected in this directory:

- Ecosystem: **Python** (manifests: pyproject.toml; scanned in UPSTREAM_CLONE)
- Top-level source layout: `llm/`, `tests/`
- Snapshot size: **112 files**, **37045 lines of code** (measured; see Benchmarks)
- Primary languages: `.py` (54), `.md` (30), `.yaml` (13), `(none)` (5), `.toml` (3), `.ini` (2)
- Upstream commit pinned for this packaging: `05d7ae7dedc524b024ab463b063854e7c43fee01`

---

## Installation

import tempfile
import subprocess
from pathlib import Path

readme_markdown = ''

with tempfile.TemporaryDirectory() as tmpdir:
    tmp_path = Path(tmpdir)
    # Run: sphinx-build -M markdown ./docs ./tmpdir
    subprocess.run([
        "sphinx-build",
        "-M", "markdown",
        "./docs",
        str(tmp_path)
    ], check=True)
    index_file = tmp_path / "markdown" / "index.md"
    readme_markdown = index_file.read_text(encoding="utf-8")

cog.out(readme_markdown)
]]] -->

*Section quoted from the upstream readme.*
Overlay install (this project):

```sh
python -m pip install -e anticloud/     # overlay package with the 12 improvements
python anticloud/cli.py --help          # 13 subcommands, JSON stdout
```

---

## Usage

- [Store prompts and responses in SQLite](https://llm.datasette.io/en/stable/logging.html#logging)
- [Generate and store embeddings](https://llm.datasette.io/en/stable/embeddings/index.html#embeddings)
- [Extract structured content from text and images](https://llm.datasette.io/en/stable/schemas.html#schemas)
- [Grant models the ability to execute tools](https://llm.datasette.io/en/stable/tools.html#tools)
- … and much, much more

*Section quoted from the upstream readme.*
Anticloud overlay CLI (available in every project):

```sh
python anticloud/cli.py --help     # 13 subcommands, JSON stdout
python anticloud/cli.py checks     # run the 16-check suite
```

---

## API

Watch **[Language models on the command-line](https://www.youtube.com/watch?v=QUXQNi6jQ30)** on YouTube for a demo or [read the accompanying detailed notes](https://simonwillison.net/2024/Jun/17/cli-language-models/).

With LLM you can:

- [Run prompts from the command-line](https://llm.datasette.io/en/stable/usage.html#usage-executing-prompts)
- [Store prompts and responses in SQLite](https://llm.datasette.io/en/stable/logging.html#logging)
- [Generate and store embeddings](https://llm.datasette.io/en/stable/embeddings/index.html#embeddings)
- [Extract structured content from text and images](https://llm.datasette.io/en/stable/schemas.html#schemas)
- [Grant models the ability to execute tools](https://llm.datasette.io/en/stable/tools.html#tools)
- … and much, much more

*Section quoted from the upstream readme.*
---

## Dependencies

| Metric | Value |
|--------|-------|
| Ecosystem | Python |
| Manifests detected | pyproject.toml |
| Files in snapshot | 112 |
| Lines of code | 37045 |
| Dependency references | 14 |
| Dependencies by ecosystem | pypi: 14 |
| Upstream license | Apache-2.0 |
| Overlay license | Anticommons 0.1.0 |

Top dependency references recorded in the benchmark snapshot:

| Ecosystem | Name | Version | Source file |
|-----------|------|---------|-------------|
| pypi | click | - | pyproject.toml |
| pypi | httpx2 | - | pyproject.toml |
| pypi | condense-json | >=1.1 | pyproject.toml |
| pypi | openai | >3 | pyproject.toml |
| pypi | click-default-group | >=1.2.3 | pyproject.toml |
| pypi | sqlite-utils | >=4.0 | pyproject.toml |
| pypi | pydantic | >=2.0.0 | pyproject.toml |
| pypi | typing-extensions | - | pyproject.toml |
| pypi | PyYAML | - | pyproject.toml |
| pypi | pluggy | - | pyproject.toml |
| pypi | python-ulid | - | pyproject.toml |
| pypi | setuptools | - | pyproject.toml |
| pypi | pip | - | pyproject.toml |
| pypi | pyreadline3 | - | pyproject.toml |

Pinned lockfile: `anticloud/requirements.lock` (hash-pinned, PEP 508). SBOM: `sbom.cdx.json` (CycloneDX 1.5, pinned to the upstream SHA).

---

## Configuration

If you have an [OpenAI API key](https://platform.openai.com/api-keys) key you can run this:

```bash
# Paste your OpenAI API key into this
llm keys set openai

# Run a prompt (with the default gpt-5.6-luna model)
llm "Ten fun names for a pet pelican"

*Section quoted from the upstream readme.*
Overlay configuration (Anticloud):

- `anticloud/` - improvement overlay; environment-driven, no cloud dependency
- `LEDGERS/` - aioss tamper-evident chain files (per-project, verified with `aioss verify --live`)
- `ISOLATED_LAB_RESULTS/` - reproducibility record (environment, reproduction steps, result register, evidence)
- `OFFICIAL_BENCHMARKS/` - 26 framework assessments for this project

---

## Contributing

Upstream contributions: fork the `LLM` project, create a feature branch, and open a pull request against upstream. Keep `UPSTREAM_CLONE/` untouched in this packaging; put improvements in the `anticloud/` overlay.

Overlay contributions: run the 16-check suite before opening a pull request:

```sh
python anticloud/bench/runner.py --cwd anticloud
```

---

## License

**Upstream license: Apache-2.0** (evidence: `LICENSE` in the upstream snapshot).

License file excerpt:

```text
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
```

### Anticommons 0.1.0 overlay

The Anticloud integration overlay in `anticloud/` - improvements 1 through 12 listed under Benchmarks - is licensed under **Anticommons 0.1.0**. Upstream code remains under its original Apache-2.0 terms. See `ANTICOMMONS_LICENSE.md` in this directory for the overlay terms and contact.

SPDX: `Apache-2.0` (upstream) + Anticommons 0.1.0 (overlay, dual).

---

## Upstream

- **Project:** `LLM` (category: CHIP QUANTIZATION)
- **Upstream URL:** https://github.com/simonw/llm
- **Pinned commit (SHA):** `05d7ae7dedc524b024ab463b063854e7c43fee01`
- **Branch:** main
- **Pin provenance:** GitHub API commits/main. The parent-project stamp is explicitly rejected for this project.
- **Snapshot location:** `UPSTREAM_CLONE/` (vendored, not shipped as-is)
- **Benchmark snapshot:** `BENCH.json`

---

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`46197963e6cf6cef2b69be9ce735abd869ecee9516b89aa018533668e0590fcc`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe and Mail, Business Insider, National Post, Financial Post, StreetInsider, Digital Journal, Barchart, International Business Times, and fox47 · National Law Review.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

