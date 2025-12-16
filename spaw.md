### Zad 1

wykryte problemy:

Java (jar)
==========
Total: 72 (UNKNOWN: 0, LOW: 5, MEDIUM: 27, HIGH: 32, CRITICAL: 8)

### Zad 2 

docker run --rm -v "$(pwd)":/src returntocorp/semgrep semgrep scan


✅ Scan completed successfully.
 • Findings: 24 (24 blocking)
 • Rules run: 448
 • Targets scanned: 1793
 • Parsed lines: ~99.9%
 • Scan skipped:
   ◦ Files larger than  files 1.0 MB: 2
   ◦ Files matching .semgrepignore patterns: 30
 • Scan was limited to files tracked by git
 • For a detailed list of skipped files and lines, run semgrep with the --verbose flag
Ran 448 rules on 1793 files: 24 findings.