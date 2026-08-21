# sim-hisepq

`sim_hisepq` is a compiled Verilator test bench from the [HiSEP-Q 2.0
repo](https://github.com/caps-tum/HiSEP-Q-2.0), packaged here so that running
the tests doesn't require Verilator ≥ 5.

Unlike `demo/run.sh`, which drives the same test bench under Vivado, this
binary is self-contained and needs no Xilinx tooling at runtime. Usage:

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

Requires Verilator. Run from a clean HiSEP-Q checkout, here assuming a
linux-x86_64 host. Prefer the Verilator version recorded in the previous
release's notes; a different version is a configuration change, so bump the
`r` suffix.

```shell
cd demo/verilator/
./run_verilator.sh --build-only        # produces ./obj_dir/sim_hisepq

# Manually bump the r1 suffix when rebuilding the same commit with a different
# configuration.
tag="sim-hisepq-$(git show -s --format=%cd --date=format:%Y%m%d HEAD)-g$(git rev-parse --short HEAD)-r1"
name="$tag-linux-x86_64"
tar -C obj_dir/ -czf "$name.tar.gz" sim_hisepq
```

Create a release like so — run inside this repo, at the correct commit (likely on `main`):

```shell
tag=...  # as above
name=... # as above

# Create a draft release (document build env in notes.md):
gh release create "$tag" --draft --title "$tag" --notes-file notes.md "$name.tar.gz"

# Iterate ... e.g. update notes:
gh release edit "$tag" --notes-file notes.md

# Publish (important: need to be on right commit, makes a git tag):
gh release edit "$tag" --draft=false
```