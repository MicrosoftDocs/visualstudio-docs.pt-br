---
title: Usando ferramentas do Visual Studio para Unity | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e67ec9a2-a449-413e-8930-9a471bd43a06
caps.latest.revision: 7
author: conceptdev
ms.author: crdun
manager: ghogen
ms.openlocfilehash: a7dbe0e13691e5ac0dbf67945728bada3ef4e57f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51771306"
---
# <a name="using-visual-studio-tools-for-unity"></a>Usando o Visual Studio Tools for Unity
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Nesta seção, você aprenderá como usar os recursos de integração e produtividade das Ferramentas do Visual Studio para Unity e como usar o depurador do Visual Studio para desenvolvimento no Unity.  
  
## <a name="unity-integration-and-productivity"></a>Integração e produtividade do Unity  
 Ferramentas do Visual Studio para Unity integra-se ao Editor do Unity para ajudá-lo a ser mais produtivo. Esses recursos que melhoram a produtividade automatizam tarefas de script comum e colocam as informações do Unity no Visual Studio para que você não precise mudar para o Editor do Unity para localizá-las.  
  
### <a name="unity-documentation-access"></a>Acesso de documentação do Unity  
 Você pode acessar a documentação de script do Unity rapidamente pelo Visual Studio. Se as Ferramentas do Visual Studio para Unity não encontrarem a documentação da API localmente, elas tentarão localizá-la online.  
  
##### <a name="to-access-unity-documentation"></a>Para acessar a documentação do Unity  
  
-   No Visual Studio, destaque ou coloque o cursor sobre a API do Unity sobre a qual deseja saber mais e depois pressione **Ctrl + Alt + M, Ctrl + H**  
  
### <a name="unity-monobehavior-scripting-wizard"></a>Assistente de script do Unity MonoBehavior  
 No Unity, a maioria dos scripts são implementados ao derivar da classe MonoBehavior e substituir alguns de seus métodos. Você pode usar o Assistente do MonoBehavior para criar rapidamente definições vazias dos métodos MonoBehavior que deseja sobrecarregar. ao usar este assistente, você pode especificar um ou mais métodos que deseja sobrecarregar da lista de métodos disponíveis, selecionar onde serão inseridos no seu código e decidir se deseja incluir comentários sobre como eles são usados.  
  
 ![A caixa de diálogo Assistente de monobehavior. ](../cross-platform/media/vstu-monobehavior-wizard-full.png "vstu_monobehavior_wizard_full")  
  
##### <a name="to-create-empty-monobehavior-method-definitions-by-using-the-monobehavior-wizard"></a>Para criar definições de método MonoBehavior vazias usando o Assistente do MonoBehavior  
  
1. No Visual Studio, posicione o cursor onde quiser que os métodos sejam inseridos e pressione **Ctrl+Shift+M** para iniciar o Assistente do MonoBehavior. Ou, se você deseja inserir os novos métodos depois que um já foi implementado, é possível especificar isso posteriormente; Basta pressionar **Ctrl+Shift+M**.  
  
2. Selecione os métodos que deseja sobrecarregar. Na janela **Criar métodos de script**, em **Selecionar métodos para criar**, marque a caixa de seleção ao lado do nome de cada método para sobrecarregar.  
  
3. Certifique-se de que a versão do framework exibida na lista suspensa **Versão do Framework** corresponde à versão que você está usando. Se não corresponder, altere o valor da lista suspensa para a versão que deseja usar.  
  
4. Escolha onde os métodos serão inseridos. Por padrão, os métodos são inseridos na posição do cursor; Se desejar inseri-los em outro lugar, é possível inseri-los depois de qualquer método que já esteja implementado na classe. Para escolher um desses locais, altere o valor da lista suspensa **Ponto de inserção** para o local desejado.  
  
5. Se desejar que o Assistente gere comentários para os métodos que você selecionou, marque a caixa de seleção **Gerar comentários do método**. Esses comentários servem para ajudá-lo a entender quando o método é chamado e quais são suas responsabilidades gerais.  
  
