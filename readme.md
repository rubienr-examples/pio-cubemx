# Introduction

This is an example project to illustrate a simplified workflow of `PlatoformIO` in combination with `stm32pio`.
Either check this repository out and proceed working on top or follow the subsequent steps.

## Example Workflow

1. optional: modify user code
2. optional: modify cubemx.ioc with STM32CubeMX if necessary
   1. auto generate CubeMX code: `stm32pio generate` 
4. run tests: `pio test ` **(TODO: introduce and configure test fw.; add exmaple for both: native and µC testing)**
5. build and run: `pio run --target upload`
6. return to step 1.

## Step by Step

The following steps use Poetry to install required packages and set up the environment.
Poetry is not a must but rather for convenience.
All steps can be achieved manually without Poetry: develop, build, flash, generate documentation.

1. Prerequisites
   ```bash
   mkdir foo-project && cd foo-project
   poetry init
   # ...
   poetry shell
   
   poetry add platformio
   poetry add stm32pio
   ```
2. Initialize the PlatformIO project:
   ```bash
   pio init --ide clion
   # optional: adjust platformio.ini
   ```
3. Install [CubeMx](https://www.st.com/en/development-tools/stm32cubemx.html)
   1. example installation directory: /home/user_foo/cubemx/current/
4. Initialize `stm32pio`:
   ```bash
   stm32pio init --board blackpill_f401cc
   
   # in the newly created stm32pio.ini ensure the `cubemx_cmd` command points to the CubeMX binary
   # stm32pio.ini:
   #
   # [app]
   # platformio_cmd = platformio
   # cubemx_cmd = /home/user_foo/cubemx/current/STM32CubeMX
   # java_cmd = None
   
   # auto generate CubeMX code
   stm32pio generate
   ```
5. Workflow
   ```bash
   # modify user code ...
   
   # adjust cubemx.ioc with STM32CubeMX ...
   
   # auto generate CubeMX code
   stm32pio generate
   
   # compile and upload to controller
   pio run --target upload
   ```

## References

1. [stm32pio](https://github.com/ussserrr/stm32pio)
2. [CubeMx](https://www.st.com/en/development-tools/stm32cubemx.html)
