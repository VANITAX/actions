## Example
```yaml
name: Flexible env

on:
  push:
  pull_request:
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: SolarGang/actions/flexible-env
      - run: echo ${{ env.FLEX_GIT_SHA }}
      - run: echo ${{ env.FLEX_GIT_REF }}
      - run: echo ${{ env.FLEX_GIT_SHA_SHORT }}
      - run: echo ${{ env.FLEX_GIT_REF_SHORT }}
      - run: echo ${{ env.FLEX_GIT_REF_FORMAT }}

      - run: echo ${{ env.FLEX_GIT_TAG }}
        if: env.FLEX_GIT_TAG
```

Change FLEX_GIT_SHA_SHORT length
```yaml
- uses: SolarGang/actions/flexible-env
  with:
    git_short_length: 10
- run: echo ${{ env.FLEX_GIT_SHA }}
  # 4fc2064c87d57440f9fd03ef8f68adcb4fd3cfdc
- run: echo ${{ env.FLEX_GIT_SHA_SHORT }}
  # 4fc2064c87
```

Get tag
```yaml
name: Flexible env - get tag

on:
  push:
    tags:
      - "**"
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: SolarGang/actions/flexible-env
      - run: echo $GITHUB_REF
        # refs/tags/v1.1.1
      - run: echo ${{ env.FLEX_GIT_TAG }}
        if: env.FLEX_GIT_TAG
        # v1.1.1
```

## Values
```bash
FLEX_GIT_SHA: 4fc2064c87d57440f9fd03ef8f68adcb4fd3cfdc
FLEX_GIT_REF: refs/heads/feature/flex-env-1.1.1
FLEX_GIT_SHA_SHORT: 6c1432f
FLEX_GIT_REF_SHORT: feature/flex-env-1.1.1
FLEX_GIT_REF_FORMAT: feature-flex-env-1-1-1
FLEX_GIT_TAG: v1.1.1
```
