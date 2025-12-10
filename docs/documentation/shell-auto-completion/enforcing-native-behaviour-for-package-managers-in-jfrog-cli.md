---
title: '  # Enforcing Native Behaviour for Package Managers in JFrog CLI'
excerpt: >-
  JFrog CLI provides two modes of operation when running package managers:
  **Wrapped Mode** and **Native Mode**. This section explains the difference and
  how to enforce fully native package-manager behaviour when needed.
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

## Execution Modes

### Wrapped Mode (Default)

In Wrapped Mode, JFrog CLI intercepts certain package-manager commands to provide Artifactory-aware features, such as:

* Automatic repository resolution
* Injection of registry/source configuration into project files
* Enhanced dependency resolution
* Automatic build-info collection (when flags like `--build-name` / `--build-number` are supplied)
* Consistent authentication and resolution via JFrog CLI config

Wrapped Mode is the recommended flow for most Artifactory-integrated development.

### Native Mode (Opt-in)

Native Mode disables all JFrog CLI wrapping and allows the package manager to run exactly as its upstream client would.

**Enable Native Mode with:**

```bash
export JFROG_RUN_NATIVE=true
```

When Native Mode is enabled:

* No Artifactory configuration or repositories are injected into project files
* No CLI YAML (`.jfrog/projects/*.yml`) is applied
* No wrapped behaviour is executed (e.g., no poetry update, no metadata alterations)
* The package manager uses its own configuration, as set through the package manager's native commands or Artifactory's Set Me Up instructions
* Lock files and metadata remain untouched
* Build-info is not collected by wrapped commands
* Execution is fully deterministic and aligned with the original client tooling

## Environment Variable

### JFROG_RUN_NATIVE

**Purpose:** Enables Native Mode and bypasses Wrapped Mode entirely for supported package managers.

**Default:** `false`

**Usage:**

```bash
export JFROG_RUN_NATIVE=true
```

**Supported Package Managers:**

* Maven
* Poetry
* Gradle

**Note:** For package managers that run natively by default (Conan), this environment variable is not required and has no effect. Helm uses run-native mode (always enabled) but provides full JFrog CLI integration.

**When to Use:**

* When you need strict lockfile fidelity
* When you want zero modification to project metadata (pom.xml, pyproject.toml, lock files, etc.)
* When you need full compatibility with the upstream package manager's behaviour
* When builds must be fully deterministic across environments
* When you have custom or advanced workflows configured directly in the package manager

**Limitations:**

* Build-info collection via wrapped commands is not supported in Native Mode (except for Gradle and Maven, which use FlexPack for build-info collection)
* CLI YAML configuration (`.jfrog/projects/*.yml`) is ignored
* Package manager config commands (e.g., `jf mvn-config`, `jf poetry-config`, `jf gradle-config`) are ignored
* Repository injection does not occur

## Supported Package Managers

Native Mode is currently supported for the following package ecosystems:

* **Maven** (requires `JFROG_RUN_NATIVE=true`)
* **Poetry** (requires `JFROG_RUN_NATIVE=true`)
* **Gradle** (requires `JFROG_RUN_NATIVE=true`)
* **Helm** (run-native mode, always enabled - full JFrog CLI integration)
* **Conan** (native by default)
* **Docker** (requires manual setup)

## When to Use Which Mode

**Use Wrapped Mode when you want:**

* Integrated Artifactory resolution
* Automatic build-info capture
* Managed repository configuration via JFrog CLI
* Consistent, unified behaviour across machines and CI

**Use Native Mode when you need:**

* Strict lockfile fidelity
* Zero modification to project metadata (pom.xml, pyproject.toml, lock files, etc.)
* Full compatibility with the upstream package manager's behaviour
* Builds that must be fully deterministic across environments
* Custom or advanced workflows configured directly in the package manager

## How Native Mode Interacts With Configuration

| Area                                                                                       | Wrapped Mode | Native Mode                                                     |
| ------------------------------------------------------------------------------------------ | ------------ | --------------------------------------------------------------- |
| CLI YAML (`.jfrog/projects/*.yml`)                                                         | Applied      | Ignored                                                         |
| CLI package-manager config (e.g., `jf poetry-config`, `jf mvn-config`, `jf gradle-config`) | Applied      | Ignored                                                         |
| Build-info capture                                                                         | Supported    | Supported via FlexPack (Gradle, Maven) / Not supported (Poetry) |
| Repository injection                                                                       | Happens      | Never                                                           |
| Lockfile changes                                                                           | Possible     | Never                                                           |
| Requires Artifactory Set Me Up                                                             | Optional     | Required                                                        |

***

## Helm

**[NEW]** JFrog CLI now provides integrated support for Helm and Helm OCI, enabling seamless interaction with JFrog Artifactory for Helm chart storage, resolution, and management. This includes streamlined configuration, authentication via JFrog CLI config, optimized performance for large artifacts, and automatic build-info collection.

Helm commands in JFrog CLI use the native Helm client (run-native mode, always enabled) but provide enhanced Artifactory integration, build-info capture, and improved performance compared to using Helm CLI directly.

