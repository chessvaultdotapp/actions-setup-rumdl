# Setup rumdl

Install official [rumdl](https://github.com/rvben/rumdl) release binaries and add
`rumdl` to `PATH` for subsequent GitHub Actions steps. No Rust toolchain is needed.

## Usage

After publishing this action, replace `FULL_COMMIT_SHA` with its full commit SHA:

```yaml
steps:
  - uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2
  - uses: chessvaultdotapp/actions-setup-rumdl@FULL_COMMIT_SHA
    with:
      version: '0.2.75'
  - run: rumdl check
```

### Inputs

| Input | Description | Default |
| --- | --- | --- |
| `version` | Exact stable release version, without the `v` prefix | `0.2.75` |

`latest`, version ranges, and prerelease versions are not supported.

### Supported platforms

- Linux: x64 and ARM64 (musl binaries)
- macOS: x64 and ARM64
- Windows: x64

The action requires Bash, curl, and tar (or unzip on Windows). Standard GitHub-hosted
runners include these tools. Downloads come directly from rumdl's public GitHub
releases; no token is required. Downloaded binaries are not checksum-verified.

## Maintenance

The installer and default version live in this repository. To update rumdl, change
`inputs.version.default` in `action.yml`, the explicit-version test in
`.github/workflows/test.yml`, and the examples and default documented here.

CI exercises all five supported platform combinations. After the checks pass,
publish the commit and update consuming repositories to its full SHA. Keep
repository-specific lint commands, configuration, and path filters in consumers.

## Local checks

```sh
bash -n install.sh
shellcheck install.sh
rumdl check README.md
```

## License

See [LICENSE](LICENSE).
