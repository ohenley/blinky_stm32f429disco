## blinky_stm32f429disco
Flashing LEDs (LD3, LD4) on the stm32f429 discovery board. 

### Prerequesite (tested on linux ubuntu 20.04 only)

#### Alire: https://github.com/alire-project/alire/releases
- Download and unzip the latest linux zip
- Add `where_you_unzipped/alr` to [PATH](https://phoenixnap.com/kb/linux-add-to-path)  
- Verify Alire is found on your path. 
```console   
which alr
```

#### OpenOCD
```console
sudo apt install openocd
```

#### STM32f429 Discovery board
![stm32f429disco](https://raw.githubusercontent.com/wolfbiters/blinky_stm32f429disco/main/stm32f429disco.jpg)   
- Plug it to your computer using the [USB MIN B cable](https://www.reviewgeek.com/53587/usb-explained-all-the-different-types-and-what-theyre-used-for/)

### Add custom Alire index (IMPORTANT)
The chain of crates used by this project is a breaking reorganization of files found in [Ada_Bare_Metal_Demos](https://github.com/lambourg/Ada_Bare_Metal_Demos) and [Ada_Drivers_Library](https://github.com/AdaCore/Ada_Drivers_Library).

- I moved the type definitions found in `hal.ads` to `beta_types.ads` and gave it its own crate. Conceptually I disliked to depend on the Hardware Abstraction Layer package for 'C like' types that are actually used "under" the HAL conceptual layer.
- I decided to parameterize `core` in the **arm_cortex** crate and `board`, `mcu`, `runtime` configuration variables in the root **stm32_config** crate.

Install my forked Alire index named `testindex` locally:
```
alr index --add git+https://github.com/ohenley/alire-index.git#stable-1.2.1 --name testindex
```

When you are done, you can delete it:
```
alr index --del testindex
```

### Fetch 
```console
alr get blinky_stm32f429disco
cd blinky*
```  

### Build (Visual Studio Code)
```console
alr build
```

### Build (GnatStudio)
```console
eval "$(alr printenv)"
gprbuild blinky_stm32f429disco.gpr
gnatstudio blinky_stm32f429disco.gpr
```

### Run

```console
openocd -f /usr/local/share/openocd/scripts/board/stm32f429disc1.cfg -c 'program bin/blinky verify reset exit'
```    
You should see the board LEDs (LD3, LD4) flashing at 1Hz.