### How Helm Works with JFrog CLI

When you run `jf helm` commands, JFrog CLI:

* Uses the native Helm client for chart operations (run-native mode, always enabled)
* Provides Artifactory-aware commands for repository management and chart operations
* Automatically handles authentication using JFrog CLI configuration (`jf config`)
* Collects build-info automatically when `--build-name` and `--build-number` are provided
* Supports both classic Helm repositories and Helm OCI registries
* Optimizes transfers for large chart artifacts

### Prerequisites

1. **Helm client installed:** Ensure Helm is installed and available in your PATH
   ```bash
   helm version
   ```

2. **Artifactory server configured:** Configure your Artifactory server using JFrog CLI:
   ```bash
   jf config add my-artifactory-server --url https://myartifactory.example.com --user <user> --password <pass>
   ```

### Configuration and Authentication

#### Configuring Classic Helm Repositories

Use `jf helm repo-add` to configure Artifactory as a classic Helm repository:

```bash
jf helm repo-add my-helm-local helm-local --server-id my-artifactory-server
```

This command configures the Helm repository and handles authentication automatically using your JFrog CLI configuration.

#### Configuring Helm OCI Registries

For OCI-based Helm repositories, JFrog CLI uses the configured Artifactory server details for authentication. No separate registry login is required when using `jf config`.

Example OCI URI format:

```
oci://myartifactory.example.com/artifactory/helm-oci-local/
```

### Core Helm Commands

#### Push Charts to Artifactory

Push Helm charts to Artifactory (classic or OCI):

**Classic Repository:**

```bash
# Push a packaged chart
jf helm push myapp-1.2.3.tgz my-helm-repo-key --build-name=MyHelmAppBuild --build-number=1.0.0

# Package and push a chart directory
jf helm push ./my-chart-source my-helm-repo-key --build-name=MyHelmAppBuild --build-number=1.0.0
```

**OCI Registry:**

```bash
# Push to OCI registry
jf helm push myapp-1.2.3.tgz oci://myartifactory.example.com/artifactory/my-helm-oci-repo/ --server-id my-artifactory-server --build-name=MyHelmAppBuild --build-number=1.0.0

# Package and push directory to OCI
jf helm push ./my-chart-source oci://myartifactory.example.com/artifactory/my-helm-oci-repo/ --server-id my-artifactory-server
```

#### Pull Charts from Artifactory

Download Helm charts from Artifactory:

**Classic Repository:**

```bash
jf helm pull myapp --version 1.2.3 --repo my-helm-repo-key
```

**OCI Registry:**

```bash
jf helm pull oci://myartifactory.example.com/artifactory/my-helm-oci-repo/myapp --version 0.1.0 --server-id my-artifactory-server
```

#### Install Charts from Artifactory

Install Helm charts directly from Artifactory:

**Classic Repository:**

```bash
jf helm install my-production-app myapp --version 1.2.3 --repo my-helm-repo-key --build-name=MyK8sDeployment --build-number=5 --module=MyHelmModule
```

**OCI Registry:**

```bash
jf helm install my-staging-app oci://myartifactory.example.com/artifactory/my-helm-oci-repo/myapp --version 0.1.0 --server-id my-artifactory-server --build-name=MyK8sDeployment --build-number=5
```

#### Search Charts

Search for Helm charts in Artifactory repositories:

```bash
jf helm search nginx --repo my-helm-repo-key
```

### Build-Info Integration

Build-info is automatically collected when you provide `--build-name` and `--build-number` flags:

* **`jf helm push`** commands automatically collect and associate build-info with published charts
* **`jf helm install`** and **`jf helm pull`** record resolved chart artifacts as build dependencies

After running Helm commands with build-info flags, publish the build-info:

```bash
jf rt build-publish MyHelmAppBuild 1.0.0
```

### Important Notes

* **JFrog CLI Configuration Required:** Helm commands use `jf config` for authentication. Configure your Artifactory server using `jf config add` before using Helm commands.
* **Authentication:** Authentication is handled automatically via JFrog CLI configuration. No need to use Helm's native authentication mechanisms (`helm repo add` with credentials).
* **Build-Info:** Build-info is automatically collected when `--build-name` and `--build-number` are provided. This is an exclusive advantage of using JFrog CLI.
* **Performance:** JFrog CLI optimizes transfers for large chart artifacts, providing improved performance compared to native Helm CLI.
* **Run-Native Mode:** Helm always uses the native Helm client (run-native mode, always enabled). This is different from the opt-in "Native Mode" (`JFROG_RUN_NATIVE=true`) used by other package managers.

### Example: Complete Workflow

**Classic Helm Repository:**

