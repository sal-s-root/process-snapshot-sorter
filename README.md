# process-snapshot-sorter

Rank a supplied process snapshot by CPU consumption.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "limit": 1,
  "processes": [
    {
      "pid": 2,
      "name": "worker",
      "cpu_percent": 70
    },
    {
      "pid": 1,
      "name": "shell",
      "cpu_percent": 2
    }
  ]
}
```

Result:

```json
{
  "processes": [
    {
      "pid": 2,
      "name": "worker",
      "cpu_percent": 70.0
    }
  ]
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

Does not sample live processes; CPU percentages depend on the upstream collection interval.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [file-integrity-manifest](https://github.com/sal-s-root/file-integrity-manifest), [system-load-analyzer](https://github.com/sal-s-root/system-load-analyzer).
