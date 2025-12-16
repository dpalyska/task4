### Zad 1

wykryte problemy:

Java (jar)
==========
Total: 72 (UNKNOWN: 0, LOW: 5, MEDIUM: 27, HIGH: 32, CRITICAL: 8)

### Zad 2 

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

### Zad 3
konfiguracji CI:

```
name: Security Scan

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  security-tests:
    runs-on: ubuntu-latest

    steps:
      - name: Check out code
        uses: actions/checkout@v4

      - name: Build Docker image
        run: |
          docker build -t myapp:latest .

      - name: Run Trivy scan
        uses: aquasecurity/trivy-action@0.33.1
        with:
          image-ref: 'myapp:latest'
          vuln-type: 'os,library'
          format: 'table'

      - name: Install Semgrep
        run: |
          python3 -m pip install --upgrade pip
          pip install semgrep

      - name: Run Semgrep SAST
        run: |
          semgrep --config p/security-audit --error --json .
```

### Zad 4
ZAP znalazł 4 medium, 4 low, 5 informational problemy.

Test skanujący z narzędziem Trivy wykazał jakie możliwe są podatności związane z używanymi w aplikacji bibliotekami.
Statyczna analiza kodu Semgrep wykazała możliwe problemy w aplikacji związane z samym kodem aplikacji, które mogłyby pozwolić atakującemu na dostanie się do aplikacji bądź jej zablokowanie / zcrashowanie.
Skan ZAP pokazał możliwe problemy związane z komunikacją siecową w naszej aplikacji (na przykład brak tokenów CSRF)

Każde narzędzie skupiło się na innym fragmencie działającej aplikacji, by stworzyć bezpieczną aplikację, trzeba zapoznać się z komunikatami ze wszystkich trzech aplikacji.