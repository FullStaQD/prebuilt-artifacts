# sim-hisepq

`sim_hisepq` is a compiled test bench from the [HiSEP-Q repo](https://github.com/caps-tum/HiSEP-Q-2.0). Usage

```shell
# Uses a $readmemh memory image as input.
./sim_hisepq +MEM_FILE=a.mem
```

## Provenance

- **Repo URL:** <https://github.com/caps-tum/HiSEP-Q-2.0>
- **Commit SHA:** encoded in asset
- **Date:** encoded in asset
- **Modified:** no

We use their provided build script to build the binary:

```shell
cd demo/verilator/
./run_verilator.sh --build-only
# produces ./obj_dir/sim_hisepq

# Use this command to prepare for release (update the `r1` manually suffix as needed):
name="sim-hisepq-$(git show -s --format=%cd --date=format:%Y%m%d HEAD)-g$(git rev-parse --short HEAD)-r1-linux-x86_64"
tar -C obj_dir/ -czf "$name.tar.gz" sim_hisepq
```

FIXME: Mention vivado toolchain.