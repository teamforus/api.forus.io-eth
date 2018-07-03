# API Kindpakket Ethereum service

This service implements the Ethereum part of Kindpakket Zuidhorn. 

## Running this image on docker

Building: `docker build --rm -f api\Dockerfile -t ethereum-api:latest api`

Running: `docker run --name <NAME> --rm -p <PORT>:80 -d ethereum-api` (e.g. `docker run --name ethereum-api --rm -p 3000:80 -d ethereum-api`)

### Configuration

The app requires a `config.json`. An example is found in `config.json.example`, although it misses certain data. 

### `coinbaseAddress`

The address of the coinbase (which has the Ether to make transactions)

### `coinbasePassword`

Used to unlock the coinbase account.

### `connectionString`

The string with URL and port number to connect to an Ethereum node

### `kindpakketTokenAddress` 

The address of the Kindpakket Token contract.

## Usage

This PoC uses a HTTP connection to interact.

### `/v1/api/balance` (GET)

Get the balance of an address. Requires a JSON body with `address` key-value, based on Ethereum addresses.

Expected results: JSON response with `"balance"` integer value and/or `"success"` boolean value, representing whether the call was successful or not. If the call was not successful, the `"balance"` is absent or not reliable. 

### `/v1/api/transfer` (POST)

Make a transaction. Requires a JSON body with `"from"` address string, `"to"` address string, `"amount"` integer and `"requester"` identifier.

Expected results: JSON result with `"success"` with a value of `true` or `false` if the code ran successfully and an optional `"message"` response with human-readable response.

Note that `"success"` can be true, but that does not mean that the transaction in the smart contract was successful. 