```bash
# 1. Configure Artifactory server (one-time setup)
jf config add my-artifactory-server --url https://my-artifactory.jfrog.io --user myuser --password mypassword

# 2. Add Helm repository
jf helm repo-add my-helm-local helm-local --server-id my-artifactory-server

# 3. Search for charts
jf helm search nginx --repo my-helm-local

# 4. Push a chart with build-info
jf helm push myapp-1.2.3.tgz my-helm-local --build-name=MyHelmAppBuild --build-number=1.0.0

# 5. Install a chart
jf helm install my-app myapp --repo my-helm-local --version 1.2.3 --build-name=MyK8sDeployment --build-number=5

# 6. Publish build-info
jf rt build-publish MyHelmAppBuild 1.0.0
jf rt build-publish MyK8sDeployment 5
```

**Helm OCI Registry:**

```bash
# 1. Configure Artifactory server (one-time setup)
jf config add my-artifactory-server --url https://my-artifactory.jfrog.io --user myuser --password mypassword

# 2. Push chart to OCI registry
jf helm push myapp-1.2.3.tgz oci://my-artifactory.jfrog.io/artifactory/helm-oci-local/ --server-id my-artifactory-server --build-name=MyHelmAppBuild --build-number=1.0.0

# 3. Pull chart from OCI registry
jf helm pull oci://my-artifactory.jfrog.io/artifactory/helm-oci-local/myapp --version 1.2.3 --server-id my-artifactory-server

# 4. Install chart from OCI registry
jf helm install my-app oci://my-artifactory.jfrog.io/artifactory/helm-oci-local/myapp --version 1.2.3 --server-id my-artifactory-server --build-name=MyK8sDeployment --build-number=5

# 5. Publish build-info
jf rt build-publish MyHelmAppBuild 1.0.0
jf rt build-publish MyK8sDeployment 5
```

### CI/CD Integration

**GitHub Actions Example:**

```yaml
- name: Configure JFrog CLI
  uses: jfrog/setup-jfrog-cli@v3
  with:
    version: latest

- name: Push Helm Chart
  run: |
    jf helm push myapp-1.2.3.tgz my-helm-local \
      --build-name=${{ github.event.repository.name }} \
      --build-number=${{ github.run_number }} \
      --server-id=my-artifactory-server

- name: Publish Build-Info
  run: |
    jf rt build-publish ${{ github.event.repository.name }} ${{ github.run_number }}
```

***

## Conan

Conan runs in Native Mode by default. JFrog CLI acts as a pass-through to the Conan client, executing Conan commands directly without any wrapping or configuration injection.

### How Conan Works with JFrog CLI

When you run `jf conan` commands, JFrog CLI:

* Executes the Conan client directly
* Passes all arguments through unchanged
* Does not inject any Artifactory configuration
* Does not modify Conan profiles or configuration files
* Does not collect build-info automatically

### Prerequisites

1. **Conan client installed:** Ensure Conan is installed and available in your PATH
   ```bash
   conan --version
   ```

2. **Artifactory configured:** Configure Conan to use Artifactory repositories using Conan's native configuration:
   * Add Artifactory remote repositories to Conan
   * Configure authentication via Conan profiles
   * Use Artifactory's Set Me Up instructions for Conan

### Using Conan with Artifactory

**Step 1: Configure Conan Remote**

From Artifactory, navigate to your Conan repository and use the "Set Me Up" instructions, or manually configure the remote:

```bash
conan remote add my-conan-repo https://your-artifactory-instance.jfrog.io/artifactory/api/conan/conan-virtual
```

**Step 2: Configure Authentication**

Create or edit your Conan profile to include Artifactory credentials:

```bash
# Edit ~/.conan/profiles/default or create a new profile
conan user -p your-password -r my-conan-repo your-username
```

Alternatively, configure authentication in your Conan profile:

```ini
[remotes]
my-conan-repo=https://your-artifactory-instance.jfrog.io/artifactory/api/conan/conan-virtual

[remote "my-conan-repo"]
user=your-username
password=your-password
```

**Step 3: Use Conan Commands via JFrog CLI**

```bash
# Install dependencies
jf conan install . --build=missing

# Create a package
jf conan create . --name=hello --version=1.0

# Upload to Artifactory
jf conan upload hello/1.0@myuser/channel -r my-conan-repo --all

# Search packages
jf conan search "*" -r my-conan-repo
```

### Important Notes

* **No Configuration Required:** Unlike other package managers, Conan does not require `jf conan-config` or any JFrog CLI-specific configuration
* **Native Authentication:** Authentication is handled by Conan's native mechanisms (profiles, user credentials)
* **Build-Info:** Build-info is not automatically collected. If you need build-info, use JFrog CLI's build-info commands separately
* **Profile Management:** All configuration is done through Conan's native commands and profile files

### Promoting Conan Packages

**⚠️ Important Limitation:** The `jf build-promote` command may not fully support Conan package promotions. When promoting builds containing Conan packages, the `conanmanifest.txt` file (which is essential for Conan package integrity) may be left in the original repository, resulting in corrupted packages that cannot be downloaded.

**Conan Package Structure:** Conan packages consist of multiple files including:

* Package recipe files
* Binary package files
* `conanmanifest.txt` - Manifest file listing all package files (required for package integrity)
* `conaninfo.txt` - Package metadata

**Recommended Alternatives for Promoting Conan Packages:**

