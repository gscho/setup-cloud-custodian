# setup-cloud-custodian

This action installs [cloud custodian](https://cloudcustodian.io/) and adds it to the `$PATH`.

It also supports installing the `c7n_azure` and `c7n_gcp` extensions via action inputs.

## Inputs

| name  | type  | default  | description  |
|---|---|---|---|
| include-gcp  | boolean  | false  | set to `true` to install the c7n_gcp extension  |
| include-azure  | boolean  | false  | set to `true` to install the c7n_azure extension  |
| include-c7n-org  | boolean  | false  | set to `true` to install c7n-org and add it to the `$PATH`  |

### Supported Platforms

This action is tested and working with `Ubuntu` GitHub Hosted runners. It requires `python3`.

## Usage

### Running a policy from within a repo

```
name: My workflow
on:
  schedule:
    - cron: "00,30 * * * *"
jobs:
  run-my-policy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: gscho/setup-cloud-custodian@v1
    - run: custodian run -s out path/to/my-policy.yml
```

### Installing Azure and GCP extensions

```
name: My workflow
on:
  schedule:
    - cron: "00,30 * * * *"
jobs:
  run-my-policy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: gscho/setup-cloud-custodian@v1
      with:
        include-azure: true
        include-gcp: true
    - run: custodian run -s out path/to/my-policy.yml
```

### Installing c7n-org

```
name: My workflow
on:
  schedule:
    - cron: "00,30 * * * *"
jobs:
  run-my-policy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: gscho/setup-cloud-custodian@v1
      with:
        include-c7n-org: true
    - run: c7n-org run -c accounts-all.yaml -u my-policy -s output-dir -r us-east-1
```

### Installing a specific version

```
name: My workflow
on:
  workflow_dispatch:
jobs:
  print-version:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: gscho/setup-cloud-custodian@v1
      with:
        custodian-version: '0.9.7.0'
    - run: custodian version
```
