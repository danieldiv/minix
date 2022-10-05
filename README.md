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
  
   <strong>
  <li>
      Servidor:
    </li>
  </strong>
  <p align="justify">
    Esta camada é a responsável por toda a parte de gerenciamento de requisicões da camada de usuário. É ela que fornece os serviços não visíveis que são úteis para os processos de usuário. Como gerenciamento de memória e sistema de arquivos (FS). É a camada de Processos de Servidor que faz a ponte entre as camadas 1 e 2 com os serviços o que são ou não visíveis para o usuário. 
  </p>
  
   <strong>
  <li>
      Usuário:
    </li>
  </strong>
  <p align="justify">
    Na quarta e ultima camada, que é a de mais "alto nível", temos todos os programas que, para funcionarem, utilizam os serviços fornecidos pela camada de Servidor. Como o intepretador de comando - no caso do Minix, é o Shell -, editores de texto, compiladores (cc, gcc, g++, perl, python...etc) entre outros programas a nível de usuário.
  </p>
  
  </ol>
  
  Após entender a função de cada uma das camadas, é evidente que o Minix3 é um Sistema Operacional de acesso hierárquico - o usúario ROOT(Admin) tem o acesso total as funcionalidades de cada camada. Uma boa forma de evidenciar o acesso das camadas é por meio dos repósitorios do Minix após a sua instalação (presente no próximo tópico a baixo).<br>
  Para acessar qualquer camada, basta estar no diretório de Usuário <code>/usr</code>. Dentro de Usuário, no diretório "Source" <code>src</code> com caminho <code>/usr/src</code> basta escolher o diretório referente a camada. Abaixo está os respectivos caminhos.<br>
  
  <ul>    
    <li>
      <code>/usr/src/kernel</code> Camada de Núcleo.
    </li>
   <li>
        <code>/usr/src/drivers</code> Camada de Drivers de dispostivo.
    </li>
    <li>
        <code>/usr/src/servers</code> Camada Servidor ou Serviços.
    </li>
  </ul>
  
  A camada de usuário é o proprio diretório <code>/usr</code>.<br>
  Para mais detalhes acerca do funcionamento de cada camada, olhar o Wiki.
  
</p>

## Como baixar e instalar

O processo de download e configuração da máquina virtual está detalhado na <a href="https://github.com/danieldiv/minix/wiki/3-Como-baixar-e-instalar"> página 3 da wiki</a>, bem como o download da .iso do Minix 3, após a conclusão dessa etapa a instalação via terminal está detalhada abaixo.

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
