## RocksDB utilizing Tiered Storage and Hybrid Compression
This work is a scheme utilizing RocksDB, allowing users to store each of the levels of RocksDB into heterogeneous storage media and decide which compression technique they want to use on those levels.

### Dependencies
- Tiered Storage
```
This scheme can be used with the storage devices on the user machine with no customizations since the changes we made are limited to the application level.
```
- Hybrid Compression
```
The following compression libraries should be linked. In case they aren't, they cannot be used in setting up the hybrid compression within levels and no compression will be used by default.
```

### Compilation

```
Compile the code with the same options as compiling RocksDB: 
https://github.com/facebook/rocksdb/blob/main/INSTALL.md

```
