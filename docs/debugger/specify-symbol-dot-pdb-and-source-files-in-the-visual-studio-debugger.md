---
title: Definir o símbolo (. pdb) e os arquivos de origem no depurador
description: Saiba como configurar e gerenciar arquivos de símbolo e de origem no Visual Studio
ms.custom: ''
ms.date: 3/31/2021
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Debugger.Native
- VS.ToolsOptionsPages.Debugger.Symbols
- vs.debug.options.Native
- vs.debug.nosymbols
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- source code
- .dbg files
- source code, managing
- symbols, managing
- .pdb files
- dbg files
- pdb files
- debugger
ms.assetid: 1105e169-5272-4e7c-b3e7-cda1b7798a6b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7ad72d2aa659f3d43bfca99c359d5db94e2d1045
ms.sourcegitcommit: 155d5f0fd54ac1d20df2f5b0245365924faa3565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/31/2021
ms.locfileid: "106083674"
---
# <a name="specify-symbol-pdb-and-source-files-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>Especificar o símbolo (. pdb) e os arquivos de origem no depurador do Visual Studio (C#, C++, Visual Basic, F #)

Arquivos de banco de dados do programa (*. pdb*), também chamados de arquivos de símbolo, identificadores de mapa e instruções no código-fonte do seu projeto para identificadores correspondentes e instruções em aplicativos compilados. Esses arquivos de mapeamento vinculam o depurador ao seu código-fonte, o que habilita a depuração.

