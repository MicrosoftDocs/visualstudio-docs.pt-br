---
title: Habilitar a depuração para aplicativos ASP.NET | Microsoft Docs
ms.custom: H1HackMay2017
ms.date: 09/21/18
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging ASP.NET Web applications
- Web.config configuration file, debug mode
- debugging [Visual Studio], ASP.NET
ms.assetid: 3beed819-cece-4864-8184-bd410000973a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 41da2eb360bac4c50f85bd908f980f5ee3c1d141
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49813410"
---
# <a name="debug-aspnet-or-aspnet-core-apps-in-visual-studio"></a>Depurar aplicativos ASP.NET ou ASP.NET Core no Visual Studio

Você pode depurar aplicativos ASP.NET e ASP.NET Core no Visual Studio. O processo é diferente entre o ASP.NET e ASP.NET Core, e se você executá-lo no IIS Express ou um servidor IIS local. 

>[!NOTE]
>As seguintes etapas e configurações se aplicam somente a depuração de aplicativos em um servidor local. Servidor de depuração de aplicativos em um IIS remoto usa **anexar ao processo**e ignora essas configurações. Para obter mais informações e instruções para depuração remota de ASP.NET aplicativos no IIS, consulte [depuração remota ASP.NET em um computador IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md) ou [ASP.NET Core de depuração remota em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md).

O servidor interno do IIS Express é incluído com o Visual Studio. O IIS Express é o servidor de depuração padrão para projetos do ASP.NET e ASP.NET Core e é pré-configurado. É a maneira mais fácil para depurar e ideal para depuração e teste inicial. 

Você também pode depurar um aplicativo ASP.NET ou ASP.NET Core em um servidor IIS local (versão 8.0 ou superior) que está configurado para executar o aplicativo. Para depurar no IIS local, você deve atender aos seguintes requisitos: 

