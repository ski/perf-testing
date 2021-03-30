# Agoric SDK Artillery Performance Testing

TL;DR:

Install (Artillery)[https://artillery.io/]

```sh
yarn global add artillery
cd perf-testing
# Start the Agoric platform
agoric install && agoric start --reset
```

Install the testing dapp and stary ag-solo

```sh
cd perf-testing
# Start the Agoric platform
agoric install && agoric start --reset
```

In a second terminal, deploy this contract and the API server

```sh
agoric deploy contract/deploy.js
agoric deploy api/deploy.js
```

In a third terminal run the tests,

```sh
# Navigate to the `ui` directory and start a local server
cd ui
# runs the tests and saves the data in report.json
artillery run tests/zoe.yaml --output zoe-result.json
```

After the test is run, generate the test report in the ui directory

```sh
# runs the tests and saves the data in report.json
artillery report zoe-result.json
```

This will generate zoe-result.json.html in the current directory which you
should be able to open in your browser of choice.

# Zoe Contract installation scenario.

The test can be found under tests/zoe.yaml. The test runs for 1 minute
with one virutal user added every second.

The first scenario tests the "test/install" operation on the dapp API.
This operation installs the secondPriceAuctionSource zoe contract and
returns. The first scenario in the test invokes this operation and then
'thinks' for 4 seconds during which time the connection is held open.
