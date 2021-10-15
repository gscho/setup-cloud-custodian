# setup-cloud-custodian

This action installs [cloud custodian](https://cloudcustodian.io/) and adds it to the `PATH`.

It also supports installing the `c7n_azure` and `c7n_gcp` extensions via action inputs.

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
  test:
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
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: gscho/setup-cloud-custodian@v1
      with:
        include-azure: true
        include-gcp: true
    - run: custodian run -s out path/to/my-policy.yml
```
