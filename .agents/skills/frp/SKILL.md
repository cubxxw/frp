```markdown
# frp Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill provides a comprehensive guide to contributing to the [frp](https://github.com/fatedier/frp) project, a fast reverse proxy written in Go. It covers the project's coding conventions, typical development workflows, and testing patterns. Whether you're fixing bugs, adding features, or preparing releases, this guide will help you follow established practices and streamline your contributions.

## Coding Conventions

### File Naming
- Use **snake_case** for file names.
  - Example: `config_loader.go`, `version_utils.go`

### Import Style
- Use **relative imports** within the module.
  - Example:
    ```go
    import (
        "github.com/fatedier/frp/pkg/util"
        "github.com/fatedier/frp/client"
    )
    ```

### Export Style
- Use **named exports** for functions, types, and variables that need to be accessed outside their package.
  - Example:
    ```go
    // Exported function
    func NewConfig() *Config {
        // ...
    }

    // Unexported (internal) function
    func parseConfig() error {
        // ...
    }
    ```

### Commit Messages
- Freeform, with no strict prefix required.
- Average commit message length: ~41 characters.

## Workflows

### Release Version Bump
**Trigger:** When preparing a new release or patch version.  
**Command:** `/release-bump`

1. Update the version in `pkg/util/version/version.go` (or `utils/version/version.go` in older structure).
2. Update `README.md` and `README_zh.md` with the new version if needed.
3. Update `Release.md` with release notes.
4. Update `go.mod` and `go.sum` for dependency changes.
5. Update `Makefile` or `Makefile.cross-compiles` if build processes change.
6. Update configuration files such as `conf/frpc_full.ini`, `conf/frps_full.ini`, etc.
7. Update or add test files in `test/e2e/`, `tests/ci/`, etc., as needed.
8. Touch main code files in `client/`, `server/`, `cmd/`, `pkg/`, etc., as needed.
9. Update web assets in `assets/frpc/static/`, `assets/frps/static/`, `web/frpc/`, `web/frps/` if applicable.

#### Example: Bumping Version
```go
// pkg/util/version/version.go
const (
    Version = "0.51.0" // <-- Update this value
)
```

---

### Config Structure Refactor
**Trigger:** When updating the configuration system or supporting new config formats.  
**Command:** `/config-refactor`

1. Move or rename config files (e.g., from `models/config/` to `pkg/config/`).
2. Update related code in `client/`, `server/`, `cmd/`, etc., to use the new config structure.
3. Add or update test files for config in `pkg/config/*_test.go`, `test/e2e/legacy/`, `test/e2e/v1/`.
4. Update documentation if needed.

#### Example: Refactoring Config Import
```go
// Before
import "github.com/fatedier/frp/models/config"

// After
import "github.com/fatedier/frp/pkg/config"
```

---

### Web Dashboard Assets Update
**Trigger:** When updating the frpc/frps web dashboard UI or static assets.  
**Command:** `/web-assets-update`

1. Update files in `web/frpc/` or `web/frps/` (Vue components, configs, `package.json`, `yarn.lock`, etc.).
2. Regenerate or update static assets in `assets/frpc/static/` and `assets/frps/static/`.
3. Update `statik.go` files to embed new assets.
4. Update `README.md` or documentation if needed.

#### Example: Embedding Static Assets
```sh
cd assets/frpc/statik
go run github.com/rakyll/statik -src=../static -dest=.
```

---

### CI/CD Workflow Update
**Trigger:** When changing build, test, or release automation.  
**Command:** `/ci-cd-update`

1. Edit or add files in `.github/workflows/` (e.g., `build-and-push-image.yml`, `goreleaser.yml`, `stale.yml`).
2. Edit `.circleci/config.yml` or `.travis.yml` if present.
3. Update `Makefile` or `package.sh` if needed.
4. Update `README.md` or `Release.md` if CI/CD changes affect usage.

#### Example: Adding a GitHub Actions Workflow
```yaml
# .github/workflows/build-and-push-image.yml
name: Build and Push Docker Image
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Build
        run: make docker-build
```

---

### Test Suite Expansion
**Trigger:** When adding new features or improving test coverage.  
**Command:** `/add-tests`

1. Add or update files in `test/e2e/`, `tests/ci/`, or `tests/mock/`.
2. Add or update `*_test.go` files in `pkg/config/`, `pkg/util/`, etc.
3. Update related code to support new tests if needed.

#### Example: Adding a Unit Test
```go
// pkg/config/config_test.go
import "testing"

func TestNewConfig(t *testing.T) {
    cfg := NewConfig()
    if cfg == nil {
        t.Fatal("expected config to be non-nil")
    }
}
```

## Testing Patterns

- Test files are named with the `*_test.go` pattern.
- Tests are written using Go's standard `testing` package.
- Test files are typically located alongside the code they test (e.g., `pkg/config/config_test.go`) or in dedicated test directories (`test/e2e/`, `tests/ci/`, `tests/mock/`).
- Example test structure:
    ```go
    // pkg/util/version_test.go
    import "testing"

    func TestVersionFormat(t *testing.T) {
        if Version == "" {
            t.Error("Version should not be empty")
        }
    }
    ```

## Commands

| Command           | Purpose                                                         |
|-------------------|-----------------------------------------------------------------|
| /release-bump     | Prepare and release a new version, updating all relevant files. |
| /config-refactor  | Refactor or migrate configuration files and related code.        |
| /web-assets-update| Update or add web dashboard frontend assets and static files.    |
| /ci-cd-update     | Update or add CI/CD workflow files.                             |
| /add-tests        | Add or expand test coverage for new or existing features.        |
```
