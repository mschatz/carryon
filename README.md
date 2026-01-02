# 🛫 carryon

Prepare web content for offline reading during air travel. Downloads top Hacker News stories and caches them as self-contained HTML files for offline viewing.

## Features

- 📰 Download top N Hacker News stories (default: 500)
- 💾 Cache full webpages using [monolith](https://github.com/Y2Z/monolith) - each page is a single self-contained HTML file
- 🖼️ Includes images and CSS (videos not included)
- 📑 Generate a lightweight index.html with story metadata (title, rank, score)
- ✈️ Perfect for air travel and offline reading

## Installation

### Prerequisites

This tool is designed for macOS and requires:

- **curl**: Built-in on macOS
- **jq**: JSON parser
- **monolith**: Webpage archiver

Install dependencies using Homebrew:

```bash
brew install jq monolith
```

### Install carryon

1. Clone this repository:
```bash
git clone https://github.com/mschatz/carryon.git
cd carryon
```

2. Make the script executable (if not already):
```bash
chmod +x carryon
```

3. (Optional) Add to your PATH:
```bash
# Add to ~/.zshrc or ~/.bash_profile
export PATH="$PATH:/path/to/carryon"
```

Or copy to a directory in your PATH:
```bash
sudo cp carryon /usr/local/bin/
```

## Usage

### Basic Usage

Download top 500 Hacker News stories:
```bash
./carryon
```

### Options

```
Usage: carryon [OPTIONS]

OPTIONS:
    -n NUM      Number of stories to download (default: 500)
    -o DIR      Output directory (default: ~/carryon-cache)
    -v          Verbose output
    -h          Show this help message
```

### Examples

Download top 100 stories:
```bash
./carryon -n 100
```

Download to a specific directory:
```bash
./carryon -n 50 -o ./my-hn-cache
```

Download with verbose output:
```bash
./carryon -v -n 10
```

### Environment Variables

You can also configure carryon using environment variables:

- `CARRYON_NUM_STORIES`: Number of stories (default: 500)
- `CARRYON_OUTPUT_DIR`: Output directory (default: ~/carryon-cache)
- `CARRYON_VERBOSE`: Enable verbose output (default: 0)

Example:
```bash
export CARRYON_NUM_STORIES=100
export CARRYON_OUTPUT_DIR="$HOME/hn-offline"
./carryon
```

## Output

carryon creates a directory with:

- `index.html` - Browse all cached stories with metadata
- `story-<id>.html` - Self-contained HTML file for each story

Each cached HTML file includes:
- All images (embedded as base64)
- All CSS styles (inlined)
- Complete page content for offline viewing

Videos are not included to keep file sizes reasonable.

## Typical Workflow

Before your flight:
```bash
# Download top 100 stories
./carryon -n 100

# Open the index
open ~/carryon-cache/index.html
```

During your flight:
- Open `~/carryon-cache/index.html` in your browser
- Browse and read stories offline
- All links work locally (no internet required)

## Tips

- **Start small**: Try with `-n 10` first to test the tool
- **Be patient**: Caching 500 stories can take 15-30 minutes
- **Check your disk space**: Each cached page can be 1-5 MB
- **Some pages may fail**: Sites with aggressive bot protection might not cache properly

## Troubleshooting

### "command not found: monolith"
Install monolith: `brew install monolith`

### "command not found: jq"
Install jq: `brew install jq`

### "Failed to cache story"
Some websites block automated downloading or have complex authentication. These stories will link to the original URL instead.

### Slow downloads
This is normal. The tool processes each story sequentially and respects rate limits. Use `-n` with a smaller number for faster testing.

## License

See [LICENSE](LICENSE) file for details.

## Contributing

Contributions welcome! Please feel free to submit a Pull Request.
