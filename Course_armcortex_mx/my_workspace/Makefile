CC=arm-none-eabi-gcc
MACH=cortex-m4
CFLAGS= -c -mcpu=$(MACH) -mthumb -mfloat-abi=soft -std=gnu11 -Wall -O0
#Wl tells the eabi-gcc compiler it is a linker command
# LDFALGS = -mcpu=$(MACH) -mthumb -mfloat-abi=soft --specs=nano.specs -T stm32_ls.ld -Wl,-Map=final.map
LDFALGS_SH = -mcpu=$(MACH) -mthumb -mfloat-abi=soft --specs=rdimon.specs -T stm32_ls.ld -Wl,-Map=final.map

all:led_main.o led.o stm32_startup.o syscalls.o final.elf

semi:led_main.o led.o stm32_startup.o final_sh.elf

led_main.o:led_main.c
	$(CC) $(CFLAGS) $^ -o $@

led.o:led.c
	$(CC) $(CFLAGS) $^ -o $@
	
stm32_startup.o:stm32_startup.c
	$(CC) $(CFLAGS) $^ -o $@
	
syscalls.o:syscalls.c
	$(CC) $(CFLAGS) $^ -o $@

final.elf: led_main.o led.o stm32_startup.o syscalls.o
	$(CC) $(LDFALGS) $^ -o $@

final_sh.elf: led_main.o led.o stm32_startup.o 
	$(CC) $(LDFALGS_SH) $^ -o $@

clean:
	rm -rf *.o *.elf

load:
	openocd -f board/stm32f4discovery.cfg