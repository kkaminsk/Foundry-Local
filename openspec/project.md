# Project Context

## Purpose
Foundry Local brings the power of Azure AI Foundry to local devices **without requiring an Azure subscription**. It enables:

- Running Generative AI models directly on local hardware with no sign-up required
- On-device data processing for enhanced privacy and security
- Integration with applications through an OpenAI-compatible API
- Optimized performance using ONNX Runtime and hardware acceleration (CUDA, NPU, CPU)

## Tech Stack

### Core SDKs (Multi-language monorepo)
- **C# SDK** (`sdk/cs/`): .NET 8/9, NuGet package `Microsoft.AI.Foundry.Local.WinML`
- **Python SDK** (`sdk/python/`): Python 3.9+, PyPI package `foundry-local-sdk`
- **JavaScript SDK** (`sdk/js/`): TypeScript, npm package `foundry-local-sdk`
- **Rust SDK** (`sdk/rust/`): Rust 2021 edition, crate `foundry-local`

### Website (`www/`)
- SvelteKit 2 with Svelte 5
- Tailwind CSS 4 with tailwind-variants
- Vite 7
- TypeScript 5
- Vercel deployment

### Build & Tooling
- GitHub Actions for CI/CD
- Package managers: winget (Windows), Homebrew (macOS)

## Project Conventions

### Code Style

**Python:**
- Ruff linter with 120 character line length
- Google docstring convention
- No relative imports (absolute imports only)
- Target version: Python 3.9

**JavaScript/TypeScript:**
- Prettier for formatting
- ESLint with TypeScript plugin
- Strict TypeScript mode with `strictNullChecks`
- ES2022 modules

**Rust:**
- `cargo fmt` for formatting (rustfmt)
- Rust 2021 edition

**C#:**
- Nullable reference types enabled
- Implicit usings enabled
- .NET 8/9 target frameworks

### Architecture Patterns
- **OpenAI-compatible API**: All SDKs integrate with standard OpenAI client libraries
- **Local-first**: No cloud dependencies for inference
- **Hardware abstraction**: Automatic selection of optimal model variants (CUDA, NPU, CPU)
- **Singleton pattern**: `FoundryLocalManager` manages service lifecycle
- **Async-first**: All SDK operations are async/await based

### Testing Strategy
- **JavaScript**: Vitest for unit tests, separate integration tests
- **Python**: Standard pytest (implied by pyproject.toml structure)
- **C#**: XUnit test projects (`FoundryLocal.Tests`)
- **Rust**: Cargo test with integration test feature flag

### Git Workflow
- Main branch: `main`
- Pull requests require CLA agreement (Microsoft CLA bot)
- Rust formatting checked in CI on PRs and pushes to main
- Follows Microsoft Open Source Code of Conduct

## Domain Context
- **Model aliases**: Users reference models by alias (e.g., `phi-3.5-mini`), and Foundry automatically selects the best variant for the user's hardware
- **Model variants**: Same model compiled for different hardware (CUDA, NPU, CPU)
- **Model catalog**: Registry of available models with metadata
- **Model caching**: Downloaded models are cached locally for reuse
- **ONNX Runtime**: Underlying inference engine for model execution

## Important Constraints
- Windows and macOS only (Apple Silicon for macOS)
- Microsoft Software License Terms (not fully open source)
- CLA required for contributions
- Microsoft trademark guidelines apply
- No Azure subscription required (key differentiator)

## External Dependencies
- **ONNX Runtime**: Model inference engine
- **OpenAI Python/JS SDKs**: Client library compatibility
- **Betalgo.Ranul.OpenAI**: C# OpenAI client library
- **Model Registry**: GitHub releases for installers, model catalog service