6. Selecione o botão **OK** para sair do assistente e inserir os métodos em seu código.  
  
   O Assistente do MonoBehavior é especialmente útil enquanto ainda estiver aprendendo a API do Unity ou quando você precisar sobrecarregar um método com o qual não esteja familiarizado. Conforme você se torna experiente com a API do Unity, é possível usar o Assistente rápido do MonoBehavior para criar métodos rapidamente com os quais você já está familiarizado.  
  
#### <a name="quick-monobehavior-scripting-wizard"></a>Assistente rápido de script do MonoBehavior  
 Quando já estiver familiarizado com a API do Unity, é possível implementar métodos sobrecarregados ainda mais rapidamente usando o Assistente rápido de MonoBehavior. Ao usar este assistente, você pode especificar apenas um método que seja inserido sem comentários de método no local do cursor.  
  
 ![A caixa de diálogo Assistente rápido de monobehavior. ](../cross-platform/media/vstu-monobehavior-wizard-quick.png "vstu_monobehavior_wizard_quick")  
  
###### <a name="to-create-an-empty-monobehavior-method-definition-by-using-the-quick-monobehavior-wizard"></a>Para criar uma definição de método MonoBehavior vazia usando o Assistente rápido do MonoBehavior  
  
1.  No Visual Studio, posicione o cursor onde quiser que os métodos sejam inseridos e pressione **Ctrl+Shift+Q** para iniciar o Assistente rápido do MonoBehavior. Diferentemente outro do assistente do MonoBehavior, você deve posicionar o cursor intencionalmente ao usar esse assistente porque o novo método é sempre inserido ali.  
  
2.  Certifique-se de que a versão do framework exibida no canto superior direito da janela **Criar método de script** corresponde à versão que você está usando. Se não corresponder, altere o valor da lista suspensa para a versão que deseja usar.  
  
3.  Localize o método que deseja sobrecarregar. Na janela Criar método de script, comece digitando o nome do método na caixa de texto. Será exibida uma lista dos métodos cujos nomes correspondem ao que você inseriu.  
  
4.  selecione o método que deseja sobrecarregar. Quando o método que deseja é exibido na lista, selecione-o com as teclas de direção ou o mouse e pressione **Enter**. Se for o único método na lista, basta pressionar **Enter**. O método é inserido no seu código.  
  
### <a name="unity-project-explorer"></a>Gerenciador de Projetos do Unity  
 Você pode usar o Gerenciador de Projetos do Unity para navegar de seu projeto do Unity dentro do Visual Studio.  
  
 ![A janela do Gerenciador de Projetos do Unity.](../cross-platform/media/vstu-unity-project-explorer.png "vstu_unity_project_explorer")  
  
##### <a name="to-view-the-unity-project-explorer"></a>Para exibir o Gerenciador de Projetos do Unity  
  
- No Visual Studio, no menu principal, escolha **Exibição**, **Gerenciador de Projetos do Unity**. Teclado: **Alt+Shift+E**  
  
   ![Exibir a janela Gerenciador de Projetos do Unity. ](../cross-platform/media/vstu-view-unity-project-explorer.png "vstu_view_unity_project_explorer")  
  
  O Gerenciador de Projetos do Unity mostra todos os arquivos de projeto do Unity e diretórios da mesma forma que o Editor do Unity, isso é diferente de navegar nos scripts do Unity com o Gerenciador de Soluções, que contém somente os arquivos de script e os exibe como os projetos e a solução gerada pelas Ferramentas do Visual Studio para Unity. Especialmente em grandes projetos, geralmente, é mais fácil localizar o script que deseja modificar usando o Gerenciador de Projetos do Unity; Ele também torna mais fácil modificar outros tipos de arquivos, por exemplo, arquivos de configuração com base em texto, no Visual studio sem adicioná-los a um dos projetos na solução do Visual Studio.  
  
