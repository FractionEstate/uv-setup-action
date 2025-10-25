# setup-uv (composite action)

Reusable composite GitHub Action to install [Astral's uv](https://docs.astral.sh/uv/) on GitHub-hosted runners.

## Usage

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install uv
        uses: FractionEstate/uv-setup-action@main
        with:
          # Optional: install a specific version, e.g. 0.9.5 (defaults to latest)
          # version: 0.9.5
          # Optional: add install dir to PATH (default true)
          # add-to-path: 'true'
      - name: Verify
        run: |
          which uv
          uv --version
```

### Inputs
- `version` (optional): Specific uv version (e.g., `0.9.5`). Default installs latest.
- `add-to-path` (optional): Add the detected install directory to `PATH`. Defaults to `true`.

### Outputs
- `version`: The installed uv version string.

## How it works

This action wraps the official installer script from `astral.sh` and then ensures the common install locations
(`~/.local/bin`, `~/.cargo/bin`) are added to PATH when requested. It works on Ubuntu/macOS runners.

If you prefer pinning, reference a tagged release instead of `@main` when available (e.g., `@v1`).
