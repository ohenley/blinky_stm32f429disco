## Blinky_stm32f429disco

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

#### STM32f429 board
- Plug it to your computer using the [USB MIN B cable](https://www.reviewgeek.com/53587/usb-explained-all-the-different-types-and-what-theyre-used-for/)
![stm32f429disco](https://raw.githubusercontent.com/wolfbiters/blinky_stm32f429disco/main/stm32f429disco.jpg)

### Build
```console
alr get blinky_stm32f429disco    
cd blinky*
alr build
```  

### Run

```console
openocd -f /usr/local/share/openocd/scripts/board/stm32f429disc1.cfg -c 'program bin/blinky verify reset exit'
```