1. **Use Conan's Native Promotion Command (Recommended):**
   ```bash
   # Promote using Conan's built-in Artifactory promotion
   conan art:promote <package-reference> <source-repo> <target-repo> --server-id <server-id>
   ```

2. **Use JFrog CLI Copy/Move Commands:**
   ```bash
   # Copy all Conan package files including manifest
   jf rt copy "conan-repo-source/*" conan-repo-target/ --flat=false

   # Or move (if you want to remove from source)
   jf rt move "conan-repo-source/*" conan-repo-target/ --flat=false
   ```

3. **Ensure Complete Build-Info Collection:**
   If you must use `jf build-promote`, ensure all Conan package files (including `conanmanifest.txt`) are properly included in the build-info before publishing:
   ```bash
   # Collect build-info manually to ensure all files are tracked
   jf rt build-add-dependencies <build-name> <build-number>
   jf rt build-publish <build-name> <build-number>
   ```

**Related Issue:** This limitation is tracked in [GitHub Issue #2834](https://github.com/jfrog/jfrog-cli/issues/2834).

### Example: Complete Workflow

```bash
# 1. Configure Conan remote (one-time setup)
conan remote add artifactory https://my-artifactory.jfrog.io/artifactory/api/conan/conan-virtual

# 2. Configure authentication
conan user -p mypassword -r artifactory myuser

# 3. Use Conan via JFrog CLI (all commands work as native Conan)
jf conan install . --build=missing
jf conan create . --name=mylib --version=1.0.0
jf conan upload mylib/1.0.0@myuser/stable -r artifactory --all
```

***

## Gradle

Gradle supports Native Mode when the `JFROG_RUN_NATIVE=true` environment variable is set. In Native Mode, Gradle runs without JFrog CLI configuration files and uses Gradle's native configuration. Build-info collection is supported via FlexPack.

### Default Behavior (Wrapped Mode)

In Wrapped Mode, Gradle requires:

1. **Configuration:** Run `jf gradle-config` to configure Artifactory repositories
2. **Artifactory Plugin:** The Artifactory Gradle Plugin is typically used for deployment
3. **Build-Info:** Automatically collected when `--build-name` and `--build-number` are provided using Build Info Extractor

### Switching to Native Mode

To use Gradle in Native Mode:

1. **Set the environment variable:** `export JFROG_RUN_NATIVE=true`
2. **Configure Gradle directly** (via `build.gradle`, `build.gradle.kts`, or `settings.gradle`)
3. **Use `jf gradle` commands** (they will run natively)
4. **Optionally configure Artifactory Gradle Plugin** in your build files if you want plugin-based deployment

### Prerequisites

1. **Gradle installed:** Ensure Gradle is installed and available in your PATH
   ```bash
   gradle --version
   ```

2. **Artifactory access:** You need Artifactory repository URLs and credentials

3. **Artifactory server configured:** Configure your Artifactory server using JFrog CLI (for authentication):
   ```bash
   jf config add my-artifactory-server --url https://myartifactory.example.com --user <user> --password <pass>
   ```

### Setting Up Gradle for Native Mode

**Step 1: Enable Native Mode**

```bash
export JFROG_RUN_NATIVE=true
```

**Step 2: Configure Gradle Repositories**

Configure Artifactory repositories in your Gradle build files. You can use either Groovy (`build.gradle`) or Kotlin DSL (`build.gradle.kts`).

**Option A: Using build.gradle (Groovy DSL - for project-specific configuration)**

```groovy
repositories {
    maven {
        url "https://your-artifactory-instance.jfrog.io/artifactory/gradle-virtual"
        credentials {
            username = project.findProperty('artifactory.user') ?: System.getenv('ARTIFACTORY_USER')
            password = project.findProperty('artifactory.password') ?: System.getenv('ARTIFACTORY_PASSWORD')
        }
    }
}

// For publishing
publishing {
    repositories {
        maven {
            url "https://your-artifactory-instance.jfrog.io/artifactory/gradle-local"
            credentials {
                username = project.findProperty('artifactory.user') ?: System.getenv('ARTIFACTORY_USER')
                password = project.findProperty('artifactory.password') ?: System.getenv('ARTIFACTORY_PASSWORD')
            }
        }
    }
}
```

**Option B: Using build.gradle.kts (Kotlin DSL - for project-specific configuration)**

```kotlin
repositories {
    maven {
        url = uri("https://your-artifactory-instance.jfrog.io/artifactory/gradle-virtual")
        credentials {
            username = project.findProperty("artifactory.user") as String? ?: System.getenv("ARTIFACTORY_USER")
            password = project.findProperty("artifactory.password") as String? ?: System.getenv("ARTIFACTORY_PASSWORD")
        }
    }
}

// For publishing
publishing {
    repositories {
        maven {
            url = uri("https://your-artifactory-instance.jfrog.io/artifactory/gradle-local")
            credentials {
                username = project.findProperty("artifactory.user") as String? ?: System.getenv("ARTIFACTORY_USER")
                password = project.findProperty("artifactory.password") as String? ?: System.getenv("ARTIFACTORY_PASSWORD")
            }
        }
    }
}
```

**Option C: Using settings.gradle or settings.gradle.kts (for multi-project builds)**

```groovy
dependencyResolutionManagement {
    repositories {
        maven {
            url "https://your-artifactory-instance.jfrog.io/artifactory/gradle-virtual"
            credentials {
                username = settings.findProperty('artifactory.user') ?: System.getenv('ARTIFACTORY_USER')
                password = settings.findProperty('artifactory.password') ?: System.getenv('ARTIFACTORY_PASSWORD')
            }
        }
    }
}
```

**Step 3: Configure Credentials**

You can configure credentials using existing JFrog CLI serverID credentials or through Gradle properties/environment variables.

**Method 1: Using JFrog CLI ServerID Credentials (Recommended)**

When `JFROG_RUN_NATIVE=true` is set, `jf gradle` commands use existing serverID credentials configured via `jf config add` for authentication with Artifactory. No additional credential configuration is needed in Gradle files if you reference the serverID.

**Method 2: Environment Variables (Recommended for CI/CD)**

```bash
export ARTIFACTORY_USER=your-username
export ARTIFACTORY_PASSWORD=your-password
```

**Method 3: gradle.properties (for local development)**

Create or edit `~/.gradle/gradle.properties`:

```properties
artifactory.user=your-username
artifactory.password=your-password
```

**Method 4: Project-specific gradle.properties**

Create `gradle.properties` in your project root:

```properties
artifactory.user=your-username
artifactory.password=your-password
```

**Step 4: Use Gradle Commands via JFrog CLI**

With `JFROG_RUN_NATIVE=true` set, `jf gradle` commands run natively:

```bash
# Build the project
jf gradle build

# Publish artifacts
jf gradle publish

# Run tests
jf gradle test

# Run with build-info collection (FlexPack)
jf gradle build --build-name=my-build --build-number=1

# Run with additional Gradle flags
jf gradle build --build-cache --parallel
```

### Build-Info Collection in Native Mode

In Native Mode, Gradle uses **FlexPack** for build-info collection instead of the Build Info Extractor. Build-info collection works in the following scenarios:

* **With Artifactory Gradle Plugin:** If you have the Artifactory Gradle Plugin configured in your `build.gradle`, JFrog CLI will detect and use it for build-info collection and artifact publishing.

* **Without Artifactory Gradle Plugin:** If the Artifactory Gradle Plugin is not configured, JFrog CLI will execute the native Gradle command and then collect build-info by parsing local resources (dependencies from `build.gradle`, artifacts from build outputs).

**Build-Info Collection Behavior:**

* **Dependencies:** All dependencies listed in `build.gradle` are captured, even if they're resolved from cache
* **Artifacts:** Only artifacts that are actually produced are included in build-info
* **Local Projects:** Local project dependencies are captured with available information
* **Multi-Module Projects:** Supported for both single and multi-module Gradle projects
* **Build Scripts:** Works with both `build.gradle` (Groovy) and `build.gradle.kts` (Kotlin DSL)

### Using Artifactory Gradle Plugin (Optional)

You can optionally use the Artifactory Gradle Plugin in Native Mode. If the plugin is detected in your build files, JFrog CLI will honor and use it for build-info collection and publishing.

**Example: build.gradle with Artifactory Plugin**

```groovy
plugins {
    id 'com.jfrog.artifactory' version '5.1.4'
}

artifactory {
    contextUrl = 'https://your-artifactory-instance.jfrog.io/artifactory'
    publish {
        repository {
            repoKey = 'gradle-local'
            username = project.findProperty('artifactory.user')
            password = project.findProperty('artifactory.password')
        }
    }
}
```

When the Artifactory Gradle Plugin is present, JFrog CLI will:

* Validate plugin configuration
* Use the plugin for build-info generation and publishing
* Throw errors if plugin configuration is insufficient

### Important Notes

* **Environment Variable Required:** You must set `JFROG_RUN_NATIVE=true` for Native Mode
* **No JFrog CLI Configuration:** Native Mode does not use `jf gradle-config` or `.jfrog` directory configuration
* **Gradle Configuration Required:** You must configure repositories in `build.gradle`, `build.gradle.kts`, or `settings.gradle`
* **Build-Info Collection:** Build-info collection works in Native Mode via FlexPack - it collects information from local resources rather than querying Artifactory
* **Authentication:** Uses existing serverID credentials configured via `jf config add` for authentication
* **Interactive Flags:** Native commands support all Gradle interactive flags and features
* **Multi-Platform Support:** Works on Linux, macOS, and Windows

### Example: Complete Native Mode Setup

**1. Enable Native Mode:**

```bash
export JFROG_RUN_NATIVE=true
```

**2. Configure Artifactory server (if not already configured):**

```bash
jf config add my-artifactory-server \
  --url=https://my-artifactory.jfrog.io \
  --user=myuser \
  --password=mypassword
```

**3. Configure build.gradle:**

```groovy
plugins {
    id 'java'
    id 'maven-publish'
}

repositories {
    maven {
        url "https://my-artifactory.jfrog.io/artifactory/gradle-virtual"
        credentials {
            username = project.findProperty('artifactory.user') ?: System.getenv('ARTIFACTORY_USER')
            password = project.findProperty('artifactory.password') ?: System.getenv('ARTIFACTORY_PASSWORD')
        }
    }
}

publishing {
    publications {
        maven(MavenPublication) {
            from components.java
        }
    }
    repositories {
        maven {
            url "https://my-artifactory.jfrog.io/artifactory/gradle-local"
            credentials {
                username = project.findProperty('artifactory.user') ?: System.getenv('ARTIFACTORY_USER')
                password = project.findProperty('artifactory.password') ?: System.getenv('ARTIFACTORY_PASSWORD')
            }
        }
    }
}
```

**4. Set credentials in gradle.properties (or use environment variables):**

```properties
artifactory.user=myuser
artifactory.password=mypassword
```

**5. Use Gradle commands via JFrog CLI:**

```bash
# Build with build-info
jf gradle build --build-name=my-build --build-number=1

# Publish artifacts
jf gradle publish --build-name=my-build --build-number=1

# Run tests
jf gradle test

# Publish build-info to Artifactory
jf rt build-publish my-build 1
```

### Migrating from Wrapped Mode to Native Mode

If you're currently using Wrapped Mode (`jf gradle` without `JFROG_RUN_NATIVE`) and want to switch to Native Mode:

1. **Set the environment variable:**
   ```bash
   export JFROG_RUN_NATIVE=true
   ```

2. **Remove or ignore JFrog CLI configuration:**
   * Native Mode ignores `.jfrog` directory configuration
   * You can keep it for reference, but it won't be used

3. **Add repositories to build.gradle, build.gradle.kts, or settings.gradle** (as shown above)

4. **Configure credentials** using one of the methods above (environment variables, gradle.properties, or JFrog CLI serverID)

5. **Optionally configure Artifactory Gradle Plugin** if you want plugin-based deployment

6. **Test the setup:**
   ```bash
   jf gradle build --build-name=test-build --build-number=1
   jf rt build-publish test-build 1
   ```

### Differences Between Wrapped and Native Mode

| Feature                    | Wrapped Mode              | Native Mode                                              |
| -------------------------- | ------------------------- | -------------------------------------------------------- |
| Configuration              | `jf gradle-config`        | `build.gradle`, `build.gradle.kts`, or `settings.gradle` |
| Build Info Collection      | Build Info Extractor      | FlexPack                                                 |
| Artifactory Plugin         | Required/Recommended      | Optional                                                 |
| Repository injection       | Automatic via init.gradle | Manual configuration required                            |
| Build script modifications | May modify init.gradle    | No modifications                                         |
| Command execution          | Wrapped execution         | Native Gradle execution                                  |
| Interactive flags          | May have limitations      | Full support                                             |
| Multi-module projects      | Supported                 | Supported                                                |
| Build script formats       | Groovy and Kotlin DSL     | Groovy and Kotlin DSL                                    |

***

## Docker

Docker requires manual setup to run in Native Mode. By default, Docker commands like `jf docker pull` and `jf docker push` use Wrapped Mode with build-info collection. To use Native Mode, you need to configure Docker directly and use native Docker commands.

### Default Behavior (Wrapped Mode)

In Wrapped Mode, Docker commands (`jf docker pull`, `jf docker push`) provide:

1. **Automatic login:** Handles Docker registry authentication via JFrog CLI config
2. **Build-info collection:** Automatically collects build-info when `--build-name` and `--build-number` are provided
3. **Artifactory integration:** Seamless integration with Artifactory Docker registries

### Switching to Native Mode

To use Docker in Native Mode, you need to:

1. **Login to Docker registry** using `docker login` or `jf docker login`
2. **Use native Docker commands** (`docker pull`, `docker push`, etc.) instead of `jf docker pull/push`
3. **Configure Docker registry** in your environment or Docker configuration

### Prerequisites

1. **Docker installed:** Ensure Docker is installed and running
   ```bash
   docker --version
   ```

2. **Artifactory Docker registry:** You need your Artifactory Docker registry URL and credentials

### Setting Up Docker for Native Mode

**Step 1: Login to Artifactory Docker Registry**

**Option A: Using JFrog CLI (Recommended)**

```bash
jf docker login [registry] --server-id <SERVER_ID>
```

Example:

```bash
jf docker login my-docker-registry.jfrog.io --server-id my-artifactory
```

**Option B: Using Native Docker Login**

```bash
docker login your-artifactory-instance.jfrog.io \
  --username your-username \
  --password your-password
```

**Step 2: Use Native Docker Commands**

After logging in, use native Docker commands:

```bash
# Pull images
docker pull my-docker-registry.jfrog.io/my-image:latest

# Build images
docker build -t my-docker-registry.jfrog.io/my-image:1.0.0 .

# Push images
docker push my-docker-registry.jfrog.io/my-image:1.0.0

# Tag images
docker tag my-image:latest my-docker-registry.jfrog.io/my-image:1.0.0
```

### Important Notes

* **Login Required:** You must login to the Docker registry before pulling/pushing images
* **No Automatic Build-Info:** Build-info is not automatically collected with native Docker commands
* **Full Docker Control:** You have full control over Docker commands and workflows
* **Registry Configuration:** Configure Docker registries using Docker's native mechanisms (`docker login`, `~/.docker/config.json`)

### Example: Complete Native Mode Workflow

**1. Login to Artifactory Docker registry:**

```bash
# Using JFrog CLI (manages credentials via jf config)
jf docker login my-docker-registry.jfrog.io --server-id my-artifactory

# Or using native Docker
docker login my-docker-registry.jfrog.io \
  --username myuser \
  --password mypassword
```

**2. Build and push using native Docker:**

```bash
# Build image
docker build -t my-docker-registry.jfrog.io/my-app:1.0.0 .

# Push image
docker push my-docker-registry.jfrog.io/my-app:1.0.0

# Pull image
docker pull my-docker-registry.jfrog.io/my-app:1.0.0
```

**3. If you need build-info, collect it separately:**

```bash
# After docker push, collect build-info manually
jf rt build-docker-create docker-local \
  --image-file image-details.txt \
  --build-name my-build \
  --build-number 1

# Publish build-info
jf rt build-publish my-build 1
```

### Migrating from Wrapped Mode to Native Mode

If you're currently using Wrapped Mode (`jf docker pull/push`) and want to switch to Native Mode:

1. **Login to Docker registry** (one-time or per session):
   ```bash
   jf docker login my-registry.jfrog.io --server-id my-artifactory
   ```

2. **Replace `jf docker pull/push` with native `docker pull/push`**

3. **Update image tags** to include full registry path:
   ```bash
   # Instead of: jf docker push my-image:tag docker-local
   # Use: docker push my-registry.jfrog.io/my-image:tag
   ```

4. **If you need build-info**, collect it separately using `jf rt build-docker-create`

### Using Docker Login with JFrog CLI

The `jf docker login` command is useful even in Native Mode because it:

* Uses credentials from JFrog CLI config (`jf c add`)
* Handles authentication automatically
* Works seamlessly with native Docker commands after login

Example:

```bash
# Configure Artifactory server (one-time)
jf c add my-artifactory \
  --url=https://my-artifactory.jfrog.io \
  --user=myuser \
  --password=mypassword

# Login to Docker registry (uses config automatically)
jf docker login my-docker-registry.jfrog.io --server-id my-artifactory

# Now use native Docker commands
docker pull my-docker-registry.jfrog.io/my-image:latest
docker push my-docker-registry.jfrog.io/my-image:1.0.0
```

***

## Maven

Maven supports Native Mode when the `JFROG_RUN_NATIVE=true` environment variable is set. In Native Mode, Maven runs without JFrog CLI configuration files and uses Maven's native configuration.

### Default Behavior (Wrapped Mode)

In Wrapped Mode, Maven requires:

1. **Configuration:** Run `jf mvn-config` to configure Artifactory repositories
2. **Build-info Extractor:** JFrog CLI uses Maven Build Info Extractor for build-info collection
3. **Automatic Deployment:** Artifacts are automatically deployed to Artifactory during the deploy phase

### Switching to Native Mode

To use Maven in Native Mode:

1. **Set the environment variable:** `export JFROG_RUN_NATIVE=true`
2. **Configure Maven directly** (via `settings.xml` or `pom.xml`)
3. **Use `jf mvn` commands** (they will run natively)

### Prerequisites

1. **Maven installed:** Ensure Maven is installed and available in your PATH
   ```bash
   mvn --version
   ```

2. **Artifactory access:** You need Artifactory repository URLs and credentials

### Setting Up Maven for Native Mode

**Step 1: Enable Native Mode**

```bash
export JFROG_RUN_NATIVE=true
```

**Step 2: Configure Maven Repositories**

Configure Artifactory repositories in Maven's `settings.xml` or project's `pom.xml`.

**Option A: Using settings.xml (Recommended for machine-wide configuration)**

Edit `~/.m2/settings.xml` or `$MAVEN_HOME/conf/settings.xml`:

```xml
<settings>
    <servers>
        <server>
            <id>artifactory-releases</id>
            <username>your-username</username>
            <password>your-password</password>
        </server>
        <server>
            <id>artifactory-snapshots</id>
            <username>your-username</username>
            <password>your-password</password>
        </server>
    </servers>
    
    <profiles>
        <profile>
            <id>artifactory</id>
            <repositories>
                <repository>
                    <id>artifactory-releases</id>
                    <url>https://your-artifactory-instance.jfrog.io/artifactory/maven-virtual</url>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                </repository>
                <repository>
                    <id>artifactory-snapshots</id>
                    <url>https://your-artifactory-instance.jfrog.io/artifactory/maven-virtual</url>
                    <releases>
                        <enabled>false</enabled>
                    </releases>
                    <snapshots>
                        <enabled>true</enabled>
                    </snapshots>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>artifactory-releases</id>
                    <url>https://your-artifactory-instance.jfrog.io/artifactory/maven-virtual</url>
                </pluginRepository>
            </pluginRepositories>
        </profile>
    </profiles>
    
    <activeProfiles>
        <activeProfile>artifactory</activeProfile>
    </activeProfiles>
</settings>
```

**Option B: Using pom.xml (for project-specific configuration)**

Add repositories and distribution management to your `pom.xml`:

```xml
<project>
    <repositories>
        <repository>
            <id>artifactory-releases</id>
            <url>https://your-artifactory-instance.jfrog.io/artifactory/maven-virtual</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
        <repository>
            <id>artifactory-snapshots</id>
            <url>https://your-artifactory-instance.jfrog.io/artifactory/maven-virtual</url>
            <releases>
                <enabled>false</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
    </repositories>
    
    <distributionManagement>
        <repository>
            <id>artifactory-releases</id>
            <url>https://your-artifactory-instance.jfrog.io/artifactory/maven-releases-local</url>
        </repository>
        <snapshotRepository>
            <id>artifactory-snapshots</id>
            <url>https://your-artifactory-instance.jfrog.io/artifactory/maven-snapshots-local</url>
        </snapshotRepository>
    </distributionManagement>
</project>
```

**Step 3: Use Maven Commands via JFrog CLI**

With `JFROG_RUN_NATIVE=true` set, `jf mvn` commands run natively:

```bash
# Clean and install
jf mvn clean install

# Deploy to Artifactory
jf mvn deploy

# Run with build-info (if needed, collect separately)
jf mvn clean install --build-name=my-build --build-number=1
```

### Important Notes

* **Environment Variable Required:** You must set `JFROG_RUN_NATIVE=true` for Native Mode
* **No JFrog CLI Configuration:** Native Mode does not use `jf mvn-config` or `.jfrog` directory configuration
* **Maven Configuration Required:** You must configure repositories in `settings.xml` or `pom.xml`
* **Build-Info Collection:** Build-info collection works differently in Native Mode - it uses FlexPack instead of Build Info Extractor
* **Deployment Behavior:** In Native Mode, `mvn install` only installs to local repository. Use `mvn deploy` to deploy to Artifactory (requires `<distributionManagement>` in `pom.xml`)

### Example: Complete Native Mode Setup

**1. Enable Native Mode:**

```bash
export JFROG_RUN_NATIVE=true
```

**2. Configure settings.xml:**

```xml
<settings>
    <servers>
        <server>
            <id>artifactory</id>
            <username>myuser</username>
            <password>mypassword</password>
        </server>
    </servers>
    
    <profiles>
        <profile>
            <id>artifactory</id>
            <repositories>
                <repository>
                    <id>artifactory</id>
                    <url>https://my-artifactory.jfrog.io/artifactory/maven-virtual</url>
                </repository>
            </repositories>
        </profile>
    </profiles>
    
    <activeProfiles>
        <activeProfile>artifactory</activeProfile>
    </activeProfiles>
</settings>
```

**3. Configure pom.xml for deployment:**

```xml
<distributionManagement>
    <repository>
        <id>artifactory</id>
        <url>https://my-artifactory.jfrog.io/artifactory/maven-releases-local</url>
    </repository>
    <snapshotRepository>
        <id>artifactory</id>
        <url>https://my-artifactory.jfrog.io/artifactory/maven-snapshots-local</url>
    </snapshotRepository>
</distributionManagement>
```

**4. Use Maven commands:**

```bash
# Build
jf mvn clean install

# Deploy
jf mvn deploy
```

### Migrating from Wrapped Mode to Native Mode

If you're currently using Wrapped Mode (`jf mvn` without `JFROG_RUN_NATIVE`) and want to switch to Native Mode:

1. **Set the environment variable:**
   ```bash
   export JFROG_RUN_NATIVE=true
   ```

2. **Remove or ignore JFrog CLI configuration:**
   * Native Mode ignores `.jfrog` directory configuration
   * You can keep it for reference, but it won't be used

3. **Configure Maven repositories** in `settings.xml` or `pom.xml` (as shown above)

4. **Update deployment configuration:**
   * Ensure `<distributionManagement>` is configured in `pom.xml` for `mvn deploy` to work
   * In Native Mode, `mvn install` does not deploy to Artifactory (unlike Wrapped Mode)

5. **Test the setup:**
   ```bash
   jf mvn clean install
   jf mvn deploy
   ```

### Differences Between Wrapped and Native Mode

| Feature                | Wrapped Mode              | Native Mode                         |
| ---------------------- | ------------------------- | ----------------------------------- |
| Configuration          | `jf mvn-config`           | `settings.xml` or `pom.xml`         |
| Build Info Extractor   | Uses Build Info Extractor | Uses FlexPack                       |
| `mvn install` behavior | May deploy to Artifactory | Only installs locally               |
| `mvn deploy` behavior  | Deploys to Artifactory    | Requires `<distributionManagement>` |
| Repository injection   | Automatic                 | Manual configuration required       |
| Lockfile fidelity      | May modify metadata       | No modifications                    |

<br />
