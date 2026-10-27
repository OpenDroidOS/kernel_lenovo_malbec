# Malbec kernel integration

`prebuilts.json` selects the ARM64 Linux 6.6.87 `prebuilt/Image` and its exact
embedded configuration, `prebuilt/kernel.config`.

From the OpenHarmony source root, prepare a selection outside the checkout:

```sh
python3 vendor/opendroid/common/scripts/stage_kernel.py --prepare \
  --manifest kernel/lenovo/malbec/prebuilts.json \
  --requirements device/soc/qualcomm/sm8735/kernel/requirements.json \
  --additional-requirements kernel/lenovo/malbec/requirements.json \
  --module-order kernel/lenovo/malbec/module-order.json \
  --output /path/to/work/kernel-selection.json
```

Pass that file as the GN argument `opendroid_kernel_selection`. Prepare a new
selection after changing inputs or their paths. Staging verifies file hashes
and kernel requirements. Editing the saved config does not change the Image.

Optional `module`, `dtb` and `dtbo` entries use paths relative to the manifest.
Modules install under `/vendor/lib/opendroid/<destination>`; list their init
load order in `module-order.json`.

The kernel's [corresponding source](https://android.googlesource.com/kernel/common/+/c2569c3b141cb39a6c2bca63c62697589fe86dc4)
is licensed under GPL-2.0 WITH Linux-syscall-note; license texts are retained
under `prebuilt/`. Original OpenDroidOS integration files use Apache-2.0.
