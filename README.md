# BIM-chain

## Blockchain & Tokens

TBD

- [ ] Property token
- [ ] Possession token

## Data layer exercises

The following is a short excercise on how to put data onto ipfs and retrieve it again.
The idea is to put the reference (ipfs hash) to this data somewhere onto the blockchain and given that reference, retrieve the data from anywhere.

Precondition (installation instructions for ubuntu):
* ipfs (data layer technology) installed & running. `sudo snap install ipfs && ipfs init && ipfs daemon`
* jq (data extraction tool for JSON) installed. `sudo apt install jq`

## prepare, publish data & save reference hash
> split 5 objects and save the first in data.json
1. `jq '.[0]' test/mocks/5objects.json  > data.json`
> add the data to ipfs, which returns a hash to retrieve the data from the network later, (which we will save in a database/blockchain)
2. `ipfs add data.json`
> save the reference that was output (Qme... is the format of your ipfs hash)
3. `echo Qme5GawkhEceihJYYccGPvK5MzatwcAifa85qhNmMowcb2 > ref`

## prepare, publish data & save reference hash (alternative command)
> Alternatively you can do 1, 2 & 3 in 1 command like this:
1. `jq '.[0]' test/mocks/5objects.json | ipfs add - | awk '{ print $NF }' > ref`

## fetch data & extract a value
> get the data from data layer back, e.g. cpi property
1. ```ipfs cat `cat ref` | jq '.cpi'```

## download data from ipfs
```bash
ipfs deamon
ipfs cat Qme5GawkhEceihJYYccGPvK5MzatwcAifa85qhNmMowcb2 > data/block1.json
```
