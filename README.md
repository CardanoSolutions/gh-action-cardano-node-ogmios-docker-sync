# `cardano-node-ogmios` Docker Sync GitHub Action
Use this action to sync an instance of `cardano-node-ogmios` into a cache to 
enable integration testing within a GitHub Workflow. As demonstrated in the 
[Ogmios repository](), the [network synchronization workflow]() synchronizes a testnet instance 
every six hours, which is then pushed to a cache used in the [continuous integration workflow]().


['Ogmios repository']: https://github.com/CardanoSolutions/ogmios
[network synchronization workflow]: https://github.com/CardanoSolutions/ogmios/blob/master/.github/workflows/network-synchronization.yaml
[continuous integration workflow]: https://github.com/CardanoSolutions/ogmios/blob/master/.github/workflows/continuous-integration.yaml