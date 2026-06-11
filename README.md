# Datadog Orchestrion Buildpack

[![Buildpack](https://img.shields.io/badge/buildpack-0.7-blue)](https://buildpacks.io/docs/buildpack-api/) [![Go](https://img.shields.io/badge/go-1.21%2B-00ADD8?logo=go&logoColor=white)](https://go.dev) [![Datadog](https://img.shields.io/badge/datadog-orchestrion-632CA6?logo=datadog&logoColor=white)](https://docs.datadoghq.com/orchestrion/)

**A Cloud Native Buildpack for installing [Datadog Orchestrion](https://github.com/datadog/orchestrion/) in Go applications**

## 📋 About

This buildpack automates the installation of [Datadog Orchestrion](https://github.com/datadog/orchestrion/) as part of your Cloud Native Buildpacks build process. It's designed specifically for Go applications and ensures that Orchestrion is available during both build and runtime phases.

Orchestrion is Datadog's internal service discovery tool that helps manage and monitor containerized workloads, making it easier to integrate with Datadog's APM, logs, and infrastructure monitoring.

## ✨ Features

- ✅ **Automatic Detection**: Automatically detects Go projects via `go.mod` file
- ✅ **Caching**: Uses buildpack layer caching to speed up subsequent builds
- ✅ **PATH Integration**: Adds Orchestrion binary to the build and launch PATH
- ✅ **Multi-Stack Support**: Compatible with `bionic` and `jammy` stacks
- ✅ **Lightweight**: Minimal overhead, only installs when needed

## 🏗️ Requirements

- Cloud Native Buildpacks compliant platform (Paketo, Heroku, etc.)
- Go 1.21+ (via `go.mod` file in your project)
- One of the supported stacks: `io.buildpacks.stacks.bionic` or `io.buildpacks.stacks.jammy`

## 📦 Installation

### Using with Paketo

Add this buildpack to your buildpack group:

```bash
pack build my-app \\
  --buildpack .... \\
  --buildpack https://github.com/groupe-rossel/tech-cloud-go-orchestrion-buildpacks.git 
```

## 🚀 Usage

Once installed, Orchestrion will be available in your build environment. The buildpack:

1. **Detects** if your project is a Go application (presence of `go.mod`)
2. **Installs** Datadog Orchestrion binary via `go install github.com/DataDog/orchestrion@latest`
3. **Caches** the binary for faster subsequent builds
4. **Exposes** the binary in the PATH for both build and launch phases

### Example Go Application

Your project should have a `go.mod` file:

```go
module github.com/yourorg/your-app

go 1.21

require (
    // your dependencies
)
```

The buildpack will automatically detect this and install Orchestrion.

## 🔧 Configuration

This buildpack currently uses default configurations. Future versions may support:

- Specifying Orchestrion version via environment variables
- Custom installation paths
- Configuration flags for Orchestrion

## 📄 Buildpack Metadata

| Property | Value |
|----------|-------|
| **Buildpack API** | 0.7 |
| **Buildpack ID** | `be.rossel.tech.orchestrion` |
| **Version** | 1.0.0 |
| **Name** | Datadog Orchestrion Installer |
| **Supported Stacks** | `io.buildpacks.stacks.bionic`, `io.buildpacks.stacks.jammy` |

## 📁 Repository Structure

```
.
├── bin/
│   ├── detect          # Buildpack detection script
│   └── build           # Buildpack build script
├── buildpack.toml      # Buildpack metadata
└── README.md           # This file
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Update tests and documentation as needed
5. Commit your changes (`git commit -m 'feat: add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Development Setup

```bash
# Clone the repository
git clone https://github.com/rossel-tech/tech-cloud-go-orchestrion-buildpacks.git
cd tech-cloud-go-orchestrion-buildpacks

# Make changes to bin/detect and bin/build
chmod +x bin/detect bin/build

# Test locally with pack
git clone https://github.com/your-go-app.git
echo "be.rossel.tech.orchestrion = ./tech-cloud-go-orchestrion-buildpacks" > project.toml
pack build test-app --path ./your-go-app --buildpack ghcr.io/paketo-buildpacks/go
```

## 🆘 Support

For issues, questions, or feature requests:

- Open an issue in this repository
- Contact the Rossel Tech Cloud team

## 📚 Resources

- [Cloud Native Buildpacks Documentation](https://buildpacks.io/docs/)
- [Datadog Orchestrion Documentation](https://docs.datadoghq.com/orchestrion/)
- [Paketo Buildpacks](https://paketo.io/)
- [Buildpack Specifications](https://github.com/buildpacks/spec)

---

**Buildpack maintained by [Rossel Tech Cloud Team](https://github.com/rossel-tech)**

*Built with love for the Cloud Native ecosystem*
