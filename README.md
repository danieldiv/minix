![VM](https://img.shields.io/badge/VM-VirtualBox-success)
![ISO](https://img.shields.io/badge/ISO-Linux-red)

Documentação teorica por ser encontrada em [Wiki](https://github.com/danieldiv/minix/wiki)

# Funcionamento

# Tutorial

## Camadas

<p align="justify">
  O Minix é divido em 4 camadas principais: Camada de Kernel (Núcleo), camada de Drivers para dispostivos do Hardware, camada de Servidor e camada do Usuário.
  <ol>
  
  <strong>
    <li>
      Kernel (Núcleo):
    </li>
  </strong>
  <p align="justify">
    Camada responsável por tratar serviços de "baixo nível" para o funcionamento do SO. Toda a parte de interrupções, <i>Traps</i>, gerenciamento de memória, escalonamento e comunicação com o hardware está nesta camada. A parte que lida com as interrupções a nível de Hardware é utilizado <i>Assembly</i>, todo o restante é escrito em <i>Linguagem C</i>.
  </p>
  
  <strong>
  <li>
      Drivers:
    </li>
  </strong>
  <p align="justify">
    Todos os processos de I/O (Input/Output) estão nesta camada. O Disco, o Terminal, a Placa de Rede (Minix3 possui suporte a redes TCP/IP) e Relógios. Estes dispositivos em outros Sitemas Operacionais, são conhecidos como Drives de Dispositivo. No Minix, todos os processos desta camadas, estão ligados aos processos da primeira camada - ligados por código. A camada 1 e 2 juntas formam um programa único, chamado KERNEL.
  </p>
  </ol>
  
</p>

## Como baixar e instalar

### Download

Partindo-se do princípio que o minix é um sistema operacional voltado para estudos e não para utilização real é coerente a ideia de instalá-lo em uma máquina virtual. Nesse caso será utilizado o `VirtualBox` da Oracle, que pode ser baixado <a href = "https://www.virtualbox.org/wiki/Downloads">aqui</a>. A próxima etapa é o download da .iso do Minix 3, a qual é encontrada no próprio <a href="https://wiki.minix3.org/doku.php?id=www:download:start">site do Minix</a>.

### Requisitos

A máquina virtual permite configurar quais recursos do hardware serão alocados para o sistema operacional visitante, no caso o Minix. Por ser um sistema leve e sem nem mesmo interface gráfica seus requsitos recomendados são bem fáceis de atender.

#### Processador

Segundo o site do SO um processador da família pentium da intel ou superior são suficidentes, assim dedicar apenas um núcleo do processador para essa máquina virtual é o suficiente.

<img src = "https://github.com/danieldiv/minix/blob/master/imgs/prints_instalacao/4.png"></img>

#### Memória

Pela documentação do Minix 3 256 MB de RAM são suficientes para o sistema, porém considerando-se que um computador razoavelmente moderno possui pelo meno 4 GB de RAM dedicar 512 MB ou 1 GB para o SO garante um bom desempenho do mesmo sem comprometer o desempenho do computador.

<img src = "https://github.com/danieldiv/minix/blob/master/imgs/prints_instalacao/2.png" height="400em"></img>

#### Armazenamento

O Minix 3 recomenda no mínimo 2.2 GB de espaço em disco para poder utilizar todas as funcionalidades do mesmo, porém novamente, considerando-se que dispositivos de armazenamento modernos possuem no mínimo 128 GB, dedicar 3 ou 4 GB para o SO garante que o armazenamento não será um problema.

Vale a pena observar que o Minix possui suporte apenas à dispositivos de armazenamento que utilizam barramento SATA (ou o mais antigo, IDE), assim SSDs do tipo NVME ou dispositivos USB não podem ser usados. Como nesse caso estamos instalando o Minix em uma VM (máquina virtual) basta configurar a partir dela o disco, idenpedente do barramento real utlizado.

<img src = "https://github.com/danieldiv/minix/blob/master/imgs/prints_instalacao/3.png" height="400em"></img>

#### Periféricos

Por se tratar de um SO voltado para o estudo de seu funcionamento, o Minix não possue suporte a muitos periféricos além do teclado, inclusive é recomendado destivar desativar o audio da máquina virtual para evitar problemas de comapatibilidade

<img src = "https://github.com/danieldiv/minix/blob/master/imgs/prints_instalacao/5.png" height="400em"></img>

## Instalação

Para iniciar o processo de instalação basta inserir o um disco virtual na VM com a .iso do Minix 3 e iniciar a máquina.

<img src = "https://github.com/danieldiv/minix/blob/master/imgs/prints_instalacao/6.png" height="400em"></img>

O processo de instalação em si é bem simples:
1. selecione a opção de "Regular Minix 3" 

<img src = "https://github.com/danieldiv/minix/blob/master/imgs/prints_instalacao/7.png" height="400em"></img>

2. Após isso faça login com o "root" e dê o comando "setup".

3. Nesse ponto o instalador pede o tipo de teclado usado, no caso do padrão brasileiro com a tecla "ç" é o "abnt2".

4. O próximo passo é a partição do disco. Como já foi tudo configurado na máquina virtual basta usar o "automatic mode".

5. Em seguida é pedido para definir o tamanho do bloco de sistema, que por padrão é de 4 kB.

6. O último estágio é a configuração de rede, que também pode ser configurado automaticamente com a opção "1".

Após isso a instalação está concluída, digite o comando "poweroff" para desligar a máquina, remova o disco com a .iso do Minix 3 e inicie ela novamente. Com isso já será possivel realizar login no sistema e utilizá-lo.

<img src = "https://github.com/danieldiv/minix/blob/master/imgs/prints_instalacao/8.png" height="400em"></img>

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
