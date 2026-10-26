# malbec kernel integration

Set `opendroid_kernel_manifest` to a private selection manifest.

Manifest fields: `format_version: 1`, `state: selected`, and `files` entries with `role`, `path`, `sha256`, `destination`. Paths are relative to the manifest. Include one `kernel` and one `config`; optional roles are `module`, `dtb`, `dtbo`.

Modules install at `/vendor/lib/opendroid/<destination>`. `module-order.json` lists their init load order. Kernel options are checked against `device/soc/qualcomm/sm8735/kernel/requirements.json`.

`requirements.json` adds the board's built-in ramdisk and first-stage filesystem requirements to the shared SoC requirements.
