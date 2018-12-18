---
title: Depuração remota de um C# ou o projeto do VB | Microsoft Docs
ms.custom:
- remotedebugging"=
- seodec18
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
ms.assetid: a9753fbb-e7f4-47f0-9dbe-9de90c6c8457
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 82873b29a173209739497087a4dfe5b293123e2c
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53055654"
---
# <a name="remote-debugging-a-c-or-visual-basic-project-in-visual-studio"></a>Depuração remota de um projeto c# ou Visual Basic no Visual Studio
Para depurar um aplicativo do Visual Studio que tenha sido implantado em um computador diferente, instalar e executar as ferramentas remotas no computador onde você implantou seu aplicativo, configure seu projeto para se conectar ao computador remoto do Visual Studio e, em seguida, executar seu aplicativo.

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
  
## <a name="remote_csharp"></a> O projeto de depuração remota
O depurador não é possível implantar aplicativos de desktop em Visual C# ou Visual Basic para um computador remoto, mas você ainda pode depurá-los remotamente da seguinte maneira. O procedimento a seguir pressupõe que você deseja para depurá-lo em um computador denominado **MJO DL**, conforme mostrado na ilustração abaixo.
  
1. Crie um projeto WPF chamado **MyWpf**.  
  
2. Defina um ponto de interrupção em algum lugar no código que é alcançado com facilidade.  
  
    Por exemplo, você pode definir um ponto de interrupção em um manipulador de botão. Para fazer isso, abra o MainWindow. XAML e adicionar um controle de botão da caixa de ferramentas, clique duas vezes no botão para abrir o manipulador de TI.
  
3. No Gerenciador de soluções, clique com botão direito no projeto e escolha **propriedades**.  
  
4. Sobre o **propriedades** , escolha o **depurar** guia.  
  
    ![RemoteDebuggerCSharp](../debugger/media/remotedebuggercsharp.png "RemoteDebuggerCSharp")  
  
5. Verifique se o **diretório de trabalho** caixa de texto está vazia.  
  
6. Escolher **usar computador remoto**e digite **MJO-DL:4022** na caixa de texto. (4022 é o número da porta mostrado na janela do depurador remoto. O número da porta incrementa 2 em cada versão do Visual Studio).
  
7. Certifique-se de que **habilitar a depuração de código nativo** não estiver selecionada.  
  
8. Compile o projeto.  
  
9. Crie uma pasta no computador remoto que é o mesmo caminho que o **Debug** pasta em seu computador do Visual Studio:  **\<caminho de origem > \MyWPF\MyWPF\bin\Debug**.  
  
10. Copie o arquivo executável que você acabou de criar do seu computador do Visual Studio para a pasta recém-criada no computador remoto.
  
    > [!CAUTION]
    >  Não faça alterações no código ou recriação (ou você deve repetir esta etapa). O executável que você copiou para o computador remoto deve corresponder exatamente, seu local de origem e símbolos.

    Você pode copiar o projeto manualmente, use Xcopy, Robocopy, Powershell ou outras opções.
  
11. Verifique se o depurador remoto está em execução no computador de destino (se não for, pesquise **depurador remoto** na **iniciar** menu). A janela do depurador remoto se parece com isso.  
  
     ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")  
  
12. No Visual Studio, inicie a depuração (**Depurar > Iniciar depuração**, ou **F5**).  
  
13. Se solicitado, insira as credenciais de rede para se conectar ao computador remoto.  
  
     As credenciais necessárias variam dependendo da configuração de segurança da sua rede. Por exemplo, em um computador de domínio, você pode inserir seu nome de domínio e senha. Em um computador fora do domínio, você pode inserir o nome do computador e um nome de conta de usuário válido, como <strong>MJO-DL\name@something.com</strong>, junto com a senha correta.

     Você deve ver que a janela principal do aplicativo do WPF está aberta no computador remoto.
  
14. Se necessário, execute a ação para o ponto de interrupção. Você deve ver que o ponto de interrupção está ativo. Caso contrário, os símbolos para o aplicativo ainda não carregado. Tente novamente e se isso não funcionar, obter informações sobre o carregamento de símbolos e como solucioná-los no [configurações de símbolo de Noções básicas sobre arquivos de símbolo e o Visual Studio](https://blogs.msdn.microsoft.com/devops/2015/01/05/understanding-symbol-files-and-visual-studios-symbol-settings/).
  
15. No computador do Visual Studio, você deve ver que a execução foi interrompido no ponto de interrupção.
  
    Se você tiver todos os arquivos não são de código que precisam ser usado pelo aplicativo, você precisará incluí-los no projeto do Visual Studio. Crie uma pasta de projeto para os arquivos adicionais (na **Gerenciador de soluções**, clique em **Adicionar > nova pasta**). Em seguida, adicione os arquivos na pasta (na **Gerenciador de soluções**, clique em **Adicionar > Item existente**, em seguida, selecione os arquivos). Sobre o **propriedades** para cada arquivo, defina **Copy to Output Directory** para **copiar sempre**.

## <a name="set-up-debugging-with-remote-symbols"></a>Configurar a depuração com símbolos remotos 

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../debugger/index.md)  
 [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)   
 [Configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md)   
 [Atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md)   
 [Depuração Remota de ASP.NET em um computador remoto IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)  
 [Erros e solução de problemas de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)