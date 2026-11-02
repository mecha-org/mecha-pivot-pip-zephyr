# Mecha Pivot Pip - Zephyr Module

Zephyr module for the **Mecha Pivot Pip**, an analog pointing stick used by the Mecha Comet
keyboard and gamepad extensions. The driver reads the stick through two ADC channels and reports
it through the Zephyr input subsystem, either as relative motion (for a mouse pointer) or as an
absolute stick position (for a gamepad stick). The mode can be switched at run time. It works in
Zephyr applications and in ZMK.

It needs Zephyr 4.1 or newer and an ADC that reads two channels in one request, with a
resolution of 16 bits at most.

Full documentation is coming. Until then, the devicetree
[binding](dts/bindings/input/mecha,pivot-pip.yaml) describes every property, and
[`samples/pivot_pip`](samples/pivot_pip) shows the driver at work on `native_sim`.

## Installation

Add the module to the `west.yml` of your project, then run `west update`:

```yaml
manifest:
  projects:
    - name: mecha-pivot-pip
      url: https://github.com/mecha-org/mecha-pivot-pip-zephyr
      revision: main # use a tag or a commit in your project
      path: modules/lib/mecha-pivot-pip
```

## Development

This repository is also a west workspace for developing and testing the module on its own. You
need the host tools and the Zephyr SDK of the
[Zephyr Getting Started Guide](https://docs.zephyrproject.org/latest/develop/getting_started/index.html).
As in that guide, the Python packages go into a
[virtual environment](https://docs.python.org/3/library/venv.html), so they stay apart from your
system Python. Create the workspace, with the latest Zephyr release, and run the tests:

```sh
mkdir mecha-pivot-pip-ws
cd mecha-pivot-pip-ws
python3 -m venv .venv
source .venv/bin/activate
pip install west
west init -m https://github.com/mecha-org/mecha-pivot-pip-zephyr
west update
west packages pip --install
west zephyr-export
cd mecha-pivot-pip-zephyr
west twister -T tests -T samples --integration
```

To test with the Zephyr of ZMK or with Zephyr main, add `--mf west-zephyr-zmk.yml` or
`--mf west-zephyr-main.yml` to `west init`. If you already cloned the repository, run
`west init -l mecha-pivot-pip-zephyr` in the folder that holds the clone instead.

In every new terminal, activate the environment again with `source .venv/bin/activate` in the
workspace folder.

Licensed under the [BSD 3-Clause license](LICENSE).
