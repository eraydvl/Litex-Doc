# Litex-Doc

## LiteX Setup

1. Install Python 3.6+ and FPGA vendor's development tools
2. Instal Migen and LLiteX and the Litex's cores:
  ```
wget https://raw.githubusercontent.com/enjoy-digital/litex/master/litex_setup.py
chmod +x litex_setup.py
./litex_setup.py --init --install --user
```
3. Update Litex:
```
./litex_setup.py --update
```
4. Install a RISC-V toolchain (Only if you want to test/create a SoC with a CPU):
```
pip3 install meson ninja
./litex_setup.py --gcc=riscv
```
5. Build the target of your board:
```
python3 -m litex-boards.litex_boards.targets.<your_boards> --build
```
6. Test LiteX directly on your computer without any FPGA board:
```
sudo apt install libevent-dev libjson-c-dev verilator
litex_sim --cpu-type=vexriscv
```
7. RISC-V toolchain:
```
wget https://static.dev.sifive.com/dev-tools/riscv64-unknown-elf-gcc-8.1.0-2019.01.0-x86_64-linux-ubuntu14.tar.gz
tar -xvf riscv64-unknown-elf-gcc-8.1.0-2019.01.0-x86_64-linux-ubuntu14.tar.gz
export PATH=$PATH:$PWD/riscv64-unknown-elf-gcc-8.1.0-2019.01.0-x86_64-linux-ubuntu14/bin/
```
   

## LiteX Build Command
LiteX has command list:
```
Target options:
  --toolchain {quartus}
          FPGA toolchain (quartus). (default: quartus)
  --build
          Build design. (default: False)
  --load  Load bitstream. (default: False)
  --sys-clk-freq SYS_CLK_FREQ
          System clock frequency. (default: 50000000.0)
  --with-led-chaser
          Enable LED chaser. (default: False)
  --with-sdcard
          Enable SD card support. (default: False)
  --with-ethernet
          Enable Ethernet support. (default: False)
  --with-etherbone
          Enable Etherbone support. (default: False)
  --etherbone-ip ETHERBONE_IP
          Etherbone IP address. (default: 192.168.48.100)
  --etherbone-phy ETHERBONE_PHY
          Etherbone PHY (0 or 1). (default: 1)
  --ethernet-phy ETHERNET_PHY
          Ethernet PHY (0 or 1). (default: 0)

Logging options:
  --log-filename LOG_FILENAME
          Logging filename. (default: None)
  --log-level LOG_LEVEL
          Logging level: debug, info (default), warning error or critical. (default: info)

Builder options:
  --output-dir OUTPUT_DIR
          Base Output directory. (default: None)
  --gateware-dir GATEWARE_DIR
          Output directory for Gateware files. (default: None)
  --software-dir SOFTWARE_DIR
          Output directory for Software files. (default: None)
  --include-dir INCLUDE_DIR
          Output directory for Header files. (default: None)
  --generated-dir GENERATED_DIR
          Output directory for Generated files. (default: None)
  --build-backend BUILD_BACKEND
          Select build backend: litex or edalize. (default: litex)
  --no-compile
          Disable Software and Gateware compilation. (default: False)
  --no-compile-software
          Disable Software compilation only. (default: False)
  --no-compile-gateware
          Disable Gateware compilation only. (default: False)
  --soc-csv SOC_CSV, --csr-csv SOC_CSV
          Write SoC mapping to the specified CSV file. (default: None)
  --soc-json SOC_JSON, --csr-json SOC_JSON
          Write SoC mapping to the specified JSON file. (default: None)
  --soc-svd SOC_SVD, --csr-svd SOC_SVD
          Write SoC mapping to the specified SVD file. (default: None)
  --memory-x MEMORY_X
          Write SoC Memory Regions to the specified Memory-X file. (default: None)
  --doc   Generate SoC Documentation. (default: False)

BIOS options:
  --bios-lto
          Enable BIOS LTO (Link Time Optimization) compilation. (default: False)
  --bios-format {integer,float,double}
          Select BIOS printf format. (default: integer)
  --bios-console {full,no-history,no-autocomplete,lite,disable}
          Select BIOS console config. (default: full)

SoC options:
  --bus-standard BUS_STANDARD
          Select bus standard: wishbone, axi-lite, axi. (default: wishbone)
  --bus-data-width BUS_DATA_WIDTH
          Bus data-width. (default: 32)
  --bus-address-width BUS_ADDRESS_WIDTH
          Bus address-width. (default: 32)
  --bus-timeout BUS_TIMEOUT
          Bus timeout in cycles. (default: 1000000)
  --bus-bursting
          Enable burst cycles on the bus if supported. (default: False)
  --bus-interconnect BUS_INTERCONNECT
          Select bus interconnect: shared (default) or crossbar. (default: shared)
  --cpu-type CPU_TYPE
          Select CPU: None, cva6, gowin_emcu, mor1kx, ibex, cva5, microwatt, marocchino, kianv, vexriscv, cv32e40p,
          zynq7000, naxriscv, eos_s3, rocket, minerva, zynqmp, femtorv, cortex_m3, firev, vexriscv_smp, cortex_m1,
          cv32e41p, openc906, neorv32, serv, blackparrot, lm32, picorv32. (default: vexriscv)
  --cpu-variant CPU_VARIANT
          CPU variant. (default: None)
  --cpu-reset-address CPU_RESET_ADDRESS
          CPU reset address (Boot from Integrated ROM by default). (default: None)
  --cpu-cfu CPU_CFU
          Optional CPU CFU file/instance to add to the CPU. (default: None)
  --no-ctrl
          Disable Controller. (default: False)
  --integrated-rom-size INTEGRATED_ROM_SIZE
          Size/Enable the integrated (BIOS) ROM (Automatically resized to BIOS size when smaller). (default: 131072)
  --integrated-rom-init INTEGRATED_ROM_INIT
          Integrated ROM binary initialization file (override the BIOS when specified). (default: None)
  --integrated-sram-size INTEGRATED_SRAM_SIZE
          Size/Enable the integrated SRAM. (default: 8192)
  --integrated-main-ram-size INTEGRATED_MAIN_RAM_SIZE
          size/enable the integrated main RAM. (default: None)
  --csr-data-width CSR_DATA_WIDTH
          CSR bus data-width (8 or 32). (default: 32)
  --csr-address-width CSR_ADDRESS_WIDTH
          CSR bus address-width. (default: 14)
  --csr-paging CSR_PAGING
          CSR bus paging. (default: 2048)
  --csr-ordering CSR_ORDERING
          CSR registers ordering (big or little). (default: big)
  --ident IDENT
          SoC identifier. (default: None)
  --no-ident-version
          Disable date/time in SoC identifier. (default: False)
  --no-uart
          Disable UART. (default: False)
  --uart-name UART_NAME
          UART type/name. (default: serial)
  --uart-baudrate UART_BAUDRATE
          UART baudrate. (default: 115200)
  --uart-fifo-depth UART_FIFO_DEPTH
          UART FIFO depth. (default: 16)
  --with-uartbone
          Enable UARTbone. (default: False)
  --with-jtagbone
          Enable Jtagbone support. (default: False)
  --jtagbone-chain JTAGBONE_CHAIN
          Jtagbone chain index. (default: 1)
  --no-timer
          Disable Timer. (default: False)
  --timer-uptime
          Add an uptime capability to Timer. (default: False)
  --l2-size L2_SIZE
          L2 cache size. (default: 8192)
```

