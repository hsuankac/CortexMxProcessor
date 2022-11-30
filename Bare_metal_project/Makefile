CC=arm-none-eabi-gcc
MACH=cortex-m4
CFLAGS= -c -mcpu=$(MACH) -mthumb -mfloat-abi=soft -std=gnu11 -Wall -O0
#Wl tells the eabi-gcc compiler it is a linker command
LDFALGS = -mcpu=$(MACH) -mthumb -mfloat-abi=soft --specs=nano.specs -T stm32_ls.ld -Wl,-Map=final.map
LDFALGS_SH = -mcpu=$(MACH) -mthumb -mfloat-abi=soft --specs=rdimon.specs -T stm32_ls.ld -Wl,-Map=final.map

all:main.o led.o stm32_startup.o syscalls.o final.elf

#semi-hosting feature does not need to include syscall.o
semi:main.o led.o stm32_startup.o final_sh.elf

main.o:main.c
	$(CC) $(CFLAGS) $^ -o $@

led.o:led.c
	$(CC) $(CFLAGS) $^ -o $@
	
stm32_startup.o:stm32_startup.c
	$(CC) $(CFLAGS) $^ -o $@
	
syscalls.o:syscalls.c
	$(CC) $(CFLAGS) $^ -o $@

final.elf: main.o led.o stm32_startup.o syscalls.o
	$(CC) $(LDFALGS) $^ -o $@

final_sh.elf: main.o led.o stm32_startup.o
	$(CC) $(LDFALGS_SH) $^ -o $@

clean:
	rm -rf *.o *.elf

load:
	openocd -f board/stm32f4discovery.cfg