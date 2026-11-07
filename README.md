# Firedrill Drill Hub

Open, tested drills for [Firedrill](https://github.com/sk1122/firedrill). Each drill checks that one company safeguard actually holds, against real systems, read-only, and ships with passing, failing and not-applicable test cases.

## Use a drill

```bash
firedrill hub search branch protection
```

```bash
firedrill hub add change/no-force-push-main
```

`hub add` copies the drill into `.firedrill/drills/` and records where it came from in `.firedrill/hub.lock`. Review the file and commit both. Drills are YAML with named facts and CEL conditions: they cannot run code, and every call Firedrill makes for them is read-only.

To pick up changes later:

```bash
firedrill hub update
```

It shows the difference for each drill that changed in the hub and asks before replacing it. A drill you edited is left alone unless you pass `--force`. New drills in the official packs are offered too.

## What is here

| Path | What it holds |
| --- | --- |
| `drills/<pack>/<slug>.drill.yaml` | One drill |
| `drills/<pack>/<slug>.test.yaml` | Its test cases: the fact values for each setup and the verdict they must give |
| `hub.yaml` | The hub's name and its official packs, maintained with Firedrill |
| `template/` | A drill and test file to start from |

The official packs are Firedrill's own starter drills. Everything else comes from contributors. See [CONTRIBUTING.md](CONTRIBUTING.md) to add one.

## License

Apache-2.0. Contributions are signed off under the [Developer Certificate of Origin](https://developercertificate.org/).
