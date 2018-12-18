---
title: Configurando o Serviço R Remoto no Linux
description: Como configurar o Serviço de R Remoto no Ubuntu e no subsistema do Windows para Linux.
ms.date: 12/04/2017
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
ms.reviewer: karthiknadig
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: 81a0a5c26e91056e757bc6e6f68cd217e98c7e06
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220801"
---
# <a name="remote-r-service-for-linux"></a>Serviço R Remoto para Linux

No momento, o Serviço R Remoto para Linux está empacotado como rtvs-daemon. O daemon é compatível com a área de trabalho e o servidor Ubuntu 16.04, 16.10 LTS e com o Subsistema Windows para o Linux em execução no Ubuntu e testado neles. A maior parte deste artigo fornece instruções para configurar o Serviço R Remoto nesses diferentes sistemas.

Depois de configurar o computador remoto, as etapas a seguir conectam as RTVS (Ferramentas do R para Visual Studio) a este serviço:

1. Selecione **Ferramentas do R** > **Windows** > **Espaços de trabalho** para abrir a janela **Espaços de trabalho**.
1. Selecione **Adicionar Conexão**.
1. Dê um nome à conexão e forneça sua URL, como `https://localhost:5444` (Subsistema Windows para Linux) ou `https://public-ip:5444` (contêiner do Azure). Selecione **Salvar** quando concluir.
1. Selecione o ícone de conexão ou clique duas vezes no item de conexão.
1. Forneça as credenciais de logon. O nome de usuário deve ter o prefixo `<<unix>>\` como no `<<unix>>\ruser1` (conforme necessário para todas as conexões com computadores Linux remotos).
1. Se você estiver usando um certificado autoassinado, poderá ver um aviso. A mensagem fornece instruções para corrigir o aviso.

## <a name="set-up-remote-r-service"></a>Configurar o Serviço R Remoto

Esta seção descreve as opções a seguir:

- [Computador físico Ubuntu](#physical-ubuntu-computer)
- [VM do Ubuntu Server ou VM de Ciência de Dados no Azure](#ubuntu-server-vm-or-data-science-vm-on-azure)
- [Contêiner do Docker local ou remoto (build limpo)](#local-or-remote-docker-container-clean-build)
- [Contêiner em execução em Instâncias de Contêiner do Azure](#container-running-on-azure-container-instances)

Em cada caso, o computador remoto deve ter uma dos seguintes interpretadores do R instalados:

- [Microsoft R Open](https://mran.microsoft.com/open/)
- [CRAN R para Windows](https://cran.r-project.org/bin/linux/ubuntu/)

### <a name="physical-ubuntu-computer"></a>Computador físico Ubuntu

1. Depois de fazer logon no computador, baixe o rtvs-daemon tarball:

    ```bash
    wget -O rtvs-daemon.tar.gz https://aka.ms/r-remote-services-linux-binary-current
    tar -xvzf rtvs-daemon.tar.gz
    ```

1. Execute o script de instalação:

    ```bash
    sudo ./rtvs-install
    ```

    Para uma automação silenciosa, use `sudo ./rtvs-install -s`.

1. Habilite e inicie o serviço:

    ```bash
    sudo systemctl enable rtvsd
    sudo systemctl start rtvsd
    ```

1. Configure o certificado SSL (necessário para a produção). Por padrão, o rtvs-daemon usa o `ssl-cert-snakeoil.pem` e o `ssl-cert-snakeoil.pem` gerados pelo pacote `ssl-cert`. Durante a instalação, eles são combinadas em `ssl-cert-snakeoil.pfx`. Para fins de produção, use o certificado SSL fornecido pelo seu administrador. O certificado SSL pode ser configurado fornecendo um arquivo *.pfx* e a senha de importação opcional em: */etc/rtvs/rtvsd.config.json*.

1. (Opcional) Verifique se o serviço está em execução:

    ```bash
    ps -A -f | grep rtvsd
    ```

    Se você não vir um processo em execução com o nome de usuário `rtvssvc`. Inicie-o usando o seguinte comando:

    ```bash
    sudo systemctl start rtvsd
    ```

1. Para configurar adicionalmente o rtvs-daemon, consulte `man rtvsd`.

### <a name="ubuntu-server-vm-or-data-science-vm-on-azure"></a>VM do Ubuntu Server ou VM de Ciência de Dados no Azure

#### <a name="create-a-vm"></a>Criar uma VM

1. Entre no [Portal do Azure](https://portal.azure.com).
1. Navegue até Máquinas Virtuais e selecione **Adicionar**.
1. Na lista de imagens de VM disponíveis, pesquise e selecione um dos seguintes:
    - Ubuntu Server: `Ubuntu Server 16.04 LTS`
    - VM de Ciência de Dados: `Linux Data Science` (consulte [Máquinas Virtuais de Ciência de Dados](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) para obter detalhes)
1. Defina o modelo de implantação como `Resource manager` e selecione **Criar**.
1. Escolha um nome para a VM, forneça um nome de usuário e senha (a senha é obrigatória, já que não há suporte para o logon da chave pública SSH).
1. Fazer outras alterações desejadas na configuração de VM.
1. Escolha um tamanho da VM, verifique a configuração e selecione **Criar**. Depois que a VM for criada, passe para a próxima seção.

#### <a name="configure-the-vm"></a>Configurar a VM

1. Na seção **Rede** da VM, adicione 5444 como uma porta de entrada permitida. Para usar uma porta diferente, altere a configuração no arquivo de configuração do daemon das RTVS (*/etc/rtvs/rtvsd.config.json*).
1. (Opcional) Definir um nome DNS; também é possível usar o endereço IP.
1. Conecte-se à VM usando um cliente SSH, como o PuTTY para WIndows.
1. Siga as instruções para um [Computador Ubuntu físico](#physical-ubuntu-computer) acima.

### <a name="windows-subsystem-for-linux-wsl"></a>WSL (Subsistema Windows para Linux)

1. Siga as instruções de instalação do WSL para o [Windows 10](/windows/wsl/install-win10#install-the-windows-subsystem-for-linux) ou para o [Windows Server](/windows/wsl/install-on-server#enable-the-windows-subsystem-for-linux-wsl).
1. Inicie o bash no Windows e siga as instruções anteriores em um [computador Ubuntu físico](#physical-ubuntu-computer) com uma exceção. Na etapa 3, inicie o serviço usando o comando `rtvsd`, porque, no momento, o WSL não dá suporte às interfaces systemd/systemctl.

### <a name="local-or-remote-docker-container-clean-build"></a>Contêiner do Docker local ou remoto (build limpo)

1. Crie um arquivo do Docker com conteúdo abaixo, que instala o daemon do Serviço R Remoto e a versão mais recente do R. **Observação**: este script cria um usuário chamado "ruser1" com a senha "foobar", que você pode modificar conforme desejado nas duas últimas instruções `RUN`.

    ```docker
    FROM ubuntu:16.04

    ARG DEBIAN_FRONTEND=noninteractive

    RUN apt-get update \
     && apt-get install -y software-properties-common python-software-properties \
     && apt-get install -y apt-transport-https \
     && rm -rf /var/lib/apt/lists/*

    RUN sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' \
     && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893 \
     && sh -c 'echo "deb https://cran.revolutionanalytics.com/bin/linux/ubuntu xenial/" > /etc/apt/sources.list.d/cran-r.list' \
     && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9 \
     && rm -rf /var/lib/apt/lists/* \
     && apt-get clean

    RUN apt-get update --fix-missing && apt-get update \
     && apt-get install -y dotnet-dev-1.0.4 libexplain51 libzip4 libc6 git lshw ssl-cert wget \
     && rm -rf /var/lib/apt/lists/*

    # install R
    RUN apt-get update && apt-get install -y r-base-dev
    RUN apt upgrade -y

    # install rtvs-daemon
    RUN wget -O rtvs-daemon.tar.gz https://aka.ms/r-remote-services-linux-binary-current && tar -xvzf rtvs-daemon.tar.gz && ./rtvs-install -s

    RUN useradd --create-home ruser1
    RUN echo "ruser1:foobar" | chpasswd

    EXPOSE 5444
    ```

1. Compilar e executar o arquivo do Docker:

    ```bash
    docker build -t myrimage .
    docker run -p 5444:5444 myrimage rtvsd
    ```

1. Para conectar-se ao conteúdo das RTVS, use `https://localhost:5444` como o caminho, nome de usuário `<<unix>>\ruser1` e a senha `foobar`. Se o contêiner estiver em execução em um computador remoto, use `https://remote-host-name:5444` como o caminho. A porta pode ser alterada atualizando */etc/rtvs/rtvsd.config.json*.

