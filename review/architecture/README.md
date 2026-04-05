# Architecture

## Contents

* [Deep Modules](deep-modules.md)
* [Domain Functions](domain-functions.md)


## Ralph Review Configuration

To configure `ralph review` with every architecture section as a review item, add the following to your `.ralph/config.yaml` file:

```yaml
review:
  items:
    - url: https://raw.githubusercontent.com/zon/code/main/review/architecture/deep-modules.md
    - url: https://raw.githubusercontent.com/zon/code/main/review/architecture/domain-functions.md
```
