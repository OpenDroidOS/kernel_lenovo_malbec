# malbec kernel integration

Keep local manifests, payloads and prepared selections under `private/`, which
is ignored by Git. Paths outside the repository are also accepted.

Prepare a private GN selection from the source root:

```sh
python3 vendor/opendroid/common/scripts/stage_kernel.py --prepare \
  --manifest /path/to/private/prebuilts.json \
  --requirements device/soc/qualcomm/sm8735/kernel/requirements.json \
  --additional-requirements kernel/lenovo/malbec/requirements.json \
  --module-order kernel/lenovo/malbec/module-order.json \
  --output /path/to/private/selection.json
```

Set `opendroid_kernel_selection` to the prepared file. Use a new output path
when the manifest, requirements, module order or source paths change.

The input manifest has `format_version: 1`, `state: selected`, and `files`
entries with `role`, `path`, `sha256`, `destination`. Paths are relative to the
manifest. Include one `kernel` and one `config`; optional roles are `module`,
`dtb`, `dtbo`.

Staging rechecks the prepared description, payload hashes and kernel options.
Modules install at `/vendor/lib/opendroid/<destination>`. `module-order.json`
lists their init load order; module dependencies and ABI need a matching set.

`requirements.json` adds the board's built-in ramdisk and first-stage filesystem requirements to the shared SoC requirements.
