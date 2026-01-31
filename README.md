# DNS_LOOKUP

## ✨ Features

- 🔍 **Multi-Record Queries**: Query A, AAAA, MX, NS, TXT, CNAME, SOA records
- 🔄 **Reverse DNS**: IP to hostname resolution
- 🗺️ **DNS Trace**: Visualize the complete resolution path from root to authoritative servers
- 📦 **Batch Lookups**: Query multiple domains concurrently with progress tracking
- 📋 **WHOIS Integration**: Retrieve comprehensive domain registration information
- 📊 **JSON Export**: Machine-readable output for scripting and automation
- 🎨 **Beautiful Output**: Color-coded tables, progress spinners, and tree visualizations
- ⚡ **Fast & Efficient**: Optimized DNS queries with concurrent processing
- 🛠️ **Custom DNS Servers**: Use specific DNS resolvers for queries
- 📱 **Cross-Platform**: Works on Windows, macOS, and Linux

## 🚀 Installation

### Prerequisites

- Python 3.13 or higher
- pip (Python package installer)

### Quick Install

#### Option 1: Install from PyPI (Recommended)

```bash
pip install dnslookup-cli
```

#### Option 2: Install from Source

```bash
# Create virtual environment (recommended)
python -m venv .venv

# Activate virtual environment
# On Windows:
.venv\Scripts\activate
# On macOS/Linux:
source .venv/bin/activate

# Install the package
pip install -e .
```

#### Option 3: Using uv (Modern Python Package Manager)

```bash
# Install uv if not already installed
pip install uv


# Sync dependencies
uv sync
```

## 📖 Usage

### Basic DNS Query

Query all DNS record types for a domain:

```bash
dnslookup query example.com
```

### Specific Record Types

Query only specific record types:

```bash
# Query A and MX records
dnslookup query example.com --type A,MX

# Query multiple types
dnslookup query google.com --type A,AAAA,MX,TXT
```

### Custom DNS Server

Use a specific DNS server for queries:

```bash
# Use Google DNS
dnslookup query example.com --server 8.8.8.8

# Use Cloudflare DNS
dnslookup query example.com --server 1.1.1.1
```

### JSON Output

Get machine-readable JSON output for scripting:

```bash
dnslookup query example.com --json
```

### Reverse DNS Lookup

Convert IP addresses to hostnames:

```bash
# IPv4 reverse lookup
dnslookup reverse 8.8.8.8

# IPv6 reverse lookup
dnslookup reverse 2606:4700:4700::1111
```

### DNS Trace

Visualize the complete DNS resolution path:

```bash
# Trace A records
dnslookup trace example.com

# Trace MX records
dnslookup trace example.com --type MX
```

### Batch Lookups

Process multiple domains from a file:

```bash
# Create a domains file
echo "google.com
github.com
stackoverflow.com
cloudflare.com" > domains.txt

# Run batch lookup
dnslookup batch domains.txt

# Save results to JSON file
dnslookup batch domains.txt --output results.json
```

### WHOIS Lookup

Retrieve domain registration information:

```bash
dnslookup whois example.com

# JSON output
dnslookup whois example.com --json
```

## 📋 Command Reference

| Command | Description | Options |
|---------|-------------|---------|
| `dnslookup query <domain>` | Query DNS records | `--type`, `--server`, `--json` |
| `dnslookup reverse <ip>` | Reverse DNS lookup | `--server`, `--json` |
| `dnslookup trace <domain>` | DNS resolution trace | `--type`, `--server` |
| `dnslookup batch <file>` | Batch domain lookup | `--output`, `--type`, `--server` |
| `dnslookup whois <domain>` | WHOIS information | `--json` |

## 🎯 Examples

### DNS Query Output
```
🌐 DNS Lookup: example.com
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

                                DNS Records
┌──────────┬───────────────────────────────────────────────────┬──────────┐
│ Type     │ Value                                             │      TTL │
├──────────┼───────────────────────────────────────────────────┼──────────┤
│ A        │ 93.184.216.34                                     │      1h │
│ AAAA     │ 2606:2800:220:1:248:1893:25c8:1946               │      1h │
│ MX       │ mail.example.com (priority: 10)                  │      1d │
│ NS       │ ns1.example.com                                   │      2d │
│ NS       │ ns2.example.com                                   │      2d │
│ TXT      │ "v=spf1 -all"                                     │      1h │
│ SOA      │ ns1.example.com, admin.example.com, 2023010101    │      1h │
└──────────┴───────────────────────────────────────────────────┴──────────┘

✓ Found 7 records in 234ms
```

