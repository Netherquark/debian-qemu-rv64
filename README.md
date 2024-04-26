# debian-qemu-rv64
Meta repo for initialising a RISC-V env

- `sudo apt install binutils-riscv64-linux-gnu binutils-riscv64-unknown-elf gcc-riscv64-unknown-elf gcc-riscv64-linux-gnu cpp-riscv64-linux-gnu g++-riscv64-linux-gnu`
  - Installs necessary toolchain packages for RISC-V architecture.
  
- `sudo apt install opensbi u-boot`
  - Installs OpenSBI and U-Boot, which are firmware/bootloader components for RISC-V. May not be available on all distros.

- `wget --output-document dqib.zip https://gitlab.com/api/v4/projects/giomasce%2Fdqib/jobs/artifacts/master/download?job=convert_riscv64-virt`
  - Downloads a zip file containing a project named dqib from GitLab.

- `unzip dqib.zip`
  - Unzips the downloaded zip file.

- `cd dqib_riscv64-virt`
  - Changes the current directory to dqib_riscv64-virt.

- `qemu-system-riscv64 -machine 'virt' -cpu 'rv64' -smp sockets=1,cores=4,threads=1 -m 4G -device virtio-blk-device,drive=hd -drive file=image.qcow2,if=none,id=hd -device virtio-net-device,netdev=net -netdev user,id=net,hostfwd=tcp::2222-:22 -bios /usr/lib/riscv64-linux-gnu/opensbi/generic/fw_jump.elf -kernel /usr/lib/u-boot/qemu-riscv64_smode/uboot.elf -object rng-random,filename=/dev/urandom,id=rng -device virtio-rng-device,rng=rng -nographic -append "root=LABEL=rootfs console=ttyS0"`
  - Executes QEMU to emulate a RISC-V machine with specific parameters, including CPU configuration, memory size, block device, network device, firmware, kernel, and boot parameters.