Quando você cria um projeto no IDE do Visual Studio com a configuração de compilação de depuração padrão, o compilador cria os arquivos de símbolo apropriados. Este artigo descreve como gerenciar arquivos de símbolo no IDE, por exemplo, como [especificar o local dos símbolos nas opções do depurador](#BKMK_Specify_symbol_locations_and_loading_behavior), como [verificar o status de carregamento de símbolos](#work-with-symbols-in-the-modules-window) durante a depuração e como [definir opções de símbolo no código](#compiler-symbol-options).

Para obter uma explicação detalhada dos arquivos de símbolo, consulte o seguinte:

- [Entender os arquivos de símbolo e as configurações de símbolo do Visual Studio](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)

- [Por que o Visual Studio exige arquivos de símbolo do depurador para corresponder exatamente aos arquivos binários com os quais foram criados?](/archive/blogs/jimgries/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with)

## <a name="how-symbol-files-work"></a>Como funcionam os arquivos de símbolo

O arquivo *. pdb* contém informações de depuração e estado do projeto que permitem a vinculação incremental de uma configuração de depuração de seu aplicativo. O depurador do Visual Studio usa arquivos *. pdb* para determinar duas partes-chave de informação durante a depuração:

* O nome do arquivo de origem e o número da linha a serem exibidos no IDE do Visual Studio.
* Onde o aplicativo deve parar por um ponto de interrupção.

Os arquivos de símbolo também mostram o local dos arquivos de origem e, opcionalmente, o servidor do qual recuperá-los.

O depurador só carrega arquivos *. pdb* que correspondem exatamente aos arquivos *. pdb* criados quando um aplicativo foi compilado (ou seja, os arquivos *. pdb* originais ou cópias). Essa [duplicação exata](/archive/blogs/jimgries/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with) é necessária porque o layout dos aplicativos pode ser alterado mesmo que o próprio código não tenha sido alterado.

> [!TIP]
> Para depurar código fora do código-fonte do projeto, como código do Windows ou código de terceiros que seu projeto chama, você deve especificar o local dos arquivos *. pdb* do código externo (e, opcionalmente, os arquivos de origem), que devem corresponder exatamente às compilações em seu aplicativo.

## <a name="symbol-file-locations-and-loading-behavior"></a>Localização de arquivos de símbolo e comportamento de carregamento

Quando você depura um projeto no IDE do Visual Studio, o depurador carrega automaticamente os arquivos de símbolo que estão localizados na pasta do projeto.

> [!NOTE]
> Ao depurar o código gerenciado em um dispositivo remoto, todos os arquivos de símbolo devem estar localizados no computador local ou em um local [especificado nas opções do depurador](#BKMK_Specify_symbol_locations_and_loading_behavior).

O depurador também procura arquivos de símbolo nos seguintes locais:

1. O local especificado dentro da DLL ou do arquivo executável (*. exe*).

   Por padrão, se você tiver criado uma DLL ou um arquivo *. exe* em seu computador, o vinculador colocará o caminho completo e o nome do arquivo *. pdb* associado no arquivo dll ou *. exe* . O depurador verifica se o arquivo de símbolo existe nesse local.

2. A mesma pasta que o arquivo DLL ou *. exe* .

3. Quaisquer locais especificados nas opções do depurador para arquivos de símbolo. Para adicionar e habilitar locais de símbolo, consulte [Configurar locais de símbolo e opções de carregamento](#BKMK_Specify_symbol_locations_and_loading_behavior).

   - Qualquer pasta de cache de símbolo local.

   - Locais de rede, Internet ou local especificados, como os servidores de símbolo da Microsoft, se selecionados. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] pode baixar arquivos de símbolo de depuração de servidores de símbolos que implementam o `symsrv` protocolo. O [Visual Studio Team Foundation Server](/azure/devops/pipelines/tasks/build/index-sources-publish-symbols) e as [ferramentas de depuração para Windows](/windows-hardware/drivers/debugger/index) são duas ferramentas que podem usar servidores de símbolo.

     Os servidores de símbolos que você pode usar incluem:

     **Servidores de símbolos públicos da Microsoft**: para depurar uma falha que ocorra durante uma chamada a uma DLL do sistema ou a uma biblioteca de terceiros, você geralmente precisa de arquivos System *. pdb* . Os arquivos System *. pdb* contêm símbolos para DLLs do Windows, arquivos *. exe* e drivers de dispositivo. Você pode obter símbolos para sistemas operacionais Windows, MDAC, IIS, ISA e .NET dos servidores de símbolos públicos da Microsoft.

     **Servidores de símbolos em uma rede interna ou em seu computador local**: sua equipe ou empresa pode criar servidores de símbolos para seus próprios produtos e como um cache para símbolos de fontes externas. Você pode ter um servidor de símbolo no seu próprio computador.

     **Servidores de símbolos** de terceiros: provedores de terceiros de aplicativos e bibliotecas do Windows podem fornecer acesso ao servidor de símbolos na Internet.

     > [!WARNING]
     > Se você usar um servidor de símbolos diferente dos servidores de símbolos públicos da Microsoft, verifique se o servidor de símbolos e seu caminho são confiáveis. Como os arquivos de símbolo podem conter código executável arbitrário, você pode ser exposto a ameaças de segurança.

<a name="BKMK_Specify_symbol_locations_and_loading_behavior"></a>
### <a name="configure-symbol-locations-and-loading-options"></a>Configurar locais de símbolo e opções de carregamento

Na página símbolos de depuração de opções de **ferramentas**  >    >    >   , você pode:

- Especifique e selecione caminhos de pesquisa e servidores de símbolo para Microsoft, Windows ou componentes de terceiros.
- Especifique os módulos que você deseja ou não deseja que o depurador carregue símbolos automaticamente.
- Altere essas configurações enquanto estiver Depurando ativamente. Consulte [Gerenciar símbolos durante a depuração](#manage-symbols-while-debugging).

**Para especificar locais de símbolo e opções de carregamento:**

1. No Visual Studio, abra   >  **Opções** ferramentas  >    >  **símbolos** de depuração (ou símbolos de opções de **depuração**  >    >  ).

2. Em **locais de arquivo de símbolo (. pdb)**,
   - Para usar os **servidores de símbolos da Microsoft** ou o **servidor de símbolos NuGet.org**, marque a caixa de seleção.

   - Para adicionar um novo local do servidor de símbolos,
     1. Selecione o **+** símbolo na barra de ferramentas.
     1. Digite a URL (http), o compartilhamento de rede ou o caminho local do servidor de símbolos ou o local do símbolo no campo de texto. O preenchimento de instruções ajuda você a localizar o formato correto.

     ![Ferramentas &#45; opções &#45; página de símbolos de &#45; de depuração](media/dbg-options-symbols.gif "Ferramentas &#45; opções &#45; página de símbolos de &#45; de depuração")

     >[!NOTE]
     >Somente a pasta especificada é pesquisada. Você deve adicionar entradas para todas as subpastas que deseja pesquisar.

   - Para adicionar um novo local do servidor de símbolos do VSTS,
     1. Selecione o ícone ![ferramentas&#47; opções&#47; depuração&#47;símbolos novo ícone do servidor](media/dbg_tools_options_foldersicon.png "Ferramentas &#45; opções &#45; depuração &#45; símbolos ícone novo servidor") na barra de ferramentas.
     1. Na caixa de diálogo **conectar ao servidor de símbolos do VSTS** , escolha um dos servidores de símbolo disponíveis e selecione **conectar**.

   - Para alterar a ordem de carregamento dos locais de símbolo, use **Ctrl +** + seta para **cima** e **Ctrl** + **para baixo** ou os ícones de direção para **cima** e **para baixo** .
   - Para editar uma URL ou caminho, clique duas vezes na entrada ou selecione-a e pressione **F2**.
   - Para remover uma entrada, selecione-a e, em seguida, selecione o **-** ícone.

3. Adicional Para melhorar o desempenho de carregamento de símbolos, em **cache Symbols neste diretório**, digite um caminho de pasta local para o qual os servidores de símbolos possam copiar símbolos.

   > [!NOTE]
   > Não coloque o cache de símbolo local em uma pasta protegida, como C:\Windows ou uma subpasta. Use uma pasta de leitura/gravação.

   > [!NOTE]
   > Para projetos C++, se você tiver a `_NT_SYMBOL_PATH` variável de ambiente definida, ele substituirá o valor definido em **cache Symbols neste diretório**.

4. Especifique os módulos que você deseja que o depurador carregue dos **locais do arquivo de símbolo (. pdb)** quando ele for iniciado.

   - Selecione **carregar todos os módulos, a menos que sejam excluídos** (o padrão) para carregar todos os símbolos de todos os módulos no local do arquivo de símbolo, exceto os módulos que você exclui especificamente. Para excluir determinados módulos, selecione **especificar módulos excluídos**, selecione o **+** ícone, digite os nomes dos módulos a serem excluídos e selecione **OK**.

   - Para carregar somente os módulos que você especificar nos locais de arquivo de símbolo, selecione **carregar apenas os módulos especificados**. Selecione **especificar módulos incluídos**, selecione o **+** ícone, digite os nomes dos módulos a serem incluídos e, em seguida, selecione **OK**. Os arquivos de símbolo para outros módulos não estão carregados.

5. Selecione **OK**.

## <a name="other-symbol-options-for-debugging"></a>Outras opções de símbolo para depuração

Você pode selecionar opções de símbolo adicionais em **ferramentas**  >  **Opções**  >  **depuração**  >  **geral** (ou opções de **depuração**  >    >  **geral**):

- **Carregar exportações de dll (somente nativo)**

  Carrega tabelas de exportação de DLL para C/C++. Para obter detalhes, consulte [dll Export Tables](#use-dumpbin-exports). A leitura de informações de exportação de DLL envolve alguma sobrecarga, portanto, carregar tabelas de exportação está desativado por padrão. Você também pode usar `dumpbin /exports` em uma linha de comando de compilação C/C++.

- **Habilitar a depuração de nível de endereço** e **mostrar a desmontagem se a origem não estiver disponível**

  Sempre mostra a desmontagem quando os arquivos de origem ou de símbolo não são encontrados.

  ![Opções &#47; depuração &#47; opções de desmontagem gerais](../debugger/media/dbg_options_general_disassembly_checkbox.png "Opções &#47; depuração &#47; opções de desmontagem gerais")
  <a name="BKMK_Use_symbol_servers_to_find_symbol_files_not_on_your_local_machine"></a>
- **Habilitar suporte a servidor de origem**

  Usa o servidor de origem para ajudar a depurar um aplicativo quando não há código-fonte no computador local ou o arquivo *. pdb* não corresponde ao código-fonte. O servidor de origem usa solicitações de arquivos e retorna os arquivos reais do controle do código-fonte. O servidor de origem é executado usando uma DLL chamada *srcsrv.dll* para ler o arquivo *. pdb* do aplicativo. O arquivo *. pdb* contém ponteiros para o repositório de código-fonte, bem como comandos usados para recuperar o código-fonte do repositório.

  Você pode limitar os comandos que *srcsrv.dll* podem executar no arquivo *. pdb* do aplicativo listando os comandos permitidos em um arquivo chamado *srcsrv.ini*. Coloque o arquivo de *srcsrv.ini* na mesma pasta que *srcsrv.dll* e *devenv.exe*.

  >[!IMPORTANT]
  >Comandos arbitrários podem ser inseridos no arquivo *. pdb* de um aplicativo, portanto, certifique-se de colocar apenas os comandos que deseja executar em um arquivo de *srcsrv.ini* . Qualquer tentativa de executar um comando que não esteja no arquivo *srcsvr.ini* fará com que uma caixa de diálogo de confirmação seja exibida. Para obter mais informações, consulte [aviso de segurança: o depurador deve executar o comando não confiável](../debugger/security-warning-debugger-must-execute-untrusted-command.md).
  >
  >Nenhuma validação é feita em parâmetros do comando. Portanto, tenha cuidado com comandos confiáveis. Por exemplo, se você listou *cmd.exe* em seu *srcsrv.ini*, um usuário mal-intencionado pode especificar parâmetros em *cmd.exe* que o tornaria perigoso.

  Selecione este item e os itens filho desejados. **Permitir que o servidor de origem para assemblies de confiança parcial (somente gerenciado)** e **sempre executar comandos de servidor de origem não confiáveis sem avisar** pode aumentar os riscos de segurança.

  ![Habilitar opções do servidor de origem](../debugger/media/dbg_options_general_enablesrcsrvr_checkbox.png "DBG_Options_General_EnableSrcSrvr_checkbox")

## <a name="compiler-symbol-options"></a>Opções de símbolo do compilador

Quando você cria um projeto no IDE do Visual Studio com a configuração de compilação de **depuração** padrão, o C++ e os compiladores gerenciados criam os arquivos de símbolo apropriados para seu código. Você também pode definir opções de compilador no código.

### <a name="net-options"></a>Opções do .NET

Crie com **/debug** para criar um arquivo *. pdb* . Você pode criar aplicativos com **/debug: Full** ou **/debug: pdbonly**. Compilando com **/debug: Full** gera o código depurável. A compilação com **/debug: pdbonly** gera arquivos *. pdb* , mas não gera o `DebuggableAttribute` que informa ao compilador JIT que as informações de depuração estão disponíveis. Use **/debug: pdbonly** se você quiser gerar arquivos *. pdb* para uma compilação de versão que não deseja que seja depurável. Para obter mais informações, consulte [/debug (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option) ou [/debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug).

### <a name="cc-options"></a>Opções do C/C++

- Arquivos *vc \<x> . pdb* e *\<project> . pdb*

  Um arquivo *. pdb* para C/C++ é criado quando você cria com [/Zi ou/Zi](/cpp/build/reference/z7-zi-zi-debug-information-format). No [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] , a opção [/FD](/cpp/build/reference/fd-program-database-file-name) nomeia o arquivo *. pdb* criado pelo compilador. Quando você cria um projeto no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] usando o IDE, a opção **/FD** é definida para criar um arquivo *. pdb* chamado *\<project> . pdb*.

  Se você criar seu aplicativo C/C++ usando um makefile e especificar **/Zi** ou **/Zi** sem usar **/fd**, o compilador criará dois arquivos *. pdb* :

  - *Vc \<x> . pdb*, em que *\<x>* representa a versão do compilador do Microsoft C++, por exemplo *VC11. pdb*

    O arquivo *vc \<x> . pdb* armazena todas as informações de depuração para os arquivos de objeto individuais e reside no mesmo diretório que o makefile do projeto. Cada vez que ele cria um arquivo de objeto, o compilador C/C++ mescla informações de depuração em *vc \<x> . pdb*. Portanto, mesmo que cada arquivo de origem inclua arquivos de cabeçalho comuns, como *\<windows.h>* , os TYPEDEFs desses cabeçalhos são armazenados apenas uma vez, em vez de em cada arquivo de objeto. As informações inseridas incluem informações de tipo, mas não incluem informações de símbolo como definições de função.

  - *\<project>. pdb*

    O arquivo *\<project> . pdb* armazena todas as informações de depuração para o arquivo *. exe* do projeto e reside no subdiretório *\debug* . O arquivo *\<project> . pdb* contém informações completas de depuração, incluindo protótipos de função, não apenas as informações de tipo encontradas em *vc \<x> . pdb*.

  Os arquivos *vc \<x> . pdb* e *\<project> . pdb* permitem atualizações incrementais. O vinculador também incorpora o caminho para os arquivos *. pdb* no arquivo *. exe* ou *. dll* que ele cria.

- <a name="use-dumpbin-exports"></a>Exportar tabelas de DLL

  Use `dumpbin /exports` para ver os símbolos disponíveis na tabela de exportação de uma dll. As informações simbólicas das tabelas de exportação de DLL podem ser úteis para trabalhar com mensagens do Windows, com os procedimentos do Windows (WindowProcs), objetos COM, marshaling ou qualquer DLL para a qual você não tem símbolos. Os símbolos estão disponíveis para qualquer DLL de 32 bits do sistema. As chamadas são listadas na ordem de chamada, com a função atual (a mais profundamente aninhada) na parte superior.

  Ao ler a `dumpbin /exports` saída, você pode ver os nomes de função exatos, incluindo caracteres não alfanuméricos. Ver nomes exatos de função é útil para definir um ponto de interrupção em uma função, pois os nomes de função podem ser truncados em outro lugar no depurador. Para obter mais informações, confira [dumpbin /exports](/cpp/build/reference/dash-exports).

### <a name="web-applications"></a>Aplicativos Web

Defina o arquivo de *web.config* do aplicativo ASP.net para o modo de depuração. O modo de depuração faz com que o ASP.NET gere símbolos para arquivos gerados dinamicamente e permite que o depurador se anexe ao aplicativo ASP.NET. O Visual Studio define isso automaticamente quando você começa a depurar, se você criou o projeto no modelo de projetos Web.

## <a name="manage-symbols-while-debugging"></a>Gerenciar símbolos durante a depuração

Você pode usar os **módulos**, **pilha de chamadas**, **locais**, **automáticos** ou qualquer janela de **inspeção** para carregar símbolos ou alterar opções de símbolo durante a depuração. Para obter mais informações, consulte familiarize- [se com o modo como o depurador se anexa ao seu aplicativo](../debugger/debugger-tips-and-tricks.md#modules_window).

### <a name="work-with-symbols-in-the-modules-window"></a>Trabalhar com símbolos na janela módulos

Durante a depuração, a janela **módulos** mostra os módulos de código que o depurador está tratando como código de usuário, ou meu código, e seu status de carregamento de símbolo. Você também pode monitorar o status de carregamento de símbolos, carregar símbolos e alterar opções de símbolo na janela **módulos** .

**Para monitorar ou alterar os locais de símbolos ou opções durante a depuração:**

1. Para abrir a janela **módulos** , durante a depuração, selecione **depurar**  >    >  **módulos** do Windows (ou pressione **Ctrl**  +  **ALT**  +  **U**).
1. Na janela **módulos** , clique com o botão direito do mouse no **status do símbolo** ou nos cabeçalhos do **arquivo de símbolo** ou em qualquer módulo.
1. No menu de contexto, selecione uma das seguintes opções:

|Opção|Descrição|
|------------|-----------------|
|**Carregar símbolos**|Aparece para módulos com símbolos ignorados, não encontrados ou não carregados. Tenta carregar símbolos de locais especificados na página de   >  símbolos de **depuração** de opções  >   . Se o arquivo de símbolo não for encontrado ou não for carregado, o iniciará o **Explorador de arquivos** para que você possa especificar um novo local para pesquisa.|
|**Informações de Carregamento de Símbolos**|Mostra o local de um arquivo de símbolo carregado ou os locais que foram pesquisados se o depurador não conseguir localizar o arquivo.|
|**Configurações de Símbolo**|Abre a página de símbolos de depuração de **Opções**  >    >   , onde você pode editar e adicionar locais de símbolo.|
|**Sempre Carregar Automaticamente**|Adiciona o arquivo de símbolo selecionado à lista de arquivos que são carregados automaticamente pelo depurador.|

### <a name="use-the-no-symbols-loadedno-source-loaded-pages"></a>Use os símbolos não carregados/nenhuma página carregada de origem

Há várias maneiras para o depurador dividir em código que não tem arquivos de símbolo ou de origem disponíveis:

- Passe para o código.
- Dividir em código de um ponto de interrupção ou exceção.
- Alterne para um thread diferente.
- Altere o quadro de pilha clicando duas vezes em um quadro na janela **pilha de chamadas** .

Quando isso acontece, o depurador exibe as páginas **nenhum símbolo carregado** ou **nenhuma fonte carregada** para ajudá-lo a localizar e carregar os símbolos ou a origem necessários.

 ![Página nenhum símbolo carregado](../debugger/media/dbg-nosymbolsloaded.png "DBG_NoSymbolsLoaded")

**Para usar a página de documento sem símbolos carregados para ajudar a localizar e carregar símbolos ausentes:**

- Para alterar o caminho de pesquisa, selecione um caminho não selecionado ou selecione **novo** caminho ou **novo caminho do VSTS** e insira ou selecione um novo caminho. Selecione **carregar** para pesquisar os caminhos novamente e carregar o arquivo de símbolo se ele for encontrado.
- Para substituir as opções de símbolo e repetir os caminhos de pesquisa, selecione **procurar \<executable-name> e localizar**. O arquivo de símbolo será carregado se for encontrado ou o **Explorador de arquivos** será aberto para que você possa selecionar manualmente o arquivo de símbolo.
- Para abrir a página de configurações de símbolo para configurar o comportamento, selecione **alterar configurações de símbolo** (ou escolha **Opções**  >    >  **símbolos** de depuração).
- Avançadas Para mostrar a desmontagem em uma nova janela uma vez, selecione **Exibir desmontagem** ou selecione a **caixa de diálogo opções** para definir a opção para sempre mostrar a desmontagem quando os arquivos de origem ou de símbolo não forem encontrados. Para obter mais informações, consulte [Exibir código de desmontagem](../debugger/how-to-use-the-disassembly-window.md).
- Para mostrar os locais pesquisados e o resultado, expanda **informações de carregamento de símbolo**.
- Para o código C#, você também pode optar por [descompilar o código-fonte](../debugger/decompilation.md) dos **símbolos não carregados** ou **nenhuma página carregada de origem** .

Se o depurador encontrar o arquivo *. pdb* depois de executar uma das opções e puder recuperar o arquivo de origem usando as informações no arquivo *. pdb* , ele exibirá a origem. Caso contrário, ele exibirá uma página **nenhuma fonte carregada** que descreve o problema, com links para ações que podem resolver o problema.

**Para adicionar caminhos de pesquisa de arquivo de origem a uma solução:**

Você pode especificar os locais em que o depurador pesquisa arquivos de origem e excluir arquivos específicos da pesquisa.

1. Selecione a solução em **Gerenciador de soluções** e, em seguida, selecione o ícone **Propriedades** , pressione **ALT** + **Enter**, ou clique com o botão direito do mouse e selecione **Propriedades**.

1. Selecione **depurar arquivos de origem**.

   ![Página depurar arquivos de origem](../debugger/media/dbg-source-files.png)

1. Em **diretórios que contêm código-fonte**, digite ou selecione locais de código-fonte para pesquisar. Use o ícone **nova linha** para adicionar mais locais, os ícones de seta para **cima** e para **baixo** para reordená-los ou o ícone **X** para excluí-los.

   >[!NOTE]
   >O depurador pesquisa apenas o diretório especificado. Você deve adicionar entradas para todos os subdiretórios que deseja pesquisar.

1. Em não **procurar esses arquivos de origem**, digite os nomes dos arquivos de origem a serem excluídos da pesquisa.

1. Selecione **OK** ou **aplicar**.

## <a name="see-also"></a>Confira também
- [Entender os arquivos de símbolo e as configurações de símbolo do Visual Studio](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)

- [Alterações de carregamento de símbolo remoto do .NET no Visual Studio 2012 e 2013](https://devblogs.microsoft.com/devops/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013/)