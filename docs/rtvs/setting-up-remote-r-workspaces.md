---
title: Workspaces remotos para R
description: Como configurar workspaces remotos de R e conectar-se a eles do Visual Studio.
ms.date: 12/04/2017
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: 207e4c2d6e7db9dd40288306b3a87086c4568f76
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49827708"
---
# <a name="set-up-remote-workspaces"></a>Configurar workspaces remotos

Este artigo explica como configurar um servidor remoto com SSL e um serviço do R adequado. Isso permite que as RTVS (Ferramentas do R para Visual Studio) se conectem a um workspace remoto nesse servidor.

## <a name="remote-computer-requirements"></a>Requisitos do computador remoto

- Windows 10, Windows Server 2016 ou Windows Server 2012 R2. As RTVS também requerem
- [.NET framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) ou superior

## <a name="install-an-ssl-certificate"></a>Instalar um certificado SSL

As RTVS requerem que todas as comunicações com um servidor remoto ocorram por HTTP, o que requer um certificado SSL no servidor. Você pode usar um certificado assinado por uma autoridade de certificação confiável (recomendado) ou um certificado autoassinado. (Um certificado autoassinado faz com que as RTVS emitam avisos quando conectadas.) Nas duas opções, você precisa instalá-lo no computador e permitir o acesso a sua chave privada.

### <a name="obtain-a-trusted-certificate"></a>Obter um certificado confiável

