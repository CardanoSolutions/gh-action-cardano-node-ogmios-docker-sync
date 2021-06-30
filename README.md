# `cardano-node-ogmios` Docker Sync GitHub Action
Use this action to sync an instance of `cardano-node-ogmios` into a cache to 
enable integration testing within a GitHub Workflow. As demonstrated in the 
[Ogmios repository](), the [network synchronization workflow]() synchronizes a testnet instance 
every six hours, which is then pushed to a cache used in the [continuous integration workflow]().


['Ogmios repository']: https://github.com/CardanoSolutions/ogmios
[network synchronization workflow]: https://github.com/CardanoSolutions/ogmios/blob/master/.github/workflows/network-synchronization.yaml
[continuous integration workflow]: https://github.com/CardanoSolutions/ogmios/blob/master/.github/workflows/continuous-integration.yaml

# Usage

see [action.yml](https://github.com/CardanoSolutions/gh-action-cardano-node-ogmios-docker-sync/blob/master/action.yml) for all possible options.


## Basic 

Be aware that this will do a full resync on every run. 

```yaml
steps:
- uses: actions/checkout@v2

- uses: CardanoSolutions/cardano-node-ogmios-docker-sync@v1
```

## With cache and multiple networks

```yaml
strategy:
  matrix:
    network: [ testnet, mainnet ]

steps:
- uses: actions/checkout@v2

- id: date
  shell: bash
  run: |
      echo "::set-output name=value::$(/bin/date -u "+%Y%m%d")"

- uses: actions/cache@v2
  with:
    path: ${{ runner.temp }}/db
    key: cardano-node-${{ matrix.network }}-${{ steps.date.outputs.value }}
    restore-keys: |
      cardano-node-${{ matrix.network }}

- uses: CardanoSolutions/cardano-node-ogmios-docker-sync@v1
  with:
    db-dir: ${{ runner.temp }}/db
    network: ${{ matrix.network }}
```
