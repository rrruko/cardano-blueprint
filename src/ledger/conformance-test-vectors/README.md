vectors.tar.gz is a set of test vectors dumped from the cardano-ledger
conway-era test suite that can be used to test alternative ledger
implementations. Each vector consists of a sequence of transactions and a pair of "initial"
and "final" "NewEpochState" records.

Test vectors were obtained by running [this](https://github.com/SundaeSwap-finance/cardano-ledger-conformance-tests/commit/62058aaac7cdfbeec51fd2feee9c0b7ac7805ecb) fork of cardano-ledger:

```
git clone git@github.com:SundaeSwap-finance/cardano-ledger-conformance-tests.git
cd cardano-ledger-conformance-tests
git checkout 62058aaac7cdfbeec51fd2feee9c0b7ac7805ecb
cabal test cardano-ledger-conway
tar czf vectors.tar.gz eras/conway/impl/dump/*
```

Ledger V9 tests were removed, as well as two tests (BodyRefScriptsSizeTooBig,
TxRefScriptsSizeTooBig) that produced very large sequences of transactions
without a correspondingly significant impact on coverage.

To optimize the size of the vector set, the ledger state format is modified to
represent protocol parameters records by their hash. Each unique protocol parameters record can be found in the pparams-by-hash directory.

See also:
[this](https://github.com/IntersectMBO/cardano-ledger/issues/4892#issuecomment-2880444621)
discussion in the cardano-ledger repository.
