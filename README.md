# spea-PolicyLint
A command-line tool to lint security policies written in YAML or JSON format.

Checks that run on the policy itself, without needing a schema to encode them:
- Contradiction: a policy that sets both `allow_all` and `deny_all` to true is a contradiction finding.
- Contradiction: an entry that appears in both the allow list (`allow` or `allowed`) and the deny list (`deny` or `denied`) is a contradiction finding.
- Invalid value: `allow_all` and `deny_all`, when present, must be booleans.

Missing field checks run through the operator supplied JSON Schema: a schema `required` list is enforced by schema validation, and a policy missing a required field fails at exit 1. That schema validation is the other check the tool performs. The tool ships no standards policy sets: it does not include CIS, NIST, or any other built in policy set, and it performs no checks beyond the built in checks above and the operator supplied schema.

An empty policy is nothing to lint: the run exits non-zero with a nothing to lint message and prints no success line. An empty schema is allowed, because the built in checks still run; if no check ran at all, the run also exits non-zero.

## Install
`git clone https://github.com/ShadowGuard-AI/spea-policylint`

## Usage
`python3 main.py POLICY_FILE SCHEMA_FILE [--format yaml|json] [--log_level LEVEL]`

## Parameters
- `policy_file`: Path to the security policy file (YAML or JSON).
- `schema_file`: Path to the JSON schema file.
- `-h`: Show help message and exit
- `--format`: Format of the policy file (yaml or json). Defaults to yaml.
- `--log_level`: Set the logging level. Defaults to INFO.

## License
Copyright (c) ShadowGuardAI
