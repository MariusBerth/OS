simul: myos.iso
	qemu-system-i386 -cdrom myos.iso

test_kernel: myos.bin
	qemu-system-i386 -kernel myos.bin

myos.iso: myos.bin
	mkdir -p isodir/boot/grub
	cp myos.bin isodir/boot/myos.bin
	cp grub.cfg isodir/boot/grub/grub.cfg
	grub-mkrescue -o myos.iso isodir

myos.bin: boot.o kernel.o linker.ld
	i686-elf-gcc -T linker.ld -o myos.bin -ffreestanding\
		-O2 -nostdlib boot.o kernel.o -lgcc

boot.o: boot.s
	i686-elf-as boot.s -o boot.o

kernel.o: kernel.c
	i686-elf-gcc -c kernel.c -o kernel.o -std=gnu99\
	       	-ffreestanding -O2 -Wall -Wextra

clean:
	rm -rf isodir
	rm -f kernel.o
	rm -f myos.bin
	rm -f myos.iso
	rm -f boot.o

.PHONY: clean simul test_kernel
