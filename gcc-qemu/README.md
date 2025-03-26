# Dockerfile for `gcc-qemu`

This Dockerfile builds a RISC-V development environment with the `riscv-gnu-toolchain` and `qemu`.

## Usage

### Build the Docker Image

```bash
docker buildx build -t gcc-qemu .
```

### Run the Docker Container

```bash
docker run -it --rm -p 2222:22 gcc-qemu
```

This command will never exit, as it starts sshd server inside the container. You can connect to the container using `ssh`:

```bash
ssh root@localhost -p 2222
```

The default password is `riscv`.

### Use the RISC-V Development Environment

```bash
# Compile a RISC-V program
riscv64-linux-gnu-g++ <SOURCE_FILE> -o <OUTPUT_FILE>

# Run the RISC-V program
./<OUTPUT_FILE>
```
