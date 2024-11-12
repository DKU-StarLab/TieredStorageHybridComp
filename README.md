## RocksDB utilizing Tiered Storage and Hybrid Compression
This work is a scheme utilizing RocksDB, allowing users to store each of the levels of RocksDB into heterogeneous storage media and decide which compression technique they want to use on those levels.

### Download
```
git clone --recurse-submodules  https://github.com/DKU-StarLab/TieredStorageHybridComp.git
```

### Dependencies
- Tiered Storage: This scheme can be used with the storage devices on the user machine with no customizations since the changes we made are limited to the application level.
- Hybrid Compression: The following compression libraries should be linked. In case they aren't, they cannot be used in setting up the hybrid compression within levels and no compression will be used by default.
  - Snappy: https://google.github.io/snappy/
  - LZ4: https://github.com/lz4/lz4
  - Zstd: https://facebook.github.io/zstd/
  - zlib: http://www.zlib.net/

### Compilation
```
Compile the code with the same options as compiling RocksDB: 
https://github.com/facebook/rocksdb/blob/main/INSTALL.md

```

### Benchmarking

- Setting up tiered storage
  1. Create directories to hold the levels of the LSM-tree in their corresponding storage device.
  1. Using the db_bench tool, specify the flags needed for tiered storage.
- Run benchmark with db_bench using the flags for tiered storage along with other db_bench options
  - use_tiered_storage - [default:0] [Possible values: 0 or 1]Boolean value which tells the LSM-tree if tiered storage will be used or not.
  - tiered_storage_path - [default:empty] [Possible values: STRING] String value of the comma-separated storage paths.

```
Example:
Storage paths:
- /mnt/ssdoptane
- /mnt/ssdnvme
- /mnt/ssdsata
- /mnt/hdd

Run db_bench with flags use_tiered_storage and tiered_storage_path
./db_bench --benchmarks=fillrandom --use_tiered_storage=1 --tiered_storage_path=/mnt/ssdoptane,/mnt/ssdnvme,/mnt/ssdsata
```
This benchmark will store L0 in "/mnt/ssdoptane", L1 in "/mnt/ssdnvme", L2 in "/mnt/ssdsata", and the rest of the levels (L3 onwards) in "/mnt/hdd"