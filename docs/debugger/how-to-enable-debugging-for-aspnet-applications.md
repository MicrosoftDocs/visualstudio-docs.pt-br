---
title: Habilitar depuração para aplicativos ASP.NET | Microsoft Docs
description: Saiba como habilitar a depuração para aplicativos ASP.NET e ASP.NET Core no Visual Studio. Você pode executar o processo em um servidor de IIS Express ou em um servidor IIS local.
ms.custom: SEO-VS-2020
ms.date: 10/29/2020
ms.topic: how-to
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
manager: jmartens
ms.workload:
- aspnet
ms.openlocfilehash: 1fd620a0c7f4860421b6f8b1a15c0b708c1ba860
ms.sourcegitcommit: a0f5e7188838c5989c9cc78d99fb29bb2813501e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2021
ms.locfileid: "109729254"
---
# <a name="debug-aspnet-or-aspnet-core-apps-in-visual-studio"></a>Depurar aplicativos ASP.NET ou ASP.NET Core no Visual Studio

Você pode depurar ASP.NET e ASP.NET Core aplicativos no Visual Studio. O processo difere entre ASP.NET e ASP.NET Core e se você o executa em IIS Express ou em um servidor IIS local.

>[!NOTE]
>As etapas e configurações a seguir se aplicam somente à depuração de aplicativos em um servidor local. A depuração de aplicativos em um servidor IIS remoto usa **anexar ao processo** e ignora essas configurações. Para obter mais informações e instruções para depuração remota de aplicativos ASP.NET no IIS, consulte [depuração remota ASP.net em um computador IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md) ou [ASP.NET Core de depuração remota em um computador IIS remoto](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md).

O servidor de IIS Express interno está incluído no Visual Studio. IIS Express é o servidor de depuração padrão para projetos ASP.NET e ASP.NET Core e é pré-configurado. É a maneira mais fácil de depurar e ideal para depuração e teste inicial.

Você também pode depurar um aplicativo ASP.NET ou ASP.NET Core em um servidor IIS local (versão 8,0 ou superior) que está configurado para executar o aplicativo. Para depurar no IIS local, você deve atender aos seguintes requisitos:

<a name="iis"></a>
- Se ele não estiver instalado, instale o **ASP.net e a carga de trabalho de desenvolvimento na Web**. (Execute novamente o Instalador do Visual Studio, selecione **Modificar** e adicione essa carga de trabalho.)

   ::: moniker range="vs-2017"
   No Visual Studio 2017, procure o componente de **suporte do IIS de tempo de desenvolvimento** . Certifique-se de que ele esteja selecionado quando você adicionar a carga de trabalho.
   ::: moniker-end
- Execute o Visual Studio como administrador.
- Instale e configure corretamente o IIS com as versões apropriadas de ASP.NET e/ou ASP.NET Core. Para obter mais informações sobre como usar o IIS com ASP.NET Core, consulte [Host ASP.NET Core no Windows com o IIS](/aspnet/core/host-and-deploy/iis/index). Para ASP.NET, consulte [instalar módulos do IIS e do ASP.net](/iis/application-frameworks/scenario-build-an-aspnet-website-on-iis/configuring-step-1-install-iis-and-asp-net-modules).
- Certifique-se de que o aplicativo seja executado no IIS sem erros.

## <a name="debug-aspnet-apps"></a>Depurar ASP.NET aplicativos

