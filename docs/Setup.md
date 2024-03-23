# Setup do ambiente EPOS

Este tutorial foi desenvolvido com base nos parâmetros do projeto do semestre 24.1 de SO2. Portanto, a branch poderá variar, assim como a arquitetura. No semestre 24.1 a arquitetura alvo era Risc-V 64 bits.

## EPOS

1. Obtenha o EPOS com o [link](https://gitlab.lisha.ufsc.br/epos/ine5424/-/commits/2024_1) do repositório na branch 2024_1. Você pode cloná-lo ou baixar diretamente e adicionar ao seu próprio repositório.

---

## GCC cross-compiler para Risc-V 64 bits

1. É necessário um compilador que seja capaz de compilar o EPOS para a arquitetura alvo. Você pode baixar uma versão pré compilada através desse [link](https://epos.lisha.ufsc.br/EPOS+Software#GCC_13.2.0_EPOS_2.2_).

2. O makefile do projeto procurará os binários do compilador na pasta `/usr/bin`, mas é possível deixar os binários da pasta que já existe alterando o makefile. Deixe o diretório do EPOS e o diretório do compilador em um mesmo diretório e modifique a variável `rv64_PREFIX` do make file para `rv64_PREFIX := $(shell pwd)/../rv64_toolchain-gcc_13.2.0/riscv/bin/riscv64-unknown-linux-gnu-`

3. O arquivo makedefs também deverá ser modificado. Altere as duas atribuições da variável `riscv_DEBUGGER` para `riscv_DEBUGGER = $(shell pwd)/../../rv64_toolchain-gcc_13.2.0/riscv/bin/riscv64-unknown-linux-gnu-gdb`

---

## Correção de configurações

1. Altere a linha `source $ETC/eposcc.cfg` no arquivo `tools/eposcc/eposcc` para `.  $ETC/eposcc.cfg`.

---

## Qemu

1. Instale o Qemu. No Ubuntu isso pode ser feito com o comando `sudo apt install qemu-system`

---

## Compilação e execução

1. Execute o comando `make` no repositório do EPOS.
2. Para testar, execute `make APPLICATION=hello run`.
3. Para debugar, execute `make APPLICATION=hello debug`. Observe que o console konsole deverá estar instalado.
