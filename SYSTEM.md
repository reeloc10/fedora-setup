# System Setup

Useful commands on a fresh Fedora 45 environment.

## 1. Isolate application network

Run any command inside an empty network namespace without root privileges:

```bash
unshare --net --user --map-root-user <command>
```

### Verification

```bash
python3 urllib_inspector.py "https://www.google.com"
# Expected: [*] Request successful! (200 OK)

unshare --net --user --map-root-user python3 urllib_inspector.py "https://www.google.com"
# Expected: [!] Network or URL Error: [Errno 101] Network is unreachable
```
