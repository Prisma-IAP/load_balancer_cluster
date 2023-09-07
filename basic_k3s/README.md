# Primeiros passos - Cluster com K3s

Neste tutorial introdutório serão apresentados os passos iniciais de utilização do K3s para a criação de um ambiente clusterizado em *Single-Board Computers (SBC)* como *Raspberry Pi*, *Orange Pi*, entre outros. Para maiores informações sobre o K3s, basta acessar a [documentação oficial](https://docs.k3s.io/).

Durante este tutorial serão abordados dois tipos de máquinas: 
- **Servers** - são as máquinas onde o K3s será instalado e terão as configurações principais com os manifestos yaml, contendo todas as informações para o deploy de aplicações, podendo ser sites com páginas estáticas, até projetos maiores envolvendo banco de dados.
- **Agents ou Workers** - são máquinas consideradas como nós, onde irão adicionar de forma complementar novas instâncias dos serviços configurados nos *Servers*. Ex.: em casos de serviços como *Load-Balancer*, quando maior a quantidade de máquinas, maior a disponibilidade de escalonamento e acesso a aplicação 

## Passo 01: Preparação de redes
- Neste passo, é de suma importância que os IPs de cada computador seja estático. Para isso, basta seguir os passos de configurações de rede [neste repositório](https://github.com/Prisma-IAP/basic_network_configs)

## Passo 02: Instalando o K3s em uma máquina Server
- Após acessar o terminal, sendo de forma remota, por ssh ou com o *SBC* conectado em um monitor, digite o comando abaixo:
```shell
curl -sfL https://get.k3s.io | sh -
```

- Caso opte por remover algum recurso complementar que é adicionado durante a instalação, como o *Traefik*, o comando pode ser realizado dessa forma:
```shell
curl -sfL https://get.k3s.io | sh -s - --disable=traefik
```