Um certificado confiável é emitido por uma autoridade de certificação (consulte [autoridades de certificação na Wikipédia](https://en.wikipedia.org/wiki/Certificate_authority) para saber mais). Como obter um cartão de identificação do governo, emitir um certificado confiável envolve um processo maior e possíveis taxas, mas verifica a autenticidade da solicitação e do solicitante.

O campo de chave que precisa estar no certificado é o nome de domínio totalmente qualificado do computador do servidor R. A autoridade de certificação exige uma prova de que você está autorizado a criar um novo servidor para o domínio ao qual seu servidor pertence.

Para obter mais informações, consulte [Public key certificate](https://en.wikipedia.org/wiki/Public_key_certificate) (certificados de chave pública) na Wikipédia.

## <a name="install-an-ssl-certificate-on-windows"></a>Instalar um certificado SSL no Windows

O certificado SSL deve ser instalado manualmente no Windows. Siga as instruções abaixo para instalar um certificado SSL.

### <a name="obtain-a-self-signed-certificate-windows"></a>Obter um certificado autoassinado (Windows)

Ignore esta seção se você tem um certificado confiável. Em comparação com um certificado de uma autoridade confiável, um certificado autoassinado é como criar um cartão de identificação para você. Esse processo é, naturalmente, muito mais simples do que trabalhar com uma autoridade confiável, mas também não tem autenticação forte, o que significa que um invasor pode substituir seus próprios certificados pelo certificado não assinado e capturar todo o tráfego entre o cliente e o servidor. Portanto, *o certificado autoassinado deve ser usado somente para testar cenários, em uma rede confiável e nunca em produção.*

Por esse motivo, as RTVS sempre emitem o seguinte aviso durante a conexão com um servidor com um certificado autoassinado:

![Caixa de diálogo de aviso de certificado autoassinado](media/workspaces-remote-self-signed-certificate-warning.png)

Para emitir um certificado autoassinado:

1. Faça logon no computador do servidor R usando uma conta Administrador.
1. Abra um novo prompt de comando do PowerShell do administrador e execute o seguinte comando, substituindo `"remote-machine-name"` pelo nome de domínio totalmente qualificado do computador servidor.

    ```ps
    New-SelfSignedCertificate -CertStoreLocation Cert:\LocalMachine\My -DnsName "remote-machine-name"
    ```

1. Se você nunca executou o PowerShell antes no computador do R Server, execute o seguinte comando para habilitar a execução explícita de comandos:

    ```ps
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    ```

Para obter informações, consulte [self-signed certificates](https://en.wikipedia.org/wiki/Self-signed_certificate) (certificados autoassinados) na Wikipédia.

### <a name="install-the-certificate"></a>Instalar o certificado

Para instalar o certificado no computador remoto, execute *certlm.msc* (o gerenciador de certificados) em um prompt de comando. Clique com o botão direito do mouse na pasta **Pessoal** e selecione o comando **Todas as Tarefas** > **Importar**:

![Comando Importar certificado](media/workspaces-remote-certificate-import.png)

### <a name="grant-permissions-to-read-the-ssl-certificates-private-key"></a>Conceder permissões para ler a chave privada do certificado SSL

Depois que o certificado for importado, conceda à conta `NETWORK SERVICE` permissões para ler a chave privada conforme descrito nas instruções a seguir. `NETWORK_SERVICE` é a conta usada para executar o agente de serviços do R, que é o serviço que termina as conexões SSL de entrada para o computador servidor.

1. Execute *certlm.msc* (o Gerenciador de Certificados) em um prompt de comando do administrador.
1. Expanda **Pessoal** > **Certificados**, clique com o botão direito do mouse no certificado e selecione **Todas as Tarefas** > **Gerenciar Chaves Privadas**.
1. Clique com o botão direito do mouse no certificado e selecione o comando **Gerenciar Chaves Privadas** em **Todas as Tarefas**.
1. Na caixa de diálogo que aparece, selecione **Adicionar** e insira `NETWORK SERVICE` como o nome da conta:

    ![Caixa de diálogo Gerenciar Chaves Privadas, adicionando NETWORK_SERVICE](media/workspaces-remote-manage-private-key-dialog.png)

1. Selecione **OK** duas vezes para fechar as caixas de diálogo e confirmar suas alterações.

## <a name="install-an-ssl-certificate-on-ubuntu"></a>Instalar um certificado SSL no Ubuntu

O pacote `rtvs-daemon` instalará um certificado autoassinado por padrão como parte da instalação.

### <a name="obtain-a-self-signed-certificate-ubuntu"></a>Obter um certificado autoassinado (Ubuntu)

Para obter os benefícios e os riscos do uso de um certificado autoassinado, confira a descrição do Windows. O pacote `rtvs-daemon` gera e configura o certificado autoassinado durante a instalação. Você precisará fazer isso apenas se quiser substituir o certificado autoassinado gerado automaticamente.

Para emitir um certificado autoassinado por conta própria:

1. Use o SSH ou faça logon no computador Linux.
2. Instale o pacote `ssl-cert`:
    ```sh
    sudo apt-get install ssl-cert
    ```
3. Execute `make-ssl-cert` para gerar o certificado SSL autoassinado padrão:
    ```sh
    sudo make-ssl-cert generate-default-snakeoil --force-overwrite
    ```
4. Converta a chave gerada e os arquivos PEM em PFX. O PFX gerado deve estar na sua pasta inicial:
    ```sh
    openssl pkcs12 -export -out ~/ssl-cert-snakeoil.pfx -inkey /etc/ssl/private/ssl-cert-snakeoil.key -in /etc/ssl/certs/ssl-cert-snakeoil.pem -password pass:SnakeOil
    ```

### <a name="configure-rtvs-daemon"></a>Configurar o daemon das RTVS

O caminho de arquivo do certificado SSL (caminho para o PFX) precisa ser definido em */etc/rtvs/rtvsd.config.json*. Atualize `X509CertificateFile` e `X509CertificatePassword` com o caminho do arquivo e a senha, respectivamente.

```json
{
  "logging": { "logFolder": "/tmp" },
  "security": {
    "allowedGroup": "",
    "X509CertificateFile": "/etc/rtvs/ssl-cert-snakeoil.pfx",
    "X509CertificatePassword": "SnakeOil"
  },
  "startup": { "name": "rtvsd" },
  "urls": "https://0.0.0.0:5444"
}
```

Salve o arquivo e reinicie o daemon, `sudo systemctl restart rtvsd`.

## <a name="install-r-services-on-windows"></a>Instalar serviços do R no Windows

Para executar o código R, o computador remoto deve ter um interpretador de R instalado da seguinte maneira:

1. Baixe e instale um dos seguintes:

   - [Microsoft R Open](https://mran.microsoft.com/open/)
   - [CRAN R para Windows](https://cran.r-project.org/bin/windows/base/)

     Ambos têm funcionalidade idêntica, mas o Microsoft R Open beneficia-se de bibliotecas de álgebra linear aceleradas por hardware como cortesia do [Intel Math Kernel Library](https://software.intel.com/intel-mkl).

2. Execute o [Instalador de serviços do R](https://aka.ms/rtvs-services) e reinicie quando solicitado. O instalador faz o seguinte:

    - Crie uma pasta em *%PROGRAMFILES%\R Tools for Visual Studio\1.0\\* e copie todos os binários necessários.
    - Instala `RHostBrokerService` e `RUserProfileService` e configura para iniciar automaticamente.
    - Configura o serviço `seclogon` para iniciar automaticamente.
    - Adicione *Microsoft.R.Host.exe* e *Microsoft.R.Host.Broker.exe* às regras de entrada do firewall na porta padrão 5444.

Os serviços do R serão iniciados automaticamente quando o computador for reiniciado:

- O **Serviço de agente de host do R** lida com todo o tráfego HTTPS entre o Visual Studio e o processo em que o código R é executado no computador.
- O **Serviço de perfil do usuário do R** é um componente com privilégios que lida com a criação de perfil do usuário do Windows. O serviço é chamado quando um novo usuário faz logon pela primeira vez no computador do servidor R.

Você pode ver esses serviços no console de gerenciamento de serviços (*compmgmt.msc*).

## <a name="install-r-services-on-linux"></a>Instalar Serviços R no Linux

Para executar o código R, o computador remoto deve ter um interpretador de R instalado da seguinte maneira:

1. Baixe e instale um dos seguintes:

   - [Microsoft R Open](https://mran.microsoft.com/open/)
   - [CRAN R para Windows](https://cran.r-project.org/bin/linux/ubuntu/)

     Ambos têm funcionalidade idêntica, mas o Microsoft R Open beneficia-se de bibliotecas de álgebra linear aceleradas por hardware como cortesia do [Intel Math Kernel Library](https://software.intel.com/intel-mkl).

2. Siga as instruções no [Serviço R Remoto para Linux](setting-up-remote-r-service-on-linux.md), que abrange computadores Ubuntu físicos, máquinas virtuais do Azure Ubuntu, WSL (Subsistema Windows para Linux) e contêineres do Docker, incluindo os que estão em execução no Repositório de Contêineres do Azure.

## <a name="configure-r-services"></a>Configurar serviços do R

Com os serviços do R em execução no computador remoto, você também precisa criar contas de usuário, definir regras de firewall, configurar a rede do Azure e configurar o certificado SSL.

1. Contas de usuário: crie contas para cada usuário que acessa o computador remoto. Você pode criar contas de usuário local padrão (sem privilégios) ou pode ingressar o computador do servidor R em seu domínio e adicionar os grupos de segurança apropriados ao grupo de segurança `Users`.

1. Regras de firewall: por padrão, o `R Host Broker` escuta na porta TCP 5444. Portanto, verifique se há regras de firewall do Windows habilitadas para o tráfego de entrada e saída (a saída é necessária para instalar pacotes e cenários semelhantes).  O instalador de serviços do R define essas regras automaticamente para o firewall do Windows interno. No entanto, se você estiver usando um firewall de terceiros, abra manualmente a porta 5444 para o `R Host Broker`.

1. Configuração do Azure: se o computador remoto for uma máquina virtual no Azure, abra a porta 5444 para tráfego de entrada na rede do Azure, que é independente do firewall do Windows. Para obter detalhes, consulte [Filtrar o tráfego de rede com grupos de segurança de rede](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) na documentação do Azure.

1. Informar ao Agente de Host do R qual certificado SSL deve ser carregado: se você estiver instalando o certificado em um servidor de Intranet, é provável que o nome de domínio totalmente qualificado do servidor seja o mesmo que seu nome NETBIOS. Nesse caso não há nada que você precise fazer, pois esse é o certificado padrão que é carregado.

    No entanto, se você estiver instalando o certificado em um servidor voltado para à Internet (como uma VM do Azure), use o FQDN (nome de domínio totalmente qualificado) do servidor, porque o FQDN de um servidor voltado à Internet nunca é o mesmo que seu nome NETBIOS.

    Para usar o FQDN, navegue para o local em que o R Services está instalado (*%PROGRAM FILES%\R Remote Service for Visual Studio\1.0*, por padrão), abra o arquivo *Microsoft.R.Host.Broker.Config.json* em um editor de texto e substitua o conteúdo pelo seguinte, atribuindo o CN ao FQDN do servidor, como `foo.westus.cloudapp.azure.com`:

    ```json
    {
      "server.urls": "https://0.0.0.0:5444",
      "security": {
        "X509CertificateName": "CN=your-server-fully-qualified-domain-name"
      }
    }
    ```

    Salve o arquivo e reinicie o computador para aplicar as alterações.

## <a name="troubleshooting"></a>Solução de problemas

**P. O computador do R Server não está respondendo. O que devo fazer?**

Tente executar ping para o computador remoto na linha de comando: `ping remote-machine-name`. Se o ping falhar, verifique se o computador está em execução.

**P. A janela do R Interativo diz que o computador remoto está ativado, mas por que o serviço não está em execução?**

Existem três motivos possíveis:

- O [.NET framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) ou superior não está instalado no computador.
- As regras de firewall para `Microsoft.R.Host.Broker` e `Microsoft.R.Host` não estão habilitadas para conexões de entrada e saída na porta 5444.
- Um certificado SSL com `CN=<remote-machine-name>` não foi instalado.

Reinicie o computador depois de fazer as alterações acima. Em seguida, verifique se `RHostBrokerService` e `RUserProfileService` estão em execução por meio do Gerenciador de Tarefas (guia serviços) ou de *services.msc*.

**P. Por que a janela R Interativo disse "401 acesso negado" ao fazer a conexão com o servidor R?**

Há dois motivos possíveis:

- É muito provável que a conta `NETWORK SERVICE` não tenha acesso à chave privada do certificado SSL. Siga as instruções anteriores para conceder o acesso `NETWORK SERVICE` à chave privada.
- Verifique se o serviço `seclogon` está em execução. Use *services.msc* para configurar `seclogon` para que ele seja iniciado automaticamente.

**P. Por que a janela R Interativo disse "404 não encontrado" ao fazer a conexão com o servidor R?**

Esse erro provavelmente ocorre devido à ausência de bibliotecas redistribuíveis do Visual C++. Verifique a janela do R Interativo para ver se há uma mensagem sobre a biblioteca (DLL) ausente. Verifique se o VS 2015 redistribuível está instalado e se o R está instalado também.

**P. Não consigo acessar a Internet e os recursos da janela R Interativo, o que devo fazer?**

Verifique se as regras de firewall para `Microsoft.R.Host.Broker` e `Microsoft.R.Host` permitem acesso de saída na porta 5444. Reinicie o computador após a aplicação das alterações.

**P. Eu tentei todas essas soluções e ainda não funciona. E agora?**

Examine os arquivos de log em *C:\Windows\ServiceProfiles\NetworkService\AppData\Local\Temp*. Essa pasta contém arquivos de log separados para cada instância do Serviço de Agente do R que foi executada. Um novo arquivo de log é criado sempre que o serviço é reiniciado. Verifique o arquivo de log mais recente para encontrar pistas sobre o que pode estar errado.
