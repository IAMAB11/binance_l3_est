# BINANCE PERP L3 Order Book Estimator

![Demo GIF](demo.gif)

This project is a real-time visualization tool for the Binance perpetual swap order book. The tool uses L2 data's change in time to naively estimate a L3 order book microstructure. we can change to more complex model to estimate the L3 book later.

## Features

* **Real-time Data**: Streams order book data using Binance's WebSocket API.
* **Bid/Ask Visualization**: Displays the current bids and asks for the binance perpetual swap.
* **Order Queue Estimation**: Estimates the order queue at each price level using L2 data.
* **Dynamic Bar Coloring**: Bid and ask bars are dynamically colored based on the age of the order.
* **K-Means Cluster**: Auto classification for different market participants

## Usage

#### From Source

To try out the project, ensure you have Rust installed. You can install it from [https://www.rust-lang.org](https://www.rust-lang.org).

1. Clone the repository:

```bash
git clone https://github.com/OctopusTakopi/binance_l3_est.git
cd binance_l3_est
```

2. Run the project with a trading pair of your choice:

```bash
cargo run -r
```

#### From Release Binary

Visit the [Releases page](https://github.com/OctopusTakopi/binance_l3_est/releases) and download the latest binary release.

The chart dynamically updates as new WebSocket messages are received, and the bars for bids and asks are color-coded based on the order age, in K-means mode it based on the order size.

> **Note:** Allow enough time for the estimator to start working as it processes the historical L2 data.

## Development

### Prerequisites

- Rust 1.93.0 or later
- Cargo (comes with Rust)

### Building

```bash
# Build in debug mode
cargo build

# Build in release mode (optimized)
cargo build --release
```

### Testing

```bash
# Run tests
cargo test

# Run tests with verbose output
cargo test --verbose
```

### Code Quality

```bash
# Format code
cargo fmt

# Check formatting without modifying files
cargo fmt --check

# Run Clippy linter
cargo clippy --all-targets --all-features

# Run Clippy with strict warnings
cargo clippy --all-targets --all-features -- -D warnings
```

## Deployment

### Continuous Integration

This repository includes GitHub Actions workflows for:

- **CI Pipeline** (`.github/workflows/ci.yml`): Runs on every push and pull request to main/master branches
  - Code formatting checks
  - Clippy linting
  - Build verification
  - Test execution
  - Security audit
  - Multi-platform builds (Linux, Windows, macOS)

- **Release Pipeline** (`.github/workflows/Release.yml`): Triggered by version tags or manually
  - Builds release binaries for all platforms
  - Creates GitHub releases with binaries attached
  - Uploads artifacts for download

### Creating a Release

To create a new release:

1. Update the version in `Cargo.toml`
2. Commit the changes
3. Create and push a version tag:

```bash
git tag -a v0.1.0 -m "Release version 0.1.0"
git push origin v0.1.0
```

The release workflow will automatically build binaries for Linux, Windows, and macOS, and create a GitHub release with all the artifacts.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
