# sim-hisepq

`sim_hisepq` is a compiled test bench from the [HiSEP-Q repo](https://github.com/caps-tum/HiSEP-Q-2.0). Usage

```shell
# Uses a $readmemh memory image as input.
./sim_hisepq +MEM_FILE=a.mem
```

## Provenance

- **Repo URL:** <https://github.com/caps-tum/HiSEP-Q-2.0>
- **Commit SHA:** `817e42e07feaf6dd8acc783b7ff6c55c9c775c08`
- **Date:** `2026-06-19`
- **Modified:** no

We use their provided build script to build the binary:

```shell
cd demo/
./verilator/run_verilator.sh --build-only
# produces verilator/obj_dir/sim_hisepq
```

FIXME: Mention vivado toolchain.