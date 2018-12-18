---
title: Remoto depurar um projeto do Visual C++ | Microsoft Docs
ms.custom: remotedebugging
ms.date: 08/14/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: 8b8eca0d-122f-4eda-848a-cf0945f207d0
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 4677380081aaa0ac79f589ea7594f19f78750613
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49844101"
---
# <a name="remote-debugging-a-visual-c-project-in-visual-studio"></a>Um projeto do Visual C++ no Visual Studio de depuração remota
Para depurar um aplicativo do Visual Studio em um computador diferente, instalar e executar as ferramentas remotas no computador onde você implantará seu aplicativo, configure seu projeto para se conectar ao computador remoto do Visual Studio e, em seguida, implantar e executar seu aplicativo.

![Componentes do depurador remoto](../debugger/media/remote-debugger-client-apps.png "Remote_debugger_components")

Para obter informações sobre aplicativos Universal do Windows (UWP) de depuração remota, consulte [depurar um pacote do aplicativo instalado](debug-installed-app-package.md).

## <a name="requirements"></a>Requisitos

O depurador remoto tem suporte no Windows 7 e mais recente (não de telefone) e versões do Windows Server a partir do Windows Server 2008 Service Pack 2. Para obter uma lista completa dos requisitos, consulte [requisitos de](../debugger/remote-debugging.md#requirements_msvsmon).

> [!NOTE]
> Não há suporte para depuração entre dois computadores conectados por meio de um proxy. Depuração em uma alta latência ou a conexão de baixa largura de banda, como dial-up da Internet, ou pela Internet entre países não é recomendado e pode falhar ou ser muito lento.
  
## <a name="download-and-install-the-remote-tools"></a>Baixe e instale as ferramentas remotas

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]
  
> [!TIP]
> Em alguns cenários, pode ser mais eficiente para executar o depurador remoto de um compartilhamento de arquivos. Para obter mais informações, consulte [executar o depurador remoto de um compartilhamento de arquivos](../debugger/remote-debugging.md#fileshare_msvsmon).
  
## <a name="BKMK_setup"></a> Configurar o depurador remoto

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> Se você precisar adicionar permissões para usuários adicionais, alterar o modo de autenticação ou número da porta para o depurador remoto, consulte [configurar o depurador remoto](../debugger/remote-debugging.md#configure_msvsmon).

## <a name="remote_cplusplus"></a> Depuração remota de um projeto do Visual C++  
 No procedimento a seguir, o nome e caminho do projeto é C:\remotetemp\MyMfc e é o nome do computador remoto **MJO DL**.  
  
1. Criar um aplicativo MFC chamado **mymfc.**  
  
2. Defina um ponto de interrupção em algum lugar no aplicativo que é atingido com facilidade, por exemplo, no **MainFrm.cpp**, no início de `CMainFrame::OnCreate`.  
  
3. No Gerenciador de soluções, clique com botão direito no projeto e selecione **propriedades**. Abra o **depuração** guia.  
  
4. Defina as **depurador a iniciar** à **depurador remoto do Windows**.  
  
    ![RemoteDebuggingCPlus](../debugger/media/remotedebuggingcplus.png "RemoteDebuggingCPlus")  
  
5. Faça as seguintes alterações nas propriedades:  
  
   |Configuração|Valor|
   |-|-|  
   |Comando remoto|C:\remotetemp\mymfc.exe|  
   |Diretório de trabalho|C:\remotetemp|  
   |Nome do servidor remoto|MJO-DL:*portnumber*|  
   |Conexão|Remoto sem Autenticação do Windows|  
   |Tipo de Depurador|Somente Nativo|  
   |Diretório de implantação|C:\remotetemp.|  
   |Arquivos adicionais a implantar|C:\data\mymfcdata.txt.|  
  
    Se você implantar arquivos adicionais (opcionais), a pasta deve existir nos dois computadores.  
  
6. No Gerenciador de soluções, clique com botão direito a solução e escolha **Configuration Manager**.  
  
7. Para o **Debug** configuração, selecione o **implantar** caixa de seleção.  
  
    ![RemoteDebugCplusDeploy](../debugger/media/remotedebugcplusdeploy.png "RemoteDebugCplusDeploy")  
  
8. Iniciar a depuração (**Depurar > Iniciar depuração**, ou **F5**).  
  
9. O executável é implantado automaticamente para o computador remoto.  
  
10. Se solicitado, insira as credenciais de rede para se conectar ao computador remoto.  
  
     As credenciais necessárias são específicas para a configuração de segurança da sua rede. Por exemplo, em um computador de domínio, você pode escolher um certificado de segurança ou insira seu nome de domínio e senha. Em um computador fora do domínio, você pode inserir o nome do computador e um nome de conta de usuário válido, como <strong>MJO-DL\name@something.com</strong>, junto com a senha correta.  
  
11. No computador do Visual Studio, você deve ver que a execução é interrompida no ponto de interrupção.  
  
    > [!TIP]
    >  Como alternativa, você pode implantar os arquivos como uma etapa separada. No **Gerenciador de soluções,** com o botão direito do **mymfc** nó e, em seguida, escolha **implantar**.  
  
    Se você tiver arquivos sem código que precisam ser usados pelo aplicativo, você precisará incluí-los no projeto do Visual Studio. Crie uma pasta de projeto para os arquivos adicionais (na **Gerenciador de soluções**, clique em **Adicionar > nova pasta**.) Em seguida, adicione os arquivos na pasta (na **Gerenciador de soluções**, clique em **Adicionar > Item existente**, em seguida, selecione os arquivos). Sobre o **propriedades** para cada arquivo, defina **Copy to Output Directory** para **copiar sempre**.
  
## <a name="set-up-debugging-with-remote-symbols"></a>Configurar a depuração com símbolos remotos 

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)] 
  
## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../debugger/index.md)  
 [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)   
 [Configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md)   
 [Atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md)   
 [Depuração Remota de ASP.NET em um computador remoto IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)  
 [Erros e solução de problemas de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)