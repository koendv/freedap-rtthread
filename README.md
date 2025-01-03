[free-dap](https://github.com/ataradov/free-dap/) is a free and open source CMSIS-DAP debugger. This package is free-dap, running on the rt-thread operating system.

## installation

Add the freedap-rtthread git to the rt-thread packages by hand:

```
$ cd .env/packages/packages/
$ wget https://raw.githubusercontent.com/koendv/freedap-rtthread/refs/heads/main/patches/package.patch
$ patch -p1 < package.patch
patching file tools/Kconfig
patching file tools/freedap/Kconfig
patching file tools/freedap/package.json
```

In the project directory run `menuconfig`.

```
RT-Thread online packages  --->
    tools packages  --->
[*] freedap: firmware download tool  --->
```

then

```
$ pkgs --update
```

This downloads the freedap-rtthread package to your project.

## configuration

## Configuration

free-dap requires two configuration files. `dap_config.h` and `hal_config.h`. Copy from the `examples/` directory to the project directory.

The values of DAP_CONFIG_DELAY_CONSTANT and DAP_CONFIG_FAST_CLOCK are determined as follows. 

- at the rt-thread shell prompt, execute `swclk_test 1` and measure the frequency of the SWCLK pin. Set DAP_CONFIG_FAST_CLOCK to the frequency in Hz of the SWCLK pin.

- at the rt-thread shell prompt, execute `swclk_test 10000` and measure the frequency of the SWCLK pin. Repeat the `swclk_test` command with different values, until the frequency of the SWCLK pin is 1 kHz. Set DAP_CONFIG_DELAY_CONSTANT to the value that gives a SWCLK frequency of 1kHz.

## Use

- Set up USB for HID (CMSIS v1) or raw bulk (CMSIS v2)

- Call dap_init() at the initialization time

- Call dap_process_request() for every received request and send the response back
  
  
  
  See [at32f435-start](https://github.com/koendv/at32f435-start) for an implementation on at32f435.

## Links

- [free-dap git](https://github.com/ataradov/free-dap/)
