---
title: Defina o símbolo (. PDB) e arquivos de origem no depurador
ms.custom: seodec18
ms.date: 10/08/2018
ms.technology: vs-ide-debug
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6ba2f7794b052712d35bbdadb02a0ea8551dc78b
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53060440"
---
# <a name="specify-symbol-pdb-and-source-files-in-the-visual-studio-debugger-c-c-visual-basic-f"></a>Especificar o símbolo (. PDB) e arquivos de origem no depurador do Visual Studio (C#, C++, Visual Basic, F#)

Banco de dados do programa (*. PDB*) arquivos, também chamados de arquivos de símbolo, mapeiam identificadores e as instruções no código-fonte do seu projeto para identificadores correspondentes e as instruções no compilado aplicativos. 

Quando você compila um projeto do IDE do Visual Studio com o padrão de configuração de build de depuração, o compilador cria os arquivos de símbolo apropriado. Você também pode [definir as opções de símbolo no código](#compiler-symbol-options). 

O *. PDB* arquivo contém informações de estado do projeto e de depuração que permite a vinculação incremental de uma configuração de depuração do seu aplicativo. O depurador do Visual Studio usa *. PDB* arquivos para determinar duas informações cruciais durante a depuração:

* O arquivo de origem nome e a linha número para exibir no IDE do Visual Studio.
* Onde no aplicativo para ser interrompido por um ponto de interrupção.

Arquivos de símbolo também mostram o local dos arquivos de origem e, opcionalmente, recuperá-los do servidor.
  
O depurador carrega apenas *. PDB* arquivos que correspondem exatamente a *. PDB* arquivos criados quando um aplicativo foi compilado (ou seja, o original *. PDB* arquivos ou cópias). Essa duplicação exata é necessária porque o layout de aplicativos pode ser alterado, mesmo se o código em si não foi alterado. Para obter mais informações, consulte [por que o Visual Studio exige arquivos de símbolo do depurador para corresponder exatamente os arquivos binários que eles foram criados?](https://blogs.msdn.microsoft.com/jimgries/2007/07/06/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with/)

> [!TIP]
> Para depurar o código fora do código-fonte seu projeto, como suas chamadas de projeto de código de terceiros ou código do Windows, você deve especificar o local do código externo *. PDB* arquivos (e, opcionalmente, os arquivos de origem), que deve corresponder exatamente a as compilações em seu aplicativo. 

## <a name="symbol-file-locations-and-loading-behavior"></a>Locais de arquivo e o comportamento de carregamento de símbolo

> [!NOTE]
> Quando estiver depurando código gerenciado em um dispositivo remoto, todos os arquivos de símbolo devem estar localizados no computador local ou em um local [especificado nas opções do depurador](#BKMK_Specify_symbol_locations_and_loading_behavior).  
  
Quando você depura um projeto no IDE do Visual Studio, o depurador carrega automaticamente os arquivos de símbolo que estão localizados na pasta do projeto. 

Além disso, o depurador procura por arquivos de símbolo nos seguintes locais:

1. O local especificado dentro da DLL ou executável (*.exe*) arquivos.  
   
   Por padrão, se você tiver criado uma DLL ou um *.exe* arquivo no seu computador, o vinculador coloca o caminho completo e nome de arquivo do associado *. PDB* arquivo na DLL ou *.exe* arquivo. O depurador verifica para ver se o arquivo de símbolo existe nesse local.  
   
2. A mesma pasta que a DLL ou *.exe* arquivo.
   
3. Qualquer locais especificados nas opções do depurador para arquivos de símbolo. Para adicionar e habilitar os locais de símbolos, consulte [configurar locais de símbolos e opções de carregamento](#BKMK_Specify_symbol_locations_and_loading_behavior). 
   
   - Qualquer pasta de cache de símbolo local.  
  
   - Rede especificada, internet, ou servidores de símbolo local e locais, como servidores de símbolo da Microsoft, se selecionado. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] pode baixar arquivos de símbolo de depuração dos servidores de símbolo que implementam o `symsrv` protocolo. [Visual Studio Team Foundation Server](/azure/devops/pipelines/tasks/build/index-sources-publish-symbols) e o [ferramentas de depuração para Windows](/windows-hardware/drivers/debugger/index) são duas ferramentas que podem usar servidores de símbolo.
      
     Servidores de símbolo, que você pode usar incluem:  
      
     **Servidores de símbolo públicos da Microsoft**: Para depurar uma falha que ocorre durante uma chamada para uma DLL do sistema ou em uma biblioteca de terceiros, você geralmente precisa de sistema *. PDB* arquivos. Sistema *. PDB* arquivos contêm símbolos para DLLs do Windows *.exe* arquivos e drivers de dispositivo. Você pode obter os símbolos para sistemas de operacionais do Windows, MDAC, IIS, ISA e o [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] dos servidores de símbolo Microsoft públicos. 
      
     **Servidores de símbolo em uma rede interna ou no computador local**: Sua equipe ou empresa pode criar servidores de símbolo para seus próprios produtos e como um cache para símbolos de fontes externas. Você pode ter um servidor de símbolo no seu próprio computador. 
      
     **Servidores de símbolo de terceiros**: Provedores de terceiros de aplicativos e bibliotecas do Windows podem fornecer acesso ao servidor de símbolo na Internet. 
    
     > [!WARNING]
     > Se você usar um servidor de símbolos que não seja a servidores públicos de símbolos da Microsoft, certifique-se de que o servidor de símbolos e seu caminho são confiáveis. Como arquivos de símbolo podem conter códigos executáveis arbitrários, você pode ser exposto às ameaças de segurança.  

<a name="BKMK_Specify_symbol_locations_and_loading_behavior"></a>
### <a name="configure-symbol-locations-and-loading-options"></a>Configurar opções de carregamento e locais de símbolos

Sobre o **ferramentas** > **opções** > **depuração** > **símbolos** página, você pode:

- Especifique e selecione caminhos de pesquisa e os servidores de símbolo Microsoft, Windows ou componentes de terceiros.
- Especifique que você deseja fazer ou não deseja que o depurador para automaticamente carregar símbolos para os módulos.
- Altere essas configurações enquanto você estiver depurando ativamente. Ver [gerenciar símbolos durante a depuração](#manage-symbols-while-debugging). 
  
**Para especificar locais de símbolos e opções de carregamento:**

1. No Visual Studio, abra **ferramentas** > **opções** > **depuração** > **símbolos** (ou **Debug** > **opções** > **símbolos**).  
   
   ![Ferramentas &#45; opções &#45; depuração &#45; página de símbolos](media/dbg-options-symbols.png "ferramentas &#45; opções &#45; depuração &#45; página de símbolos")  
   
2. Sob **locais de arquivo (. PDB) de símbolo**,
   - Para usar o **servidores de símbolo Microsoft**, marque a caixa de seleção.  
   
   - Para adicionar um novo local de servidor do símbolo
     1. Selecione o **+** símbolo na barra de ferramentas. 
     1. Digite o caminho de URL ou pasta do servidor de símbolos ou local do símbolo no campo de texto. O preenchimento de instruções ajuda você a localizar o formato correto.
     
     >[!NOTE]
     >Somente a pasta especificada é pesquisada. Você deve adicionar entradas para todas as subpastas que você deseja pesquisar.  
   
   - Para adicionar um novo local do servidor de símbolos do VSTS, 
     1. Selecione o ![ferramentas&#47; opções&#47; depuração&#47;ícone novo do servidor de símbolos](media/dbg_tools_options_foldersicon.png "ferramentas &#45; opções &#45; depuração &#45; novo ícone de servidor de símbolos") ícone na barra de ferramentas. 
     1. No **conectar-se ao servidor de símbolos do VSTS** caixa de diálogo, escolha um dos servidores de símbolo disponíveis e selecione **Connect**.  
   
   - Para alterar a ordem de carregamento para os locais de símbolos, use **Ctrl**+**backup** e **Ctrl**+**para baixo**, ou o **para cima** e **para baixo** ícones de seta. 
   - Para editar uma URL ou caminho, duas vezes na entrada, ou selecione-o e pressione **F2**.  
   - Para remover uma entrada, selecione-o e, em seguida, selecione a **-** ícone.
  
3. (Opcional) Para melhorar o desempenho de carregamento de símbolo, sob **armazenar em Cache os símbolos neste diretório**, digite um caminho de pasta local que servidores de símbolo podem copiar símbolos para.  
  
   > [!NOTE]
   > Não coloque o cache de símbolo local em uma pasta protegida, como C:\Windows ou em uma subpasta. Use uma pasta de leitura/gravação.  
  
   > [!NOTE]
   > Para projetos do C++, se você tiver o `_NT_SYMBOL_PATH` conjunto de variáveis de ambiente, ele substituirá o valor definido em **armazenar em Cache os símbolos neste diretório**.
  
4. Especificar os módulos que você deseja que o depurador para carregar a partir de **símbolo locais de arquivo (. PDB)** quando ele for iniciado.  
  
   -  Selecione **carregar todos os módulos, a menos que excluídos** (o padrão) para carregar todos os símbolos para todos os módulos no local do arquivo de símbolo, exceto excluir especificamente os módulos. Para excluir determinados módulos, selecione **especificar módulos excluídos**, selecione o **+** ícone, digite os nomes dos módulos a serem excluídos e, em seguida, selecione **Okey**.  
  
   -  Para carregar somente os módulos que você especificar os símbolo locais de arquivos, selecione **carregar somente os módulos especificados**. Selecione **especificar módulos incluídos**, selecione o **+** ícone, digite os nomes dos módulos para incluir e, em seguida, selecione **Okey**. Os arquivos de símbolo para outros módulos não são carregados.  
  
5. Selecione **OK**.

## <a name="other-symbol-options-for-debugging"></a>Outras opções de símbolo de depuração
  
Você pode selecionar opções adicionais de símbolo na **ferramentas** > **opções** > **depuração** > **geral** (ou **Debug** > **opções** > **geral**):  

- **Carregar exportações de dll (somente Nativas)**  
  
  Carrega o DLL exportar tabelas para C/C++. Para obter detalhes, consulte [DLL exportar tabelas](#use-dumpbin-exports). Informações de exportação de DLL de leitura envolve alguma sobrecarga, o carregamento de tabelas de exportação é desativado por padrão. Você também pode usar `dumpbin /exports` em uma linha de comando de compilação do C/C++.  
  
- **Habilitar a depuração no nível do endereço** e **Mostrar desmontagem se a fonte não disponível**  
  
  Sempre mostra a desmontagem quando os arquivos de origem ou de símbolo não forem encontrados.  
  
  ![Opções de &#47; depuração &#47; opções gerais de desmontagem](../debugger/media/dbg_options_general_disassembly_checkbox.png "opções &#47; depuração &#47; opções gerais de desmontagem")  
  <a name="BKMK_Use_symbol_servers_to_find_symbol_files_not_on_your_local_machine"></a>
- **Habilitar suporte a servidor de origem**  
  
  Usa o servidor de origem para ajudar a depurar um aplicativo quando não há nenhum código-fonte no computador local, ou o *. PDB* arquivo não coincide com o código-fonte. Servidor de origem recebe solicitações de arquivos e retorna os arquivos reais do controle de origem. Servidor de origem é executado por meio de uma DLL denominada *SRCSRV* para ler do aplicativo *. PDB* arquivo. O *. PDB* arquivo contém ponteiros para o repositório de código-fonte, bem como os comandos usados para recuperar o código-fonte do repositório. 
  
  Você pode limitar os comandos que *SRCSRV* pode executar a partir do aplicativo *. PDB* arquivo listando os comandos permitidos em um arquivo chamado *SRCSRV. ini*. Coloque o *SRCSRV. ini* arquivo na mesma pasta que *SRCSRV* e *devenv.exe*.  
  
  >[!IMPORTANT]
  >Comandos arbitrários podem ser inseridos em um aplicativo *. PDB* de arquivos, portanto, certifique-se de colocar somente os comandos que você deseja executar em um *SRCSRV. ini* arquivo. Qualquer tentativa de executar um comando que não esteja no arquivo *srcsvr.ini* fará com que uma caixa de diálogo de confirmação seja exibida. Para obter mais informações, consulte [aviso de segurança: O depurador deve executar o comando não confiável](../debugger/security-warning-debugger-must-execute-untrusted-command.md). 
  >
  >Nenhuma validação é feita em parâmetros do comando. Portanto, tenha cuidado com comandos confiáveis. Por exemplo, se você listou *cmd.exe* no seu *SRCSRV. ini*, um usuário mal-intencionado pode especificar parâmetros na *cmd.exe* seria mais perigoso.  
  
  Selecione este item e os itens filho que deseja. **Permitir que o servidor de origem para os assemblies de confiança parcial (somente gerenciado)** e **sempre executar comandos do servidor de origem não confiável, sem avisar** pode aumentar os riscos de segurança.  
  
  ![Habilitar opções de servidor de origem](../debugger/media/dbg_options_general_enablesrcsrvr_checkbox.png "DBG_Options_General_EnableSrcSrvr_checkbox")  

## <a name="compiler-symbol-options"></a>Opções do compilador do símbolo  

Quando você compila um projeto do IDE do Visual Studio com o padrão **depurar** configuração de build, o C++ e os compiladores gerenciados criam os arquivos de símbolos apropriados para seu código. Você também pode definir opções do compilador no código. 

### <a name="cc-options"></a>Opções do C/C++ 

- *VC\<x >. PDB* e  *\<projeto >. PDB* arquivos
  
  Um *. PDB* do arquivo para C/C++ é criado quando você compila com [/ZI ou /Zi](/cpp/build/reference/z7-zi-zi-debug-information-format). Na [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)], o [/Fd](/cpp/build/reference/fd-program-database-file-name) nomes de opção a *. PDB* arquivo, o compilador cria. Quando você cria um projeto no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] usando o IDE, o **/Fd** opção é definida para criar um *. PDB* arquivo chamado  *\<projeto >. PDB*.  
  
  Se você criar seu aplicativo C/C++ usando um makefile e especificar **/ZI** ou **/Zi** sem usar **/Fd**, o compilador cria dois *. PDB*arquivos:  
  
  - *VC\<x>.pdb*, em que *\<x>* representa a versão do Visual C++, por exemplo, *VC11.pdb* 
    
    O *VC\<x >. PDB* arquivo armazena todas as informações de depuração para os arquivos de objeto individuais e reside no mesmo diretório que o makefile do projeto. Cada vez que ele cria um arquivo de objeto, o compilador do C/C++ mescla informações de depuração em *VC\<x >. PDB*. Portanto, mesmo se todos os arquivos de origem incluam arquivos de cabeçalho, como  *\<Windows. h >*, os typedefs desses cabeçalhos são armazenados apenas uma vez, em vez de em todos os arquivos de objeto. As informações inseridas incluem informações de tipo, mas não incluem informações de símbolo como definições de função.  
  
  - *\<projeto >. PDB* 
    
    O  *\<projeto >. PDB* arquivo armazena todas as informações de depuração para o projeto *.exe* de arquivo e reside no *\debug* subdiretório. O arquivo *\<projeto>.pdb* contém todas as informações de depuração, incluindo protótipos de função, não apenas as informações de tipo encontradas no *VC\<x>.pdb*. 
  
  Os dois os *VC\<x >. PDB* e  *\<projeto >. PDB* arquivos permitem atualizações incrementais. O vinculador também insere o caminho para o *. PDB* arquivos de *.exe* ou *. dll* arquivo que ele cria.  
  
- <a name="use-dumpbin-exports"></a>Tabelas de exportação DLL
  
  Use `dumpbin /exports` para ver os símbolos disponíveis na tabela de exportação de uma DLL. Informações simbólicas das tabelas de exportação DLL podem ser útil para trabalhar com mensagens do Windows, procedimentos do Windows (WindowProcs), COM objetos, empacotamento ou qualquer DLL, você não tem símbolos para. Os símbolos estão disponíveis para qualquer DLL de 32 bits do sistema. As chamadas são listadas na ordem de chamada, com a função atual (a mais profundamente aninhada) na parte superior. 
  
  Lendo o `dumpbin /exports` de saída, você pode ver os nomes de função exato, incluindo caracteres não alfanuméricos. Ver os nomes de função exato é útil para definir um ponto de interrupção em uma função, porque os nomes de função podem ser truncados em outro lugar no depurador. Para obter mais informações, confira [dumpbin /exports](/cpp/build/reference/dash-exports).  
  
### <a name="net-framework-options"></a>Opções do .NET Framework 
  
Compilar com o **/Debug** para criar um *. PDB* arquivo. Você pode criar aplicativos com **/Debug: full** ou **/Debug: pdbonly**. Compilando com **/Debug: full** gera código depurável. Compilando com **/Debug: pdbonly** gera *. PDB* os arquivos, mas não gera o `DebuggableAttribute` que informa o compilador JIT que as informações de depuração estão disponíveis. Use **/Debug: pdbonly** se você quiser gerar *. PDB* arquivos para uma versão de compilação que você não deseja ser depurável. Para obter mais informações, consulte [/Debug (C# opções do compilador)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option) ou [/debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug).  
  
### <a name="web-applications"></a>Aplicativos Web  
  
Defina as *Web. config* arquivo do seu aplicativo ASP.NET para o modo de depuração. O modo de depuração faz com que o ASP.NET gere símbolos para arquivos gerados dinamicamente e permite que o depurador se anexe ao aplicativo ASP.NET. Visual Studio define isso automaticamente quando você inicia a depuração, se você tiver criado seu projeto do modelo projetos web.  

##  <a name="manage-symbols-while-debugging"></a>Gerenciar símbolos durante a depuração 

Você pode usar o **módulos**, **pilha de chamadas**, **locais**, **Autos**, ou qualquer **inspeção** janela para carregar símbolos ou alterar as opções de símbolo durante a depuração. Para obter mais informações, consulte [se familiarizar mais com como o depurador se anexa ao aplicativo](../debugger/debugger-tips-and-tricks.md#modules_window).

### <a name="use-the-modules-window"></a>Usar a janela módulos

Durante a depuração, o **módulos** janela mostra os módulos de código que o depurador está tratando como o código do usuário, ou o meu código e seu status de carregamento de símbolo. Também monitorar o status de carregamento de símbolo, carregar símbolos e alterar as opções de símbolo na **módulos** janela.

**Para monitorar ou alterar locais de símbolos ou opções durante a depuração:**

1. Para abrir o **módulos** janela, durante a depuração, selecione **Debug** > **Windows** > **módulos**. 
1. No **módulos** janela, com o botão direito do **Status do símbolo** ou **arquivo de símbolo** cabeçalhos ou qualquer módulo. 
1. No menu de contexto, selecione uma das seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Carregar Símbolos**|É exibida para os módulos com símbolos ignorados, não foi encontrados ou não carregados. Tenta carregar símbolos de locais especificados na **opções** > **depuração** > **símbolos** página. Se o arquivo de símbolo não é foi encontrado ou não carregado, inicia **Explorador de arquivos** para que você possa especificar um novo local de pesquisa.|  
|**Informações de Carregamento de Símbolos**|Mostra o local de um arquivo de símbolo carregado ou os locais que foram pesquisados se o depurador não é possível localizar o arquivo.|  
|**Configurações de Símbolo**|Abre o **opções** > **depuração** > **símbolos** página, onde você pode editar e adicionar locais de símbolos.|  
|**Sempre Carregar Automaticamente**|Adiciona o arquivo de símbolo selecionado à lista de arquivos que são carregados automaticamente pelo depurador.|  

### <a name="use-the-no-symbols-loadedno-source-loaded-pages"></a>Use as páginas nenhuma símbolos Loaded/No origem carregada

Há várias maneiras para que o depurador entrar no código que não tenha arquivos de símbolo ou de origem disponíveis:  

-  Intervir no código.  
-  Entrar no código de um ponto de interrupção ou exceção.  
-  Alternar para um thread diferente.  
-  Alterar o registro de ativação clicando duas vezes em um quadro na **pilha de chamadas** janela.  
   
Quando isso acontece, o depurador exibe o **nenhum símbolo carregado** ou **nenhuma origem carregada** páginas para ajudá-lo a localizar e carregar os símbolos necessários ou código-fonte.  
  
 ![Nenhuma página símbolos carregados](../debugger/media/dbg-nosymbolsloaded.png "DBG_NoSymbolsLoaded")  
  
**Para usar a página de documento nenhum símbolo carregado para ajudar a localizar e carregar símbolos ausentes:**  
  
-   Para alterar o caminho de pesquisa, selecione um caminho não selecionado ou selecione **novo caminho** ou **novo caminho do VSTS** e insira ou selecione um novo caminho. Selecione **carregar** para procurar novamente os caminhos e carregar o arquivo de símbolo se ela for encontrada.  
-   Para substituir as opções de qualquer símbolo e repita os caminhos de pesquisa, selecione **procurar e localizar \<nome do executável >**. O arquivo de símbolo será carregado se ele for encontrado, ou **Explorador de arquivos** será aberta para que você pode selecionar manualmente o arquivo de símbolo.  
-   Para abrir o **opções** > **depuração** > **símbolos** página, selecione **alterar configurações de símbolo**.  
-   Para mostrar a desmontagem em uma nova janela uma vez, selecione **exibir a desmontagem**, ou selecione **caixa de diálogo Opções** para definir a opção para sempre mostrar a desmontagem quando os arquivos de origem ou de símbolo não forem encontrados. 
-   Para mostrar os locais pesquisados e o resultado, expanda **informações de carregamento de símbolo**. 

Se o depurador encontrar o *. PDB* depois de executar uma das opções e pode recuperar o arquivo de origem usando as informações do arquivo a *. PDB* arquivo, ele exibe a origem. Caso contrário, ele exibe uma **nenhuma origem carregada** página que descreve o problema, com links para as ações que podem resolver o problema.

**Para adicionar caminhos de pesquisa do arquivo de origem para uma solução:**
  
Você pode especificar os locais em que o depurador procura por arquivos de origem e excluir arquivos específicos da pesquisa.

1. Selecione a solução no **Gerenciador de soluções**e, em seguida, selecione o **Properties** ícone, pressione **Alt**+**Enter**, ou Clique com botão direito e selecione **propriedades**.
   
1. Selecione **depurar arquivos de origem**.
   
1. Sob **diretórios que contêm o código-fonte**, digite ou selecione os locais de código fonte para pesquisar. Use o **nova linha** ícone para adicionar mais locais, o **backup** e **para baixo** ícones de seta para reordená-los, ou o **X** ícone excluí-los.
   
   >[!NOTE]
   >O depurador procura somente o diretório especificado. Você deve adicionar entradas para todos os subdiretórios que deseja pesquisar.
   
1. Sob **não procurar por esses arquivos de origem**, digite os nomes dos arquivos de origem serão excluídos da pesquisa. 
   
1. Selecione **Okey** ou **aplicar**.


## <a name="see-also"></a>Consulte também  
[Entender os arquivos de símbolo e configurações de símbolo do Visual Studio](https://blogs.msdn.microsoft.com/devops/2015/01/05/understanding-symbol-files-and-visual-studios-symbol-settings/)

[Alterações de carregamento de símbolo remoto do .NET no Visual Studio 2012 e 2013](https://blogs.msdn.microsoft.com/devops/2013/10/16/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013/)
