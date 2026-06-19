# Gobuster

## Available Commands

- **completion** - Generate the autocompletion script for the specified shell
- **dir** - Uses directory/file enumeration mode
- **dns** - Uses DNS subdomain enumeration mode
- **fuzz** - Uses fuzzing mode. Replaces the keyword FUZZ in the URL, Headers and the request body
- **gcs** - Uses gcs bucket enumeration mode
- **help** - Help about any command
- **s3** - Uses aws bucket enumeration mode
- **tftp** - Uses TFTP enumeration mode
- **version** - Shows the current version
- **vhost** - Uses VHOST enumeration mode (you most probably want to use the IP address as the URL parameter)

## Most Commonly Used Flags

| Flag | Description |
|------|-------------|
| `--debug` | Enable debug output |
| `--delay duration` | Time each thread waits between requests (e.g. 1500ms) |
| `-h, --help` | Help for gobuster |
| `--no-color` | Disable color output |
| `--no-error` | Don't display errors |
| `-z, --no-progress` | Don't display progress |
| `-o, --output string` | Output file to write results to (defaults to stdout) |
| `-p, --pattern string` | File containing replacement patterns |
| `-q, --quiet` | Don't print the banner and other noise |
| `-t, --threads int` | Number of concurrent threads (default 10) |
| `-v, --verbose` | Verbose output (errors) |
| `-w, --wordlist string` | Path to the wordlist. Set to - to use STDIN. |
| `--wordlist-offset int` | Resume from a given position in the wordlist (defaults to 0) |

Use `gobuster [command] --help` for more information about a command.

## Example

Let us look at an example of how we would use these commands and flags together to enumerate a web directory:

```bash
gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
```

- `gobuster dir` indicates that we will use the directory and file enumeration mode
- `-u "http://www.example.com/"` tells Gobuster that the target URL is `http://example.com/`
- `-w /usr/share/wordlists/dirb/small.txt` directs Gobuster to use the small.txt wordlist to brute force the web directories. Gobuster will use each entry in the wordlist to form a new URL and send a GET request to that URL. If the first entry of the wordlist were images, Gobuster would send a GET request to `http://example.com/images/`
- `-t 64` sets the number of threads Gobuster will use to 64. This improves the performance drastically