## LiteX Simulator
We need setup for simulation area (I dont install):
```
sudo apt install verilator
sudo apt install libevent-dev libjson-c-dev
```

## Setup OpenOCD
only needed for hardware test:
```
sudo apt install libtool automake pkg-config libusb-1.0-0-dev
git clone https://github.com/ntfreak/openocd.git
cd openocd
./bootstrap
./configure --enable-ftdi
make
sudo make install
```

## Running on Hardware
Our board add `./make.py` list:
```
# DE2-115 support ----------------------------------------------------------------------------------
class terasic_de2_115(Board):
    soc_kwargs = {
        "l2_size" : 2048          # Use Wishbone and L2 for memory accesses.
    }
    def __init__(self):
        from litex_boards.targets import de2_115
        Board.__init__(self, de2_115.BaseSoC, soc_capabilities={
            # Communication
            "serial"
            #"ethernet",
            # GPIOs
            #"leds",
            # Video, video_terminal
            #"framebuffer"
        })#, bitstream_ext=".sof"
```
```
supported_boards = {
     # Altera/Intel
     "de0nano":         De0Nano,
     "de10nano":        De10Nano,
     "terasic_de2_115":          terasic_de2_115,
     "qmtech_ep4ce15":  Qmtech_EP4CE15,
 }
```
`.sof` desteği sonradan yapılacak
yukarıdaki parentez içindeki elemanlardan şuan sadece led ve serail desteklenmektedir. Diğer istenilen eleman destekleri için `litex-boards.litex_boards.targets.<your_boards>` düzenlenmesi gerekmektedir.

Once installed, build the bitstream with:
```
./make.py --board=XXYY --cpu-count=X --build
```

later load:
```
./make.py --board=XXYY --cpu-count=X --load
```

hangi serialin bağlı olduğuna bakmak için `lsusb` komutu kullanılmalı. Kullanılan usb port ile:
```
sudo chmod 777 /dev/ttyUSB0
sudo litex_term --images=images/boot.json /dev/ttyUSB0
```