### <a name="container-running-on-azure-container-instances"></a>Contêiner em execução em Instâncias de Contêiner do Azure

1. Siga as instruções em [Contêiner do Docker local ou remoto (build limpo)](#local-or-remote-docker-container-clean-build) para criar a imagem.
1. Enviar por push o contêiner para o hub do Docker ou para o Repositório de Contêineres do Azure.
1. Inicie a CLI do Azure e entre usando o comando `az login`.
1. Use o comando `az container create` para criar o contêiner usando `--command-line "rtvsd"` se você não tiver configurado o contêiner para executar `rtvsd` como um serviço `systemd`. No comando abaixo, espera-se que a imagem esteja no hub do Docker. Também é possível usar o Repositório de Contêineres do Azure adicionando argumentos de credencial do Repositório de Contêineres à linha de comando.

    ```bash
    az container create --image myimage:latest --name myaz-container --resource-group myaz-container-res --ip-address public --port 5444 --cpu 2 --memory 4 --command-line "rtvsd"
    ```
1. Use o comando `az container list` para verificar o status. Pesquise `provisioningState`: `Succeeded`.
1. Se o provisionamento tiver sido bem-sucedido, agora será possível se conectar ao contêiner. Pesquise o endereço IP público, no campo `ipAddress`, que pode ser usado com as credenciais no arquivo do docker para conectar-se ao contêiner das RTVS.

