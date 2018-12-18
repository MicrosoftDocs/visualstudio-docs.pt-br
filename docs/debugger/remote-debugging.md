---
title: Depuração remota | Microsoft Docs
ms.custom:
- remotedebugging
- seodec18
ms.date: 07/02/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.remote.overview
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: 5a94ad64-100d-43ca-9779-16cb5af86f97
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6701a05d76117e0b8164488de3ec858c61021e17
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53065500"
---
# <a name="remote-debugging"></a>Depuração remota
Você pode depurar um aplicativo do Visual Studio que tenha sido implantado em um computador diferente. Para fazer isso, você deve usar o depurador remoto do Visual Studio.

Para obter instruções detalhadas sobre a depuração remota, consulte estes tópicos.

|Cenário|Link|
|-|-|-|
|Serviço de Aplicativo do Azure|[Depurador de instantâneo](../debugger/debug-live-azure-applications.md) ou [remoto depurar o ASP.NET no Azure](../debugger/remote-debugging-azure.md)|
|VM do Azure|[Depuração remota ASP.NET no Azure](../debugger/remote-debugging-azure.md)|
|Azure Service Fabric|[Depurar um aplicativo do Azure Service Fabric](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)|
|ASP.NET|[ASP.NET Core de depuração remota](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md) ou [depuração remota ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|C# ou Visual Basic|[Depuração remota de um projeto C# ou Visual Basic](../debugger/remote-debugging-csharp.md)|
|C++|[Depuração remota de um projeto em C++](../debugger/remote-debugging-cpp.md)|
|Aplicativos universais do Windows (UWP)|[Executar aplicativos UWP em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md) ou [depurar pacote de aplicativo instalado](../debugger/debug-installed-app-package.md)|

Se você apenas deseja baixar e instalar o depurador remoto e não precisa de quaisquer instruções adicionais para seu cenário, siga as etapas neste artigo.

## <a name="download-and-install-the-remote-tools"></a>Baixe e instale as ferramentas remotas

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="requirements_msvsmon"></a> Requisitos

[!INCLUDE [remote-debugger-requirements](../debugger/includes/remote-debugger-requirements.md)]

## <a name="fileshare_msvsmon"></a> (Opcional) Para executar o depurador remoto de um compartilhamento de arquivos

Você pode encontrar o depurador remoto (*msvsmon.exe*) em um computador com Visual Studio Community, Professional ou Enterprise já está instalado. Para alguns cenários, a maneira mais fácil de configurar a depuração remota é executar o depurador remoto (msvsmon.exe) de um compartilhamento de arquivos. Para limitações de uso, consulte a página de Ajuda do depurador remoto (**Ajuda > uso** no depurador remoto).

1. Encontre *msvsmon.exe* no diretório correspondente à versão do Visual Studio. Para Visual Studio Enterprise 2017:

      *Programa arquivos (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe*

      *Programa arquivos (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe*

2. Compartilhamento de **depurador remoto** pasta no computador do Visual Studio.

3. No computador remoto, execute *msvsmon.exe* da pasta compartilhada. Siga as [instruções de instalação](#bkmk_setup).

> [!TIP]
> Para instalação de linha de comando e referência de linha de comando, consulte a página de Ajuda *msvsmon.exe* digitando ``msvsmon.exe /?`` na linha de comando no computador com o Visual Studio instalado (ou acesse **Ajuda > uso**no depurador remoto).

## <a name="bkmk_setup"></a> Configurar o depurador remoto

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

### <a name="configure_msvsmon"></a> Configurar o depurador remoto
Você pode alterar alguns aspectos da configuração do depurador remoto depois que tiver iniciado pela primeira vez.

-   Se você precisar adicionar permissões para outros usuários se conectem ao depurador remoto, escolha **Ferramentas > permissões**. Você deve ter privilégios de administrador para conceder ou negar permissões.

     > [!IMPORTANT]
     > Você pode executar o depurador remoto em uma conta de usuário é diferente da conta de usuário que você está usando no computador do Visual Studio, mas você deve adicionar a conta de usuário diferente para permissões de usuário do depurador remoto.

     Como alternativa, você pode iniciar o depurador remoto na linha de comando com o **/Allow \<nome de usuário >** parâmetro: **msvsmon / permitir \< username@computer>**.

-   Se você precisar alterar o modo de autenticação ou o número da porta ou especificar um valor de tempo limite para as ferramentas remotas: escolha **Ferramentas > Opções**.

     Para obter uma lista dos números de porta usados por padrão, consulte [as atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md).

     > [!WARNING]
     >  Você também pode optar por executar as ferramentas remotas no Modo Sem Autenticação, mas isso é altamente desaconselhável. Nesse modo não há nenhuma segurança de rede. Escolha o modo sem autenticação somente se você tiver certeza de que a rede não está em risco de tráfego mal-intencionado ou hostil.

##  <a name="bkmk_configureService"></a> (Opcional) Configurar o depurador remoto como um serviço
Para depuração no ASP.NET e outros ambientes de servidor, você deve executar o depurador remoto como um administrador ou, se você quiser que ele sempre em execução, executar o depurador remoto como um serviço.

 Se você quiser configurar o depurador remoto como um serviço, siga estas etapas.

1. Localizar o **Assistente de configuração do depurador remoto** (rdbgwiz.exe). (Isso é um aplicativo separado do depurador remoto.) Ele está disponível apenas quando você instala as ferramentas remotas. Ele não é instalado com o Visual Studio.

2. Começar a executar o Assistente de configuração. Quando a primeira página é exibida, clique em **próxima**.

3. Verifique as **executar o depurador remoto do Visual Studio 2015, como um serviço** caixa de seleção.

4. Adicione o nome da conta de usuário e senha.

    Talvez você precise adicionar o **fazer logon como um serviço** direito de usuário dessa conta (localizar **política de segurança Local** (secpol. msc) na **iniciar** página ou janela (ou tipo  **secpol** em um prompt de comando). Quando a janela é exibida, clique duas vezes **atribuição de direitos de usuário**, em seguida, localize **fazer logon como um serviço** no painel direito. Clique duas vezes nesse item. Adicione a conta de usuário para o **propriedades** janela e clique em **Okey**). Clique em **Avançar**.

5. Selecione o tipo de rede que você deseja que as ferramentas remotas para se comunicar com. Pelo menos um tipo de rede deve ser selecionado. Se os computadores estiverem conectados por meio de um domínio, você deve escolher o primeiro item. Se os computadores estiverem conectados por meio de um grupo de trabalho ou um grupo doméstico, você deve escolher os itens de segundo ou terceiro. Clique em **Avançar**.

6. Se o serviço pode ser iniciado, você verá **concluiu com êxito o Assistente de configuração de depurador Visual remoto Studio**. Se o serviço não pode ser iniciado, você verá **Falha ao concluir o Assistente de configuração de depurador Visual remoto Studio**. A página também fornece algumas dicas a seguir para restaurar o serviço para iniciar.

7. Clique em **Finalizar**.

   Neste ponto, o depurador remoto está em execução como um serviço. Você pode verificar isso acessando **painel de controle > serviços** e procurando **depurador remoto do Visual Studio 2015**.

   Você pode parar e iniciar o serviço de depurador remoto do **painel de controle > serviços**.

## <a name="set-up-debugging-with-remote-symbols"></a>Configurar a depuração com símbolos remotos

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>Consulte também

- [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)
- [Configurar o Firewall do Windows para Depuração Remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [Atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md)
- [ASP.NET Core em um computador remoto IIS de depuração remota](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [Erros e solução de problemas de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)