### DNS Trace Output
```
🔍 DNS Trace: example.com
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🌍 DNS Resolution Path
├── [.] Root Servers
│   └── → a.root-servers.net (198.41.0.4)
│       └── Referred to .com TLD servers
├── [com.] TLD Servers
│   └── → a.gtld-servers.net (192.5.6.30)
│       └── Referred to example.com nameservers
└── [example.com.] Authoritative Servers
    └── → ns1.example.com (93.184.216.34)
        └── A: 93.184.216.34

✓ Resolution complete in 156ms
```

### Batch Processing
```
📦 Batch DNS Lookup
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Processing domains: google.com, github.com, stackoverflow.com

google.com          ✓ 8 records (142ms)
github.com          ✓ 12 records (98ms)
stackoverflow.com   ✓ 6 records (203ms)

✓ Batch complete: 3/3 domains processed in 443ms
```

## 🛠️ Development

### Setup Development Environment

```bash
# Install development dependencies
pip install -e ".[dev]"

# Or with uv
uv sync --dev
```

### Available Development Commands

```bash
# Run the tool
dnslookup query example.com

# Run tests
pytest

# Run with coverage
pytest --cov=dnslookup

# Lint code
ruff check .

# Format code
ruff format .

# Type checking
mypy dnslookup/
```

### Project Structure

```
dns-lookup/
├── dnslookup/
│   ├── __init__.py
│   ├── cli.py          # Main CLI application
│   ├── dns_client.py   # DNS query logic
│   ├── whois_client.py # WHOIS functionality
│   └── utils.py        # Helper functions
├── tests/
│   ├── test_cli.py
│   ├── test_dns.py
│   └── test_whois.py
├── pyproject.toml      # Project configuration
├── justfile           # Development tasks
└── README.md          # This file
```

## 🔧 Configuration

The tool uses sensible defaults but can be configured via environment variables:

```bash
# Set default DNS server
export DNS_DEFAULT_SERVER=8.8.8.8

# Set default timeout (seconds)
export DNS_TIMEOUT=10

# Enable debug logging
export DNS_DEBUG=true
```

## 🐛 Troubleshooting

### Common Issues

**"Command not found"**
- Ensure the package is installed: `pip install dnslookup-cli`
- Check if virtual environment is activated

**"DNS timeout"**
- Try a different DNS server: `--server 8.8.8.8`
- Check your internet connection

**"Python version error"**
- Requires Python 3.13+: `python --version`
- Upgrade Python if necessary

**"Permission denied"**
- On Linux/macOS, you might need to adjust permissions
- Try running with `sudo` (not recommended for security)

### Getting Help

```bash
# Show help
dnslookup --help

# Show command-specific help
dnslookup query --help
dnslookup batch --help
```

## 📊 Performance

- **Concurrent Queries**: Batch processing uses asyncio for parallel DNS queries
- **Optimized Resolvers**: Uses dnspython for efficient DNS resolution
- **Memory Efficient**: Streams large batch files without loading everything into memory
- **Fast WHOIS**: Cached WHOIS server detection for improved performance

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

### Development Guidelines

- Follow PEP 8 style guidelines
- Add tests for new features
- Update documentation
- Ensure all tests pass

## 🙏 Acknowledgments

- [dnspython](https://www.dnspython.org/) - DNS toolkit for Python
- [Rich](https://github.com/Textualize/rich) - Beautiful terminal output
- [Typer](https://typer.tiangolo.com/) - Modern CLI framework
- [python-whois](https://github.com/richardpenman/whois) - WHOIS library

## 👤 Author

**Anike**  
Cybersecurity Enthusiast & Developer

- **Email**: [your-email@example.com](mailto:your-email@example.com)
- **GitHub**: [your-github-username](https://github.com/your-github-username)
- **LinkedIn**: [Your LinkedIn Profile](https://linkedin.com/in/your-profile)
- **Portfolio**: [Your Portfolio Website](https://your-portfolio.com)

## 📞 Contact & Support

- **Issues**: [GitHub Issues](https://github.com/your-username/Cybersecurity-Projects/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-username/Cybersecurity-Projects/discussions)
- **Email**: your-email@example.com

---

**Made with ❤️ by Anike**

#   D N S _ L O O K U P 
 
 # DNS_LOOKUP