### <a name="unity-error-list"></a>Lista de Erros do Unity  
 Você pode exibir as mensagens do console do Unity dentro do Visual Studio quando ele estiver conectado a uma instância do Unity. Isso inclui erros e avisos do Unity. As mensagens são exibidas na janela **Lista de Erros** do Visual Studio; mensagens de erro do Unity são exibidas na guia **Erros**, as mensagens de aviso na guia **Avisos** e outras mensagens, por exemplo, as mensagens enviadas usando a API do Unity Debug. Log, são exibidas na guia **Mensagens**.  
  
 Para ver as mensagens, o projeto do Unity deve ser [Depurando seu projeto em um Player do Unity](#debugging-your-project-in-a-unity-player) para oferecer suporte à depuração de Script e para importar o pacote das Ferramentas do Visual Studio para Unity que sejam adequados para sua versão do Visual Studio e o Visual Studio deve estar [Conectando o Visual Studio para Unity](#connecting-visual-studio-to-unity).  
  
 Se não desejar visualizar erros, avisos e mensagens do Unity na janela **Lista de Erros** do Visual Studio, desabilite-os no menu Configuração.  
  
### <a name="keyboard-shortcuts"></a>Atalhos de teclado  
 Você pode acessar rapidamente a funcionalidade Ferramentas do Unity para Visual Studio usando seus atalhos de teclado. Este é um resumo dos atalhos que estão disponíveis.  
  
|Comando|Atalho|Nome de comando de atalho|  
|-------------|--------------|---------------------------|  
|Abrir o Assistente do MonoBehavior|**Ctrl+Shift+M**|**EditorContextMenus.CodeWindow.ImplementMonoBehaviours**|  
|Abrir o Assistente rápido do MonoBehavior|**Ctrl+Shift+Q**|**EditorContextMenus.CodeWindow.QuickMonoBehaviours**|  
|Abrir o Gerenciador de Projetos do Unity|**Alt+Shift+E**|**View.UnityProjectExplorer**|  
|Acessar a documentação do Unity|**Ctrl+Alt+M, Ctrl+H**|**Help.UnityAPIReference**|  
|Anexar ao depurador do Unity (player ou editor)|**_nenhum padrão_**|**Debug.AttachUnityDebugger**|  
  
 Será possível alterar as combinações de teclas de atalho se não desejar o padrão. Para obter informações sobre como mudá-las, consulte [Identificando e personalizando atalhos de teclado no Visual Studio](https://msdn.microsoft.com/library/5zwses53.aspx).  
  
## <a name="unity-debugging"></a>Depuração do Unity  
 Ferramentas do Visual Studio para Unity permitem depurar scripts do editor e jogos para seu projeto do Unity usando um depurador poderoso do Visual Studio.  
  
###  <a name="connecting-visual-studio-to-unity"></a> Conectando o Visual Studio ao Unity  
 Ferramentas do Visual Studio para Unity se comunicam com o Unity por meio de uma conexão UDP. Isso significa que você pode se conectar a uma instância do Unity em execução localmente ou em qualquer lugar na rede exatamente da mesma maneira. Você pode se conectar a qualquer uma das instâncias do Unity que puder ver na rede usando a caixa de diálogo **Selecionar instância do Unity**.  
  
##### <a name="to-open-the-select-unity-instance-dialog"></a>Para abrir a caixa de diálogo Selecionar instância do Unity  
  
-   No Visual Studio, no menu principal, escolha **Depuração**, **Anexar depurador do Unity**.  
  
     ![Anexe o depurador do Unity. ](../cross-platform/media/vstu-debugging-attach-unity-debugger.png "vstu_debugging_attach_unity_debugger")  
  
-   *Ou*, no Visual Studio, na barra de status, escolha o ícone de plugue no canto inferior direito do Visual Studio.  
  
     ![Esse ícone mostra que VSTU está conectado ao Unity. ](../cross-platform/media/vstu-connection-connected.png "vstu_connection_connected")  
  
> [!TIP]
>  Se o ícone de plugue mostrar uma marca de seleção, você já está conectado a uma instância do Unity.  
  
 A caixa de diálogo **Selecionar Instância do Unity** exibe informações sobre cada instância do Unity a que você pode se conectar.  
  
 ![Escolha uma instância do Unity à qual se conectar. ](../cross-platform/media/vstu-connection-to-unity.png "vstu_connection_to_unity")  
  
 **Projeto**  
 O nome do projeto para Unity que está sendo executado nesta instância do Unity.  
  
 **Computador**  
 O nome do computador ou dispositivo no qual essa instância do Unity está em execução.  
  
 **Tipo**  
 **Editor** se esta instância do Unity for executada como parte do Editor do Unity; **Player** se esta instância do Unity for um player autônomo.  
  
 **Porta**  
 O número da porta do soquete UDP pela qual esta instância do Unity está se comunicando.  
  
> [!IMPORTANT]
>  Como as Ferramentas do Visual Studio para Unity e a instância do Unity se comunicam por um soquete de rede UDP, o firewall pode perguntar sobre ele. Se isso acontecer, você precisará autorizar a conexão para que o VSTU e o Unity possam se comunicar.  
  
###  <a name="debugging-your-project-in-a-unity-player"></a> Depurando seu projeto em um Player do Unity  
 Você pode conectar as Ferramentas do Visual Studio para Unity diretamente ao seu aplicativo do Unity em execução em um player autônomo quando não estiver executando o Editor do Unity ou para depurar os problemas que são específicos à plataforma.  
  
##### <a name="to-enable-script-debugging-in-a-unity-player"></a>Para habilitar a depuração de scripts em um player do Unity  
  
- certifique-se de que esteja criando um build de desenvolvimento com a depuração de script habilitada. Nas configurações de build do seu projeto do Unity, marque as caixas de seleção **Build de Desenvolvimento** e **Depuração de Script**.  
  
  ![Defina as configurações de build do Unity para depuração. ](../cross-platform/media/vstu-debugging-build-settings.png "vstu_debugging_build_settings")  
  
  Além disso, para depurar um aplicativo Unity em execução no **Web Player do Unity**, também é necessário configurá-lo para usar o **Canal de versão de desenvolvimento**.  
  
##### <a name="to-configure-the-development-release-channel-in-unity-web-player"></a>Para configurar o Canal de versão de desenvolvimento no Web Player do Unity  
  
- No Web Player do Unity, no menu de contexto, escolha **Canal de Versão** e certifique-se de que a opção **Desenvolvimento** esteja habilitada.  
  
  > [!IMPORTANT]
  >  No Unity 4.2 e posterior, o item de menu de contexto **Canal de Versão** só está disponível no menu de contexto do Web Player quando a tecla **Alt** é pressionada à medida que o menu de contexto é aberto. Se o Web Player estiver sendo executado no Mac OS X, pressione a tecla **Opção**.  
  
  Finalmente, certifique-se de que você esteja conectado à instância do Unity que você deseja depurar. Para obter informações sobre como fazer isso, consulte a seção [Conectando o Visual Studio ao Unity](#connecting-visual-studio-to-unity).  
  
### <a name="debugging-a-dll-in-your-unity-project"></a>Depurando uma DLL em seu projeto do Unity  
 Muitos desenvolvedores do Unity estão escrevendo componentes de código como DLLs externas para que a funcionalidade que desenvolvem possa ser facilmente compartilhada com outros projetos. Ferramentas do Visual Studio para Unity facilitam a depuração do código nessas DLLs perfeitamente com outro código no seu projeto do Unity.  
  
> [!NOTE]
>  Neste momento, as Ferramentas do Visual Studio para Unity dá suporte somente DLLs gerenciadas. Elas não oferecem suporte à depuração de DLLs de código nativo, como aquelas escritas em C++.  
  
 Observe que o cenário descrito aqui pressupõe que você tenha o código-fonte, ou seja, se você estiver desenvolvendo ou reutilizando seu próprio código primário ou se você tiver o código-fonte em uma biblioteca de terceiros e pretender implantá-lo em seu projeto do Unity como uma DLL. Esse cenário não descreve como depurar uma DLL para a qual você não tem o código-fonte.  
  
##### <a name="to-debug-a-managed-dll-project-used-in-your-unity-project"></a>Para depurar um projeto de DLL gerenciado usado em seu projeto do Unity  
  
1. Adicione o projeto de DLL existente para a solução do Visual Studio gerada pelas Ferramentas do Visual Studio para Unity. Com menos frequência, você pode iniciar um novo projeto DLL gerenciado para conter componentes de código no seu projeto do Unity; Se esse for o caso, você poderá adicionar um novo projeto de DLL gerenciado para a solução do Visual Studio em vez disso. Para obter mais informações sobre como adicionar um projeto novo ou existente a uma solução, consulte [Como adicionar projetos a uma solução](https://msdn.microsoft.com/library/vstudio/ff460187.aspx).  
  
    ![Adicione o projeto de DLL existente à solução.](../cross-platform/media/vstu-debugging-dll-add-existing.png "vstu_debugging_dll_add_existing")  
  
    Em ambos os casos, as Ferramentas do Visual Studio para Unity mantêm a referência de projeto, mesmo se ele tiver de gerar novamente os arquivos de projeto e solução novamente, então, você precisa executar essas etapas de uma vez.  
  
2. Faça referência ao perfil de framework do Unity correto no projeto de DLL. No Visual Studio, nas propriedades do projeto DLL, defina a propriedade **Estrutura de destino** para a versão do framework do Unity que você está usando. Essa é a Biblioteca de classes base di Unity que corresponde à compatibilidade de API que seu projeto tenha como alvo, como bibliotecas de classes base completas, micro ou da Web. Isso impede que a DLL chame métodos do framework que existem em outros frameworks ou níveis de compatibilidade, mas que podem não existir na versão de framework do Unity que você está usando.  
  
    ![Defina a estrutura de destino da DLL para o framework do Unity.](../cross-platform/media/vstu-debugging-dll-target-framework.png "vstu_debugging_dll_target_framework")  
  
3. Copie a DLL para a pasta Ativos do seu projeto do Unity. No Unity, ativos são arquivos que são empacotados e implantados juntos com seu aplicativo do Unity para que eles possam ser carregados no tempo de execução. Como DLLs vinculadas no tempo de execução, elas devem ser implantadas como ativos. Para serem implantadas como um ativo, o Editor do Unity exige que as DLLs sejam colocadas dentro da pasta Ativos em seu projeto do Unity. Há duas formas de fazer isso:  
  
   - Modifique as configurações de build do seu projeto de DLL para incluir uma tarefa posterior ao build que copia os arquivos DLL e PDB de saída de sua pasta de saída para a pasta **Ativos** do seu projeto do Unity.  
  
   - Modifique as configurações de build do seu projeto de DLL para definir a pasta de saída como a pasta **Ativos** do seu projeto do Unity. Arquivos DLL e PDB serão colocados na pasta **Ativos**.  
  
     Os arquivos PDB são necessários para a depuração porque eles contêm símbolos de depuração da DLL e mapeiam o código da DLL para sua forma de código-fonte. As Ferramentas do Visual Studio para Unity usarão informações da DLL e PDB para criar um arquivo DLL.MDB, que é o formato de símbolo de depuração usado pelo mecanismo de script do Unity.  
  
4. Depure seu código. Agora você pode depurar seu código-fonte de DLL junto com o código-fonte do seu projeto do Unity e usar todos os recursos de depuração com os quais esteja acostumado, como pontos de interrupção e depuração no código.