<a name="iis"></a>
- Selecione **tempo de desenvolvimento, suporte ao IIS** durante a instalação do Visual Studio. (Se necessário, execute novamente o instalador do Visual Studio, selecione **modificar**e adicionar esse componente.)
- Estar executando o Visual Studio como administrador. 
- Instalar e configurar corretamente o IIS com as versões apropriadas do ASP.NET e/ou ASP.NET Core. Para obter mais informações e instruções, consulte [IIS 8.0 usando ASP.NET 3.5 e ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) ou [Host ASP.NET Core no Windows com o IIS](https://docs.microsoft.com/aspnet/core/host-and-deploy/iis/index).
- Verifique se que o aplicativo é executado no IIS sem erros.

## <a name="debug-aspnet-apps"></a>Depurar aplicativos ASP.NET 

O IIS Express é o padrão e é pré-configurado. Se você estiver depurando no IIS Local, verifique se você atende a [requisitos para depuração local do IIS](#iis). 

1. Selecione o projeto do ASP.NET no Visual Studio **Gerenciador de soluções** e clique no **Properties** ícone, pressione **Alt**+**Enter**, ou clique com botão direito e escolha **propriedades**.
   
1. Selecione o **Web** guia.
   
1. No **propriedades** painel, em **servidores**, 
   - Para o IIS Express, selecione **IIS Express** na lista suspensa.
   - Para o IIS local,
     1. Selecione **IIS Local** na lista suspensa.
     1. Ao lado de **URL do projeto** campo, selecione **criar diretório Virtual**, se você ainda não configurou o aplicativo no IIS.
   
1. Sob **depuradores**, selecione **ASP.NET**.
   
   ![As configurações do depurador ASP.NET](media/dbg-aspnet-enable-debugging2.png "as configurações do depurador ASP.NET")
   
1. Use **arquivo** > **salvar itens selecionados** ou **Ctrl**+**S** para salvar as alterações. 
   
1. Para depurar o aplicativo, em seu projeto, definir pontos de interrupção no código. Na barra de ferramentas do Visual Studio, verifique se a configuração é definida como **Debug**, e o navegador que você deseja é exibido na **IIS Express (\<nome do navegador >)** ou **IIS Local (\< Nome do navegador >)** no campo de emulador. 
   
1. Para iniciar a depuração, selecione **IIS Express (\<nome do navegador >)** ou **IIS Local (\<nome do navegador >)** na barra de ferramentas, selecione **iniciar depuração**partir de **depurar** menu, ou pressione **F5**. O depurador faz uma pausa nos pontos de interrupção. Se o depurador não pode atingir os pontos de interrupção, consulte [solucionar problemas de depuração](#troubleshoot-debugging).

## <a name="debug-aspnet-core-apps"></a>Depurar aplicativos ASP.NET Core 

O IIS Express é o padrão e é pré-configurado. Se você estiver depurando no IIS Local, verifique se você atende a [requisitos para depuração local do IIS](#iis). 

1. Selecione o projeto do ASP.NET Core no Visual Studio **Gerenciador de soluções** e clique no **Properties** ícone, pressione **Alt**+**Enter**, ou clique com botão direito e escolha **propriedades**.

1. Selecione a guia **Depurar**.
   
1. No **propriedades** painel, ao lado **perfil**, 
   - Para o IIS Express, selecione **IIS Express** na lista suspensa.
   - Para o IIS local, selecione o nome do aplicativo na lista suspensa ou selecione **New**, crie um novo nome de perfil e selecione **Okey**.
   
1. Lado **inicie**, selecione **IIS Express** ou **IIS** na lista suspensa. 
   
1. Certifique-se **Iniciar navegador** está selecionado.
   
1. Sob **variáveis de ambiente**, verifique se **ASPNETCORE_ENVIRONMENT** está presente com um valor de **desenvolvimento**. Se não, selecione **adicionar** e adicioná-lo.
   
   ![Configurações do depurador do ASP.NET Core](../debugger/media/dbg-aspnet-enable-debugging3.png "configurações do depurador do ASP.NET Core")
   
1. Use **arquivo** > **salvar itens selecionados** ou **Ctrl**+**S** para salvar as alterações. 
   
1. Para depurar o aplicativo, em seu projeto, definir pontos de interrupção no código. Na barra de ferramentas do Visual Studio, verifique se a configuração é definida como **Debug**e qualquer **IIS Express**, ou o novo nome de perfil do IIS, é exibido no campo de emulador. 
   
1. Para iniciar a depuração, selecione **IIS Express** ou  **\<nome do perfil do IIS >** na barra de ferramentas, selecione **iniciar depuração** do **depurar** menu, ou pressione **F5**. O depurador faz uma pausa nos pontos de interrupção. Se o depurador não pode atingir os pontos de interrupção, consulte [solucionar problemas de depuração](#troubleshoot-debugging).

## <a name="troubleshoot-debugging"></a>Solucionar problemas de depuração

Se a depuração de IIS local não pode Avançar para o ponto de interrupção, siga estas etapas para solucionar problemas. 

1. Inicie o aplicativo web do IIS e certificar-se de que ele seja executado corretamente. Deixe o aplicativo web em execução.
   
2. No Visual Studio, selecione **Depurar > Anexar ao processo** ou pressione **Ctrl**+**Alt**+**P**, e conectar-se ao processo do ASP.NET ou ASP.NET Core (normalmente **w3wp.exe** ou **dotnet.exe**). Para obter mais informações, consulte [anexar ao processo](attach-to-running-processes-with-the-visual-studio-debugger.md) e [como localizar o nome do processo do ASP.NET](how-to-find-the-name-of-the-aspnet-process.md).

Se você pode conectar-se e atingir o ponto de interrupção usando **anexar ao processo**, mas não usando **Debug** > **iniciar depuração** ou **F5**, uma configuração provavelmente está incorreta nas propriedades do projeto. Se você usar um arquivo de HOSTS, certifique-se de que também está configurado corretamente.

## <a name="configure-debugging-in-the-webconfig-file"></a>Configurar a depuração no arquivo Web. config  

Projetos do ASP.NET possuem *Web. config* arquivos por padrão, que contêm os dois configuração e inicialização informações do aplicativo, incluindo configurações de depuração. O *Web. config* arquivos devem ser configurados corretamente para depuração. O **propriedades** configurações de atualização de seções anteriores a *Web. config* arquivos, mas você também pode configurá-las manualmente. 

> [!NOTE]
> Projetos do ASP.NET Core não têm inicialmente *Web. config* arquivos, mas use *appSettings. JSON* e *launchsettings. JSON* arquivos de configuração do aplicativo e inicialização informações. Implantar o aplicativo cria uma *Web. config* arquivo ou arquivos no projeto, mas eles normalmente não contêm informações de depuração.

> [!TIP]
> O processo de implantação pode atualizar o *Web. config* configurações, portanto, antes de tentar a depuração, verificam se o *Web. config* está configurado para depuração.
  
**Para configurar manualmente uma *Web. config* arquivo para depuração:**

1. No Visual Studio, abra o projeto do ASP.NET *Web. config* arquivo.  
  
2. *Web. config* é um arquivo XML, portanto, contém as seções aninhadas marcadas por aspas. Localize o `configuration/system.web/compilation` seção. (Se o `compilation` elemento não existir, crie-o.)
  
3. Certifique-se de que o `debug` de atributo na `compilation` é definido como `true`. (Se o `compilation` elemento não contém uma `debug` do atributo, adicioná-lo e defina-o como `true`.) 
  
   Se você estiver usando o IIS local em vez do servidor de IIS Express padrão, verifique se o `targetFramework` valor no atributo de `compilation` elemento coincide com a estrutura no servidor IIS.
  
   O `compilation` elemento do *Web. config* arquivo deve ser semelhante ao seguinte exemplo:

   > [!NOTE]
   > Este exemplo é um parcial *Web. config* arquivo. Há seções adicionais geralmente XML o `configuration` e `system.web` elementos e o `compilation` elemento também pode conter outros elementos e atributos.
  
   ```xml
   <configuration>  
      ...  
      <system.web>  
          <compilation  debug="true"  targetFramework="4.6.1" ... > 
             ...  
          </compilation>  
      </system.web>  
   </configuration>  
   ```

[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] detecta automaticamente qualquer alteração feita *Web. config* arquivos e aplica as novas definições de configuração. Você não precisa reiniciar o computador ou o servidor IIS para que as alterações entrem em vigor.  
  
Um site pode conter vários diretórios e subdiretórios virtuais, com *Web. config* arquivos em cada um deles. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativos herdam definições de configuração de *Web. config* arquivos em níveis mais altos no caminho da URL. O hierárquica *Web. config* configurações do arquivo se aplicam a todos os [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativos abaixo na hierarquia. Definindo uma configuração diferente uma *Web. config* inferiores na hierarquia do arquivo substituirá as configurações no arquivo de mais alto.  
  
Por exemplo, se você especificar `debug="true"` na <em>www.microsoft.com/aaa/web.config</em>, qualquer aplicativo na *aaa* pasta ou qualquer subpasta *aaa* herdará essa configuração, exceto se um desses aplicativos substitui a configuração com sua própria *Web. config* arquivo.  
  
## <a name="publish-in-debug-mode-using-the-file-system"></a>Publicar no modo de depuração usando o sistema de arquivos

Há várias maneiras de publicar aplicativos para o IIS. Estas etapas mostram como criar e implantar um perfil de publicação usando o sistema de arquivos de depuração. Para fazer isso, você deve estar executando o Visual Studio como administrador. 

> [!IMPORTANT]
> Se você alterar seu código ou recompilação, você deve repetir estas etapas para publicar novamente. 

1. No Visual Studio, clique com botão direito no projeto e escolha **publicar**.

3. Escolher **IIS, FTP, etc** e clique em **publicar**.

    ![Publicar no IIS](media/dbg-aspnet-local-iis.png "publicar no IIS")

4. No **CustomProfile** caixa de diálogo, para **método de publicação**, escolha **sistema de arquivos**.

5. Para **local de destino**, selecione **procurar** (**...** ).
   
   - Para o ASP.NET, selecione **Local IIS**, selecione o site que você criou para o aplicativo e, em seguida, selecione **abrir**.
     
     ![Publicar para o ASP.NET no IIS](media/dbg-aspnet-local-iis1.png "publicar ASP.NET no IIS")
     
   - Para o ASP.NET Core, selecione **sistema de arquivos**, selecione a pasta que você configurar para o aplicativo e, em seguida, selecione **abrir**.

1. Selecione **Avançar**. 

1. Sob **Configuration**, selecione **depurar** na lista suspensa.

1. Selecione **Salvar**.

1. No **Publish** caixa de diálogo, certifique-se **CustomProfile** (ou o nome do perfil que você acabou de criar) for exibida, e **LastUsedBuildConfiguration** é definido como  **Depurar**. 

1. Selecione **Publicar**.

    ![Publicar no IIS](media/dbg-aspnet-local-iis-select-site.png "publicar no IIS")

> [!IMPORTANT]
> Modo de depuração reduz consideravelmente o desempenho do seu aplicativo. Para melhor desempenho, defina `debug="false"` no *Web. config* e especificar um build de versão quando você implanta um aplicativo de produção ou conduzir medidas de desempenho.  

## <a name="see-also"></a>Consulte também  
[Depuração do ASP.NET: requisitos do sistema](aspnet-debugging-system-requirements.md)   
[Como: executar o processo de trabalho em uma conta de usuário](how-to-run-the-worker-process-under-a-user-account.md)   
[Como: localizar o nome do processo do ASP.NET](how-to-find-the-name-of-the-aspnet-process.md)   
[Depurar aplicativos web implantados](debugging-deployed-web-applications.md)   
[Passo a passo: Depurando um formulário da web](walkthrough-debugging-a-web-form.md)   
[Como: depurar exceções do ASP.NET](how-to-debug-aspnet-exceptions.md)   
[Depurar aplicativos web: erros e solução de problemas](debugging-web-applications-errors-and-troubleshooting.md)
  
