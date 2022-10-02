![VM](https://img.shields.io/badge/VM-VirtualBox-success)
![ISO](https://img.shields.io/badge/ISO-Linux-red)

Documentação teorica por ser encontrada em [Wiki](https://github.com/danieldiv/minix/wiki)

# Funcionamento

# Tutorial

## Camadas

`Gabriel Oliveira Alves`

## Como baixar e instalar

`João Victor F Barros`

## Localizacao

> Escalonador

- Gerenciador de memoria
- Gerenciador de arquivo

### Quantum

- Tempo de execução que uma CPU tem disponivel para executar um processo em `milisegundos`

- O `quantum` pode ser encontrado em [minix/include/minix/config.h](https://github.com/danieldiv/minix/blob/master/minix/include/minix/config.h#L74) utilizando o define `#define USER_QUANTUM 200`, onde 200 representa `200` milisegundos.

### Filas de prioridade

- A quantidade da fila de prioridade do minix pode ser encontrada em [minix/include/minix/config.h](https://github.com/danieldiv/minix/blob/master/minix/include/minix/config.h#L66) utilizando o define `#define NR_SCHED_QUEUES 16`, onde 16 representa uma fila de prioridade com tamanho `16`.

- Implementado pelo nucleo `(kernel)` e usuário, abaixo será mostrado algumas das funções que implementam as configurações.

- Kernel [src/so/minix/kernel](https://github.com/danieldiv/minix/tree/master/minix/kernel)

  - `proc.h` -> possui a tabela de procesos, faz a inclusao de (const.h) que inclue o (config.h)
  - `proc.c`-> faz a inclusao de (proc.h)

- Usuario [minix/servers/sched](https://github.com/danieldiv/minix/tree/master/minix/servers/sched)
  - `schedule.c`
  - `schedproc.h`
  - `sched.h`
  - `proto.h`
  - `utility.c`
  - `main.c`

## Modificacoes

`Ygor Santos Vieira`

# Referencias

- [Compilando o MINIX 3 ...](https://sergioprado.org/compilando-o-minix-3-para-beaglebone-black/)
- [How to compile MINIX and run ...](https://www.youtube.com/watch?v=cH1UDLp9pQ0)
- [Conheça o Minix ...](https://sempreupdate.com.br/minix-o-sistema-que-o-linus-se-basesou-para-criar-o-linux/)
- [Escalonamento no Minix 3 ...](https://www.youtube.com/watch?v=-TUmEsa3sno)
- [Stichting MINIX Research Foundation (Git)](https://github.com/Stichting-MINIX-Research-Foundation/minix)
