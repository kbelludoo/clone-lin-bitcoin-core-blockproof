# clone-lin-bitcoin-core-blockproof

Experimental LIN clone of Bitcoin Core v27.1 **GetBlockProof** (compact nBits → chain work) plus **SetCompact**. This repository is the LIN copy.

Results and the machine-written proof harness live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) (`examples/bitcoin_blockproof/`, `test/prove_bitcoin_blockproof_external.py`).

## Upstream

- Repo: [bitcoin/bitcoin](https://github.com/bitcoin/bitcoin)
- Tag: `v27.1` commit `1088a98f5aad080cc6cca2da174f206509fcda6c`
- License: **MIT**
- `src/chain.cpp` sha256 `bbc1aa18b580d8a36ce7c416ee6cadee2c89686905912fc9a1edf6b3873992a5` blob `82007a8a1e7f38f7b02eb299f8fc30fc61fc190e`
- `src/arith_uint256.cpp` sha256 `b46d67db26cef11a9da125b98e29bd8bf77b7a5c71418ee63bb77a0125a09d06` blob `0d5b3d5b0e6476b88053bd74a35c5cdbef1d2ae8`
- `src/test/arith_uint256_tests.cpp` sha256 `6785d8cb5e70e731d81c61a32cf3cb5ca9cf4ac38ee66b26b0b8941570e1d6fe` blob `10028c7c9345ecd7804466e821c71fbc0a060b7c`

## Canonical vectors

| nBits | meaning | work (low) |
|---|---|---|
| `0x1d00ffff` | genesis / pow limit | `4295032833` = `0x100010001` |
| `0x1b0404cb` | first retarget | `70040908352512` |
| `0x20123456` | Core SetCompact hex vector | `14` |
| `0xff123456` | overflow | `0` |
| `0x01fedcba` | negative compact | `0` |

Class: **EXPERIMENTAL**. Not a Bitcoin node. Not SHA256d CheckProofOfWork.

## Reproduce (C11 oracle, no Zig)

```
gcc -O2 -std=c11 -o bitcoin_blockproof_c11 test/oracles/bitcoin_blockproof_c11.c
./bitcoin_blockproof_c11 selftest
./bitcoin_blockproof_c11 work 0x1d00ffff
```