IIS Express é o padrão e é pré-configurado. Se você estiver depurando no IIS Local, certifique-se de atender aos requisitos [para depuração local do IIS.](#iis)

1. Selecione o ASP.NET no Visual Studio **Gerenciador de Soluções** e clique no  ícone Propriedades ou pressione **Alt** Enter ou clique com o botão direito do mouse e + escolha **Propriedades**.

1. Selecione a **guia Web.**

1. No painel **Propriedades,** em **Servidores**,
   - Por IIS Express, selecione **IIS Express** na lista suspenso.
   - Para o IIS local,
     1. Selecione **IIS Local** no menu suspenso.
     1. Ao lado do **campo URL do** Projeto, selecione Criar Diretório **Virtual,** se você ainda não tiver definido o aplicativo no IIS.

1. Em **Depurador,** selecione **ASP.NET**.

   ![ASP.NET configurações do depurador](media/dbg-aspnet-enable-debugging2.png "ASP.NET configurações do depurador")

1. Escolha **Arquivo**  >  **Salvar Itens Selecionados** (ou pressione **Ctrl** + **S**) para salvar as alterações.

1. Para depurar o aplicativo, em seu projeto, de definir pontos de interrupção em algum código. Na barra de ferramentas Visual Studio, certifique-se de que a configuração está definida como **Depurar** e se o navegador que você deseja aparece no **IIS Express ( \<Browser name> )** ou **IIS Local ( \<Browser name> )** no campo do emulador.

1. Para iniciar a depuração, **selecione IIS Express ( \<Browser name> )** ou **IIS Local ( \<Browser name> )** na barra de ferramentas, selecione Iniciar Depuração no menu **Depurar** ou pressione  **F5**. O depurador pausa nos pontos de interrupção. Se o depurador não puder atingir os pontos de interrupção, confira [Solucionar problemas de depuração.](#troubleshoot-debugging)

## <a name="debug-aspnet-core-apps"></a>Depurar ASP.NET principais aplicativos

IIS Express é o padrão e é pré-configurado. Se você estiver depurando no IIS local, certifique-se de atender aos [requisitos para depuração local do IIS](#iis).

1. Selecione o projeto ASP.NET Core no Visual Studio **Gerenciador de soluções** , clique no ícone **Propriedades** ou pressione **ALT** + **Enter**, ou clique com o botão direito do mouse e escolha **Propriedades**.

1. Selecione a guia **Depurar**.

1. No painel **Propriedades** , ao lado de **perfil**,
   - Para IIS Express, selecione **IIS Express** na lista suspensa.
   - Para IIS local, selecione o nome do aplicativo no menu suspenso ou selecione **novo**, crie um novo nome de perfil e selecione **OK**.

1. Ao lado de **Iniciar**, selecione **IIS Express** ou **IIS** na lista suspensa.

1. Verifique se a **inicialização do navegador** está selecionada.

1. Em **variáveis de ambiente**, verifique se **ASPNETCORE_ENVIRONMENT** está presente com um valor de **desenvolvimento**. Caso contrário, selecione **Adicionar** e adicione-o.

   ![ASP.NET Core configurações do depurador](../debugger/media/dbg-aspnet-enable-debugging3.png "ASP.NET principais configurações do depurador")

1. Use **arquivo**  >  **salvar itens selecionados** ou **Ctrl** + **S** para salvar as alterações.

1. Para depurar o aplicativo, em seu projeto, defina pontos de interrupção em algum código. Na barra de ferramentas do Visual Studio, verifique se a configuração está definida como **depurar** e **IIS Express** ou o novo nome do perfil do IIS, aparece no campo emulador.

1. Para iniciar a depuração, selecione **IIS Express** ou **\<IIS profile name>** na barra de ferramentas, selecione **Iniciar Depuração** no menu **depurar** ou pressione **F5**. O depurador pausa nos pontos de interrupção. Se o depurador não puder atingir os pontos de interrupção, consulte [solucionar problemas de depuração](#troubleshoot-debugging).

## <a name="troubleshoot-debugging"></a>Solucionar problemas de depuração

Se a depuração local do IIS não puder progredir para o ponto de interrupção, siga estas etapas para solucionar o problema.

1. Inicie o aplicativo Web do IIS e certifique-se de que ele seja executado corretamente. Deixe o aplicativo Web em execução.

2. No Visual Studio, selecione **Depurar >** Anexar ao Processo ou pressione **Ctrl** Alt P e conecte-se ao processo ASP.NET ou +  + ASP.NET Core (normalmente w3wp.exe **oudotnet.exe**). Para obter mais informações, [consulte Anexar ao processo](attach-to-running-processes-with-the-visual-studio-debugger.md) e Como encontrar o nome do ASP.NET [processo](how-to-find-the-name-of-the-aspnet-process.md).

Se você puder se conectar e atingir o ponto de interrupção usando Anexar ao Processo **,** mas não usando **Depurar** Iniciar  >  **Depuração** ou **F5,** uma configuração provavelmente está incorreta nas propriedades do projeto. Se você usar um arquivo HOSTS, certifique-se de que ele também está configurado corretamente.

## <a name="configure-debugging-in-the-webconfig-file"></a>Configurar a depuração no arquivo web.config dados

ASP.NET projetos têm *web.config* arquivos por padrão, que contêm informações de configuração e de início do aplicativo, incluindo configurações de depuração. Os *web.config* arquivos devem ser configurados corretamente para depuração. As **configurações** de Propriedades nas seções anteriores *atualizam os arquivosweb.config,* mas você também pode configurá-los manualmente.

> [!NOTE]
> ASP.NET core projetos não têm inicialmente arquivosweb.config, mas  usamappsettings.jsno  elaunchSettings.jsem arquivos para informações de inicialização e configuração de aplicativo.  A implantação do aplicativo cria *web.config* arquivo ou arquivos no projeto, mas normalmente não contêm informações de depuração.

> [!TIP]
> O processo de implantação pode atualizar *asweb.config* configurações, portanto, antes de tentar depurar, certifique-se de que oweb.config *está* configurado para depuração.

**Para configurar manualmente um *arquivoweb.config* para depuração:**

1. No Visual Studio, abra o ASP.NET do projeto *web.config* arquivo.

2. *Web.config* é um arquivo XML, portanto, contém seções aninhadas marcadas por marcas. Localize a seção `configuration/system.web/compilation`. (Se o `compilation` elemento não existir, crie-o.)

3. Certifique-se de `debug` que o atributo no elemento está definido como `compilation` `true` . (Se o `compilation` elemento não contém um `debug` atributo, adicione-o e de definido como `true` .)

   Se você estiver usando o IIS local em vez do servidor de IIS Express padrão, verifique se o `targetFramework` valor do atributo no `compilation` elemento corresponde à estrutura no servidor IIS.

   O `compilation` elemento do arquivo de *web.config* deve ser semelhante ao exemplo a seguir:

   > [!NOTE]
   > Este exemplo é um arquivo de *web.config* parcial. Geralmente, há seções XML adicionais nos `configuration` elementos e `system.web` , e o `compilation` elemento também pode conter outros atributos e elementos.

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

[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] o detecta automaticamente quaisquer alterações em *web.config* arquivos e aplica as novas definições de configuração. Você não precisa reiniciar o computador ou o servidor IIS para que as alterações entrem em vigor.

Um site pode conter vários diretórios virtuais e subdiretórios, com *web.config* arquivos em cada um. [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] os aplicativos herdam as definições de configuração de *web.config* arquivos em níveis mais altos no caminho da URL. As configurações de arquivo hierárquico *web.config* se aplicam a todos os [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativos abaixo delas na hierarquia. Definir uma configuração diferente em um arquivo de *web.config* inferior na hierarquia substitui as configurações no arquivo superior.

Por exemplo, se você especificar `debug="true"` no <em>www.Microsoft.com/AAA/web.config</em>, qualquer aplicativo na pasta *AAA* ou em qualquer subpasta de *AAA* herda essa configuração, exceto se um desses aplicativos substituir a configuração pelo seu próprio arquivo de *web.config* .

## <a name="publish-in-debug-mode-using-the-file-system"></a>Publicar no modo de depuração usando o sistema de arquivos

Há diferentes maneiras de publicar aplicativos no IIS. Estas etapas mostram como criar e implantar um perfil de publicação de depuração usando o sistema de arquivos. Para fazer isso, você deve estar executando o Visual Studio como administrador.

> [!IMPORTANT]
> Se você alterar seu código ou recompilar, deverá repetir essas etapas para republicar.

1. No Visual Studio, clique com o botão direito do mouse no projeto e escolha **publicar**.

3. Escolha **IIS, FTP, etc.** e clique em **publicar**.

    ![Captura de tela da caixa de diálogo escolher um destino de publicação no Visual Studio. Um IIS, FTP Implantação da Web é selecionado e o botão publicar é realçado.](media/dbg-aspnet-local-iis.png)

4. Na caixa **de diálogo CustomProfile,** para **Método de publicação,** escolha **Sistema de arquivos**.

5. Para **Local de destino,** selecione **Procurar** (**...**).

   - Por ASP.NET, selecione **IIS Local,** selecione o site que você criou para o aplicativo e, em seguida, **selecione Abrir**.

     ![Publicar no ASP.NET no IIS](media/dbg-aspnet-local-iis1.png "Publicar ASP.NET no IIS")

   - Para ASP.NET Core, **selecione** Sistema de Arquivos , selecione a pasta configurada para o aplicativo e, em seguida, selecione **Abrir**.

1. Selecione **Avançar**.

1. Em **Configuração,** selecione **Depurar** no menu suspenso.

1. Selecione **Salvar**.

1. Na caixa **de** diálogo Publicar, certifique-se de que **CustomProfile** (ou o nome do perfil que você acabou de criar) seja exibido e **LastUsedBuildConfiguration** esteja definido como **Depurar**.

1. Selecione **Publicar**.

    ![Captura de tela da caixa de diálogo Publicar, com o aplicativo CustomProfile selecionado, o botão Publicar realçada e LastBuildConfiguration definido como Depuração.](media/dbg-aspnet-local-iis-select-site.png)

> [!IMPORTANT]
> O modo de depuração reduz consideravelmente o desempenho do aplicativo. Para melhor desempenho, de acordo com oweb.confige especifique um build de versão ao implantar um aplicativo de produção ou `debug="false"` realizar medidas de desempenho. 

## <a name="see-also"></a>Consulte também
- [Depuração do ASP.NET: requisitos do sistema](aspnet-debugging-system-requirements.md)
- [Como executar o processo de trabalho em uma conta de usuário](how-to-run-the-worker-process-under-a-user-account.md)
- [Como localizar o nome do processo ASP.NET](how-to-find-the-name-of-the-aspnet-process.md)
- [Depurar aplicativos Web implantados](debugging-deployed-web-applications.md)
- [Passo a passo: depurando um formulário da Web](walkthrough-debugging-a-web-form.md)
- [Como depurar exceções do ASP.NET](how-to-debug-aspnet-exceptions.md)
- [Depurar aplicativos Web: erros e solução de problemas](debugging-web-applications-errors-and-troubleshooting.md)
