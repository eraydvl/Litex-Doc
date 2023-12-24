# Litex-Doc

[English](README.md)
[Türkçe](README-tr.md)

<details>
<summary>Bağımlılıklar</summary>

## Bağımlılıklar
|Araçlar|Sürüm|
|:---|:---|
|İşletim sistemi|Ubuntu 22.04
|git|2.34.1|
|Python|3.10.12|
|quartus|Quartus (Quartus Prime 22.1std) Lite Edition|
|litex|master-branch|
|Verilator|Verilator 4.038|
|meson|1.3.0|
|ninja|1.11.1.git.kitware.jobserver|
|gcc|riscv64-unknown-elf-gcc-8.1.0|
|OpenOCD|0.12.0|
|SBT|1.9.8|
|java-jdk|openjdk-8-jdk|

</details>

## LiteX Kurulumu
LiteXi kurmak istediğiniz dizine `mkdir LiteX` komutunu verdikten sonra `cd LiteX` komutunu kullanın ve aşağıdaki adımları uygulayın.
1. Python 3.6+ ve FPGA tedarikçisinin geliştirme araçlarını yükleyin
2. Migen ve LLiteX'i ve Litex'in çekirdeklerini yükleyin:
LiteX dizininde bulunulmalıdır.
```
wget https://raw.githubusercontent.com/enjoy-digital/litex/master/litex_setup.py
chmod +x litex_setup.py
./litex_setup.py --init --install --user
```
> Litex'i güncelleyin:`update` komutunu kullanın. LiteX dizininde bulunulmalıdır. 
```
sudo ./litex_setup.py --update
```

3. Bir RISC-V araç zinciri yükleyin:

    Yalnızca bir CPU ile bir SoC test etmek/oluşturmak istiyorsanız, LiteX dizininde bulunulmalıdır.
```
pip3 install meson ninja
./litex_setup.py --gcc=riscv
```

4. Kartınızın hedefini oluşturun:

    Yazılması gereken komut aşağıdadır, LiteX dizininde bulunulmalıdır. Eğer değilse, `litex-boards.litex_boards.targets.<your_boards>` dosyasını düzenlemeniz gerekir.
```
python3 -m litex-boards.litex_boards.targets.<your_boards> --build
```
5. LiteX'i herhangi bir FPGA kartı olmadan doğrudan bilgisayarınızda test edin:

    Test için gerekli dosya yapılarını indirmek için kod sağlanmıştır.

    Diğer kod ise simülasyonu başlatmak için gerekli kod ve hangi işlemcinin kullanılacağı ile ilgili bilgilerdir. LiteX dizininde bulunulmalıdır.
```
sudo apt install libevent-dev libjson-c-dev verilator
litex_sim --cpu-type=vexriscv
```

6. RISC-V toolchain:
```
wget https://static.dev.sifive.com/dev-tools/riscv64-unknown-elf-gcc-8.1.0-2019.01.0-x86_64-linux-ubuntu14.tar.gz
tar -xvf riscv64-unknown-elf-gcc-8.1.0-2019.01.0-x86_64-linux-ubuntu14.tar.gz
export PATH=$PATH:$PWD/riscv64-unknown-elf-gcc-8.1.0-2019.01.0-x86_64-linux-ubuntu14/bin/
```
Yukarıdaki adımlardan sonra dizinin son hali aşağıdaki resimde gösterildiği gibidir:

![LiteX located image](https://github.com/eraydvl/Litex-Doc/blob/main/litex_located.png)

<details>
<summary>LiteX İnşa Komutları</summary>

İnşa etmek için kullanılabilecek komutlar:

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

</details>

## LiteX Simülasyon
Bize simülasyon için alan gerekli:
```
sudo apt install verilator
sudo apt install libevent-dev libjson-c-dev
```

## OpenOCD Kurulumu

Donanım üzerinde test için gereksinimler:
```
sudo apt install libtool automake pkg-config libusb-1.0-0-dev
git clone https://github.com/ntfreak/openocd.git
cd openocd
./bootstrap
./configure --enable-ftdi
make
sudo make install
```
Yukarıdaki adımlar bittikten sonra dosyanın genel görüntüsü aşağıdaki resim gibi olmalıdır:

![OpenOCD located image](https://github.com/eraydvl/Litex-Doc/blob/main/images/openOCD.png)

## Donanım Üzerinde Çalışma
Sahip olduğunuz kart `./make.py` dosyası tarafından desteklenmiyorsa, kartınızı oluşturduğunuz özelliklere göre kendi `--boards` argümanınızı ekleyebilirsiniz. 

Elimdeki Terasic DE2 115 kartı için destek olmadığı için `./make.py` dosyasına aşağıdaki komutları ekledim.

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
     "terasic_de2_115": terasic_de2_115,
     "qmtech_ep4ce15":  Qmtech_EP4CE15,
 }
```

`.sof` desteği daha sonra yapılacaktır.

Yukarıdaki parantez içindeki elemanlardan şu anda sadece led ve seri iletişim desteklenmektedir. Diğer istenen eleman destekleri için `litex-boards.litex_boards.targets.<your_boards>` dosyasının düzenlenmesi gerekiyor.

Linux için olanı yandaki linkten indirip `/images` klasörüne atılmalıdır.
https://github.com/litex-hub/linux-on-litex-vexriscv/issues/164

Yukarıdaki adımların tümü başarıyla tamamlandıysa, donanım üzerinde çalışacak yazılımı oluşturmak ve kurmak için aşağıdaki adımlar izlenmelidir.
İle bit akışını oluşturun:

```
./make.py --board=terasic_de2_115 --cpu-count=1 --build
```
Eğer inşa başarıyla sonuçlandıysa aşağıdaki komutu kullanın: 
```
./make.py --board=terasic_de2_115 --cpu-count=1 --load
```

Hangi serinin bağlı olduğunu görmek için `lsusb` komutunu kullanın. Kullanılan usb portu ile:
```
sudo chmod 777 /dev/ttyUSBX
litex_term --images=images/boot.json /dev/ttyUSBX
```

Yukarıdaki adımların tümü başarıyla tamamlandıysa, son ekran görüntüsü aşağıdaki resimdeki gibi görünmelidir:

![litex_term located image](https://github.com/eraydvl/Litex-Doc/blob/main/images/litex_vexriscv.png)

Karşımıza çıkan ekranda `serialboot` komutunu kullanarak yüklediğimiz boot dosyasını başlatmalıyız.

![linux located image](https://github.com/eraydvl/Litex-Doc/blob/main/images/linux_located.png)
