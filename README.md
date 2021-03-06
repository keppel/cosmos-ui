# cosmos-ui

> Human interface to Cosmos. Links to binary downloads coming soon.

## Warning

This is still alpha-level software as of September 2017. Do not enter in your Cosmos fundraiser seed.

## Development

To run the dev build, first you will need the following binaries installed in your GOPATH: `basecoin`, `baseserver`, and `tendermint`.

```
npm install
npm run dev
```

This should launch the app, running on a local testnet.

## Production

You can create production builds to get an app which will connect to an actual blockchain network.

First you will need the prerequisite source repositories installed:

```bash
# install basecoin/baseserver
go get github.com/cosmos/cosmos-sdk
cd $GOPATH/src/github.com/cosmos/cosmos-sdk
git checkout develop
make get_vendor_deps
make install

# install tendermint
go get github.com/tendermint/tendermint
cd $GOPATH/src/github.com/tendermint/tendermint
git checkout v0.11.0
make get_vendor_deps
make install
```

```fish
# check your versions
$ basecoin version
v0.7.0-alpha f40fa5b
$ basecli version
v0.7.0-alpha f40fa5b
$ tendermint version
0.11.0-7682ad9a
```

Then build and run the app:
```bash
npm run pack && npm run build:darwin
open builds/cosmos-ui-darwin-x64/cosmos-ui.app
```
