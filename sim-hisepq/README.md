# sim-hisepq

`sim_hisepq` is a compiled Verilator test bench from the [HiSEP-Q 2.0
repo](https://github.com/caps-tum/HiSEP-Q-2.0), packaged here so that running
the tests doesn't require Verilator ≥ 5.

The binary itself has no Xilinx or Vivado runtime dependency.

```shell
# Uses a $readmemh memory image as input.
./sim_hisepq +MEM_FILE=a.mem
```

Licensed Apache-2.0 — see [LICENSE](LICENSE).

## Provenance

- **Repo:** <https://github.com/caps-tum/HiSEP-Q-2.0>
- **Modified:** no

Upstream commit SHA and date are encoded in each asset filename; the exact
Verilator version used and other relevant environment aspects are recorded in
the corresponding release notes.

## Building a release

Requires Verilator. Run from a clean HiSEP-Q checkout, here assuming on
linux-86_64 host:

```shell
cd demo/verilator/
./run_verilator.sh --build-only        # produces ./obj_dir/sim_hisepq

# Manually bump the r1 suffix if rebuilding the same commit with a different
# configuration.
tag="sim-hisepq-$(git show -s --format=%cd --date=format:%Y%m%d HEAD)-g$(git rev-parse --short HEAD)-r1"
name="$tag-linux-x86_64"
tar -C obj_dir/ -czf "$name.tar.gz" sim_hisepq
```

Create a release like so:

```shell
# Create a draft release:
gh release create "$tag" --draft --title "$tag" --notes-file notes.md "$name.tar.gz"

# iterate ... e.g. notes on build environment:
gh release edit "$tag" --notes-file notes.md

# Publish:
gh release edit "$tag" --draft=false
```