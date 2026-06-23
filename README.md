# Enable Detailed Logs — Java Console

A Java console application that demonstrates how to enable full verbose logging — the programmatic equivalent of navigating to:

**Java Control Panel → Advanced → Java Console → Show Console**

When a remote console connection fails and the cause is unclear, detailed logs help identify exactly what is happening. The output can reveal issues such as firewall blocks, SSL certificate mismatches, Java Security Manager denials, invalid ports, or connection timeouts.

The project simulates realistic troubleshooting scenarios while showing how different logging levels expose progressively deeper diagnostic information.

---

## Project Structure

```text
src/main/java/com/logger/
├── Main.java
├── config/
│   ├── LoggerConfig.java
│   └── DetailedFormatter.java
├── handlers/
│   └── DetailedConsoleHandler.java
├── demo/
│   └── ConnectionDemo.java

src/main/resources/
└── logging.properties

logs/
└── app.log
```

---

## Log Levels

| Level     | Purpose                                  |
| --------- | ---------------------------------------- |
| `FINEST`  | DNS lookup, TCP SYN, policy checks       |
| `FINER`   | Handshake progress and retry counts      |
| `FINE`    | Socket creation and certificate details  |
| `INFO`    | Important application events             |
| `WARNING` | Potential problems detected              |
| `SEVERE`  | Connection failures with suggested fixes |

---

## Build & Run

```cmd
mkdir out && mkdir logs
dir /s /b src\*.java > sources.txt
javac -d out @sources.txt
java -cp out com.logger.Main
```

## Output

Detailed logs are automatically displayed in the console and written to:

```text
logs/app.log
```

Example output:

```text
[2026-06-23 10:15:33] INFO     Starting connection attempt...
[2026-06-23 10:15:34] FINEST   Resolving DNS...
[2026-06-23 10:15:35] WARNING  Certificate mismatch detected
[2026-06-23 10:15:35] SEVERE   Connection refused
Fix: Verify target host and port settings
```
