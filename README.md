# WatchRun

A modern, cross-platform CLI tool that monitors file changes and automatically executes commands. Perfect for development workflows, build automation, and continuous testing.

## Features

- **Recursive Directory Monitoring** - Watch entire directory trees
- **Smart File Filtering** - Monitor specific file extensions and patterns
- **Multi-Command Execution** - Run multiple commands per trigger
- **Colorful Terminal Output** - Modern, informative display with ANSI colors
- **Configuration Files** - Save and load settings from `.watchrunrc`
- **Cross-Platform** - Works on Linux, macOS, and Windows
- **Daemon Mode** - Run in background as a service
- **JSON Output** - Machine-readable output for integration
- **Pattern Matching** - Include/exclude files with glob patterns
- **Configurable Polling** - Adjust monitoring frequency

## Quick Start

### Build from Source

```bash
git clone https://github.com/DitzDev/watchrun
cd watchrun
make
```

### Basic Usage

```bash
# Watch C files and run make
./watchrun -w src -e c,h -x "make"

# Watch Python files with custom interval
./watchrun -w . -e py -x "python test.py" -i 500

# Multiple commands with patterns
./watchrun -w src --include "*.c" --exclude "*test*" -x "make" -x "./run_tests"
```

## Command Line Options

### Required Options
- `-w, --watch PATH` - Directory to watch for changes
- `-x, --exec CMD` - Command to execute on changes (can be used multiple times)

### Optional Options
- `-e, --ext EXT` - File extensions to watch (comma-separated)
- `-i, --interval MS` - Polling interval in milliseconds (default: 1000)
- `-c, --config FILE` - Configuration file path
- `--include PATTERN` - Include files matching pattern
- `--exclude PATTERN` - Exclude files matching pattern  
- `--no-clear` - Don't clear screen before running commands
- `--no-recursive` - Don't watch subdirectories
- `--daemon` - Run as daemon process
- `--json` - Output in JSON format
- `--verbose` - Verbose output
- `--quiet` - Suppress banner and info messages
- `--save-config` - Save current configuration to file
- `-h, --help` - Show help message
- `-v, --version` - Show version information

## 🔧 Configuration File

Create a `.watchrunrc` file to save your settings:

```ini
# watchrun configuration file
watch_path=src
extensions=c,h,cpp,hpp
commands=make,./run_tests
interval=1000
include_patterns=*.c,*.h
exclude_patterns=*test*,*tmp*
recursive=true
verbose=false
quiet=false
daemon=false
json_output=false
no_clear=false
```

### Using Configuration Files

```bash
# Load config file
./watchrun -c ~/.watchrunrc

# Save current settings to config
./watchrun -w src -e c,h -x "make" --save-config -c .watchrunrc
```

## Usage Examples

### Development Workflow

```bash
# Auto-build C project
./watchrun -w src -e c,h -x "make clean" -x "make" -x "./run_tests"

# Python development with testing
./watchrun -w . -e py --exclude "*__pycache__*" -x "python -m pytest"

# Web development
./watchrun -w assets -e css,js,html -x "npm run build" -x "npm run test"
```

### Advanced Patterns

```bash
# Watch specific patterns only
./watchrun -w . --include "src/*.c" --include "include/*.h" -x "make"

# Exclude temporary and build files
./watchrun -w . -e c,h --exclude "*tmp*" --exclude "build/*" -x "make"

# JSON output for integration
./watchrun -w src -e py -x "python test.py" --json --quiet
```

### Daemon Mode

```bash
# Run in background
./watchrun -c ~/.watchrunrc --daemon

# With systemd (Linux)
sudo systemctl enable watchrun@user.service
sudo systemctl start watchrun@user.service
```

## Build Options

### Standard Build
```bash
make                # Build release version
make debug          # Build with debug symbols
make dev            # Build with sanitizers
```

### Cross-Platform
```bash
make windows        # Cross-compile for Windows (requires MinGW)
```

### Installation
```bash
make install              # Install to /usr/local/bin (Unix)
make install-termux      # Install to $PREFIX/bin (Termux)
make uninstall-termux    # Remove from $PREFIX/bin (Termux)
make uninstall            # Remove from system
```

### Development
```bash
make format         # Format code (requires clang-format)
make analyze        # Static analysis (requires cppcheck) 
make test           # Run basic tests
make package        # Create distribution package
```

## Contributing

1. Fork repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -am 'Add amazing feature'`)
4. Push branch (`git push origin feature/amazing-feature`)
5. Create Pull Request

## License
```
MIT License

Copyright (c) 2025 DitzDev

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```