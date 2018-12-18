---
title: Integração com o Visual Studio (MSBuild) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, reference resolution
- MSBuild, well-known target names
- MSBuild, hosting
- MSBuild, editing project files
- MSBuild, Visual Studio integration
- MSBuild, IntelliSense
- MSBuild, output groups
- MSBuild, in-process compilers
- MSBuild, design-time target execution
ms.assetid: 06cd6d7f-8dc1-4e49-8a72-cc9e331d7bca
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 874642371f173b56a174dabdd17ee1cf50cc79fc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49875470"
---
# <a name="visual-studio-integration-msbuild"></a>Integração com o Visual Studio (MSBuild)
O Visual Studio hospeda o [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] para carregar e compilar projetos gerenciados. Como [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] é responsável pelo projeto, quase todo projeto que estiver no formato [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] poderá ser utilizado com êxito no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], mesmo se o projeto tiver sido criado por meio de uma ferramenta diferente e tenha um processo de build personalizado.  
  
 Este artigo descreve aspectos específicos da hospedagem do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] pelo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] que devem ser considerados ao personalizar projetos e arquivos *.targets* que serão carregados e compilados em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Isso ajudará a certificar recursos [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], como o IntelliSense e a depuração de trabalho no projeto personalizado.  
  
 Para saber mais sobre projetos C++, confira [Arquivos de projeto](/cpp/ide/project-files).  
  
## <a name="project-file-name-extensions"></a>Extensões de nome do arquivo de projeto  
 O *MSBuild.exe* reconhece extensões de nome de arquivo de projeto que correspondem ao padrão *.\*proj*. No entanto, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] reconhece somente um subconjunto dessas extensões de nome de arquivo de projeto, o que determina o sistema de projeto específico a um idioma que carregará o projeto. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] não tem um [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] com neutralidade de idioma baseado no sistema de projeto.  
  
 Por exemplo, o sistema de projeto [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] carrega os arquivos *.csproj*, mas não é possível para [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] carregar um arquivo *.xxproj*. Um arquivo de projeto para arquivos fonte em um idioma arbitrário deve usar a mesma extensão dos arquivos de projeto [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ou [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] para ser carregado no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
## <a name="well-known-target-names"></a>Nomes de destinos bem conhecidos  
 O comando **Compilar** no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] executará o destino padrão do projeto. Geralmente, esse destino também é denominado `Build`. Os comandos **Recompilar** ou **Limpar** farão com que ocorra uma tentativa de executar um destino de nome igual no projeto. O comando **Publicar** executará um destino nomeado como `PublishOnly` no projeto.  
  
## <a name="configurations-and-platforms"></a>Configurações e plataformas  
 As configurações são representadas nos projetos [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] por meio de propriedades agrupadas em um elemento `PropertyGroup` que contém um atributo `Condition`. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] examina essas condições a fim de criar uma lista para exibir configurações de projeto e plataformas. Para extrair essa lista com êxito, é necessário que as condições tenham um formato semelhante ao seguinte:  
  
```xml  
Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' "  
Condition=" '$(Configuration)' == 'Release' "   
Condition=" '$(Something)|$(Configuration)|$(SomethingElse)' == 'xxx|Debug|yyy' "  
```  
  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] examina as condições em elementos `PropertyGroup`, `ItemGroup`, `Import`, de propriedade e de item para essa finalidade.  
  
## <a name="additional-build-actions"></a>Ações de compilação adicionais  
 O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] permite que o nome do tipo de item de um arquivo seja alterado em um projeto com a propriedade **Ação de Build** da janela **Propriedades do arquivo**. Os nomes de tipo de item **Compile**, **EmbeddedResource**, **Content** e **None** sempre estarão listados no menu, juntamente com quaisquer outros nomes de tipo de item que já estejam no projeto. Para garantir a disponibilidade dos nomes de tipo de item personalizados nesse menu, é possível adicionar os nomes a um tipo de item de nome `AvailableItemName`. Por exemplo, adicionar o seguinte ao arquivo de projeto adicionará o tipo personalizado **JScript** a esse menu para todos os projetos que o importarem:  
  
```xml  
<ItemGroup>  
    <AvailableItemName Include="JScript"/>  
</ItemGroup>  
```  
  
> [!NOTE]
>  Alguns nomes de tipo de item são específicos do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], mas não aparecem nessa lista suspensa.  
  
## <a name="in-process-compilers"></a>Compiladores em processo  
 Quando possível, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] tentará usar a versão em processo do compilador [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] para melhorar o desempenho. (não se aplica a [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]). Para que isso funcione corretamente, as condições a seguir devem ser cumpridas:  
  
- Em um destino do projeto, deve haver uma tarefa nomeada como `Vbc` para projetos [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)].  
  
- O parâmetro `UseHostCompilerIfAvailable` da tarefa deve ser definido como true.  
  
## <a name="design-time-intellisense"></a>IntelliSense do Tempo de Design  
 Para obter o suporte do IntelliSense em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] antes que o build gere um assembly de saída, as condições a seguir devem ser cumpridas:  
  
-   Deve haver um destino com o nome `Compile`.  
  
-   É necessário que o destino `Compile` ou uma de suas dependências chame a tarefa do compilador do projeto, como `Csc` ou `Vbc`.  
  
-   O destino `Compile` ou uma de suas dependências deve fazer com que o compilador receba todos os parâmetros necessários para o IntelliSense, em particular, todas as referências.  
  
-   As condições listadas na seção [Compiladores em processo](#in-process-compilers) devem ser cumpridas.  
  
## <a name="build-solutions"></a>Soluções de compilação  
 Dentro do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], as ordens do arquivo de solução e do build de projeto são controladas pelo próprio [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Ao compilar uma solução com o *msbuild.exe* na linha de comando, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] analisa o arquivo de solução e ordena os builds de projeto. Em ambos os casos, os projetos são compilados individualmente em ordem de dependência e as referências projeto a projeto não são percorridas. Por outro lado, quando projetos individuais são compilados com o *msbuild.exe*, as referências projeto a projeto são percorridas.  
  
 Ao compilar em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], a propriedade `$(BuildingInsideVisualStudio)` será definida como `true`. Isso pode ser usado no projeto ou em arquivos *.targets* para fazer com que o build se comporte de maneira diferente.  
  
## <a name="display-properties-and-items"></a>Exibir propriedades e itens  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] reconhece determinados nomes de propriedades e valores. Por exemplo, a seguinte propriedade de um projeto fará com que **Aplicativos do Windows** apareçam na caixa **Tipo de Aplicativo** no **Designer de Projeto**.  
  
```xml  
<OutputType>WinExe</OutputType>  
```  
  
 O valor da propriedade pode ser editado no **Designer de Projeto** e salvo no arquivo de projeto. Se essa propriedade receber um valor inválido na edição manual, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] mostrará um aviso quando o projeto for carregado e substituirá o valor inválido por um valor padrão.  
  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] entende os padrões de algumas propriedades. Essas propriedades não serão mantidas no arquivo de projeto, a menos que eles tenham valores não padrão.  
  
 Propriedades com nomes arbitrários não são exibidas no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Para modificar propriedades arbitrárias em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], é necessário abrir o arquivo de projeto no editor de XML e editá-las manualmente. Para saber mais, confira a seção [Editar arquivos de projeto no Visual Studio](#edit-project-files-in-visual-studio) mais adiante neste tópico.  
  
 Os itens definidos no projeto com nomes de tipo de item arbitrários são exibidos por padrão no **Gerenciador de Soluções**, em seus respectivos nós de projeto. Para ocultar um item da exibição, defina os metadados `Visible` como `false`. Por exemplo, o item a seguir participará do processo de build, mas não será exibido no **Gerenciador de Soluções**.  
  
```xml  
<ItemGroup>  
    <IntermediateFile Include="cache.temp">  
        <Visible>false</Visible>  
    </IntermediateFile>  
</ItemGroup>  
```  
  
 Os itens declarados em arquivos importados para o projeto não serão exibidos por padrão. Os itens criados durante o processo de build nunca serão exibidos no **Gerenciador de Soluções**.  
  
## <a name="conditions-on-items-and-properties"></a>Condições em itens e propriedades  
 Durante o build, todas as condições serão plenamente respeitadas.  
  
 Ao determinar os valores da propriedade a ser exibida, as propriedades que [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] considerar dependentes da configuração serão avaliadas de forma diferente de propriedades consideradas independentes da configuração. Para as propriedades consideradas dependentes da configuração, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] definirá as propriedades `Configuration` e `Platform` de forma apropriada e instruirá [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] a reavaliar o projeto. Para as propriedades consideradas independentes da configuração, não é possível determinar como as condições serão avaliadas.  
  
 As expressões condicionais de itens sempre serão ignoradas com a finalidade de decidir se o item deve ser exibido no **Gerenciador de Soluções**.  
  
## <a name="debugging"></a>Depuração  
 Para localizar e iniciar o assembly de saída e anexar o depurador, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] precisa que as propriedades `OutputPath`, `AssemblyName` e `OutputType` estejam definidas corretamente. Não será possível anexar o depurador se o processo de build não fizer com que o compilador gere um arquivo *.pdb*.  
  
## <a name="design-time-target-execution"></a>Execução de destino do tempo de design  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] tentará executar destinos com determinados nomes ao carregar um projeto. Esses destinos incluem `Compile`, `ResolveAssemblyReferences`, `ResolveCOMReferences`, `GetFrameworkPaths` e `CopyRunEnvironmentFiles`. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] executará esses destinos para que o compilador seja inicializado a fim de fornecer o IntelliSense, o depurador poderá ser inicializado e as referências exibidas no Gerenciador de Soluções poderão ser resolvidas. Se esses destinos não estiverem presentes, o projeto carregará e compilará corretamente, mas a experiência de tempo de design no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] não será totalmente funcional.  
  
##  <a name="edit-project-files-in-visual-studio"></a>Editar arquivos de projeto no Visual Studio  
 Para editar um [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] diretamente do projeto, abra o arquivo de projeto no editor de XML do Visual Studio.  
  
#### <a name="to-unload-and-edit-a-project-file-in-visual-studio"></a>Para descarregar e editar um arquivo de projeto no Visual Studio  
  
1.  No **Gerenciador de Soluções**, abra o menu de atalho do projeto e, em seguida, escolha **Descarregar Projeto**.  
  
     O projeto está marcado como **(indisponível)**.  
  
2.  No **Gerenciador de Soluções**, abra o menu de atalho do projeto indisponível e, em seguida, escolha **Editar \<Arquivo de Projeto>**.  
  
     O arquivo de projeto será aberto no Editor de XML do Visual Studio.  
  
3.  Edite, salve e feche o arquivo de projeto.  
  
4.  No **Gerenciador de Soluções**, abra o menu de atalho do projeto indisponível e, em seguida, escolha **Recarregar Projeto**.  
  
## <a name="intellisense-and-validation"></a>IntelliSense e validação  
 Ao usar o editor XML para editar arquivos de projeto, o IntelliSense e a validação são controlados pelos arquivos de esquema [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. Eles são instalados no cache do esquema, que pode ser encontrado no *\<diretório de instalação do Visual Studio>\Xml\Schemas\1033\MSBuild*.  
  
 Os tipos de núcleo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] são definidos em *Microsoft.Build.Core.xsd* e os tipos comuns usados por [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] são definidos em *Microsoft.Build.CommonTypes.xsd*. Para personalizar os esquemas a fim de obter o IntelliSense e a validação para nomes, propriedades e tarefas de tipo de item personalizados, é possível editar o *Microsoft.Build.xsd* ou criar um esquema próprio que inclua CommonTypes ou esquemas de Núcleo. Ao criar um esquema próprio, será necessário direcionar o editor de XML a encontrá-lo por meio da janela **Propriedades**.  
  
## <a name="edit-loaded-project-files"></a>Como editar arquivos de projeto carregados  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] armazena em cache o conteúdo dos arquivos de projeto e os arquivos importados pelos arquivos de projeto. Se um arquivo de projeto carregado for editado, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] solicitará automaticamente o recarregamento do projeto para que as alterações tenham efeito. No entanto, se um arquivo importado por um projeto carregado for editado, não haverá solicitação de recarregamento e será necessário descarregar e recarregar o projeto manualmente para que as alterações tenham efeito.  
  
## <a name="output-groups"></a>Grupos de saída  
 Vários destinos definidos em *Microsoft.Common.targets* têm nomes que terminam em `OutputGroups` ou `OutputGroupDependencies`. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] chama esses destinos para obter listas específicas de saídas de projeto. Por exemplo, o destino `SatelliteDllsProjectOutputGroup` cria uma lista de todos os assemblies satélites que um build criará. Esses grupos de saída são usados por recursos como publicação, implantação e referências projeto a projeto. Os projetos que não os definirem serão carregados e compilados no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], mas alguns recursos podem não funcionar corretamente.  
  
## <a name="reference-resolution"></a>Resolução de referência  
 Resolução de referência é o processo de usar os itens de referência armazenados em um arquivo de projeto para localizar assemblies reais. É necessário que [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] dispare uma resolução de referência para mostrar propriedades detalhadas de cada referência na janela **Propriedades**. A lista a seguir descreve os três tipos de referências e como elas são resolvidas.  
  
- Referências do assembly:  
  
   O sistema de projeto chama um destino com o nome conhecido `ResolveAssemblyReferences`. Esse destino deve produzir itens com o nome de tipo de item `ReferencePath`. Cada um desses itens deve ter uma especificação de item (o valor do atributo `Include` de um item) que contém o caminho completo para a referência. Os itens devem ter todos os metadados dos itens de entrada aprovados, além dos novos metadados a seguir:  
  
  - `CopyLocal`, que indica se o assembly deve ser copiado para a pasta de saída, definido como true ou false.  
  
  - `OriginalItemSpec`, que contém a especificação de item original da referência.  
  
  - `ResolvedFrom`, definido como “{TargetFrameworkDirectory}” se tiver sido resolvido do diretório [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)].  
  
- Referências COM:  
  
   O sistema de projeto chama um destino com o nome conhecido `ResolveCOMReferences`. Esse destino deve produzir itens com o nome de tipo de item `ComReferenceWrappers`. Cada um desses itens deve ter uma especificação de item que contém o caminho completo para o assembly de interoperabilidade da referência COM. Os itens devem ter todos os metadados dos itens de entrada aprovados, além dos novos metadados com o nome `CopyLocal`, que indicam se o assembly deve ser copiado para a pasta de saída, definido como true ou false.  
  
- Referências nativas  
  
   O sistema de projeto chama um destino com o nome conhecido `ResolveNativeReferences`. Esse destino deve produzir itens com o nome de tipo de item `NativeReferenceFile`. Os itens devem ter todos os metadados dos itens de entrada aprovados, além de uma nova parte de metadados com o nome `OriginalItemSpec`, que contém a especificação de item original da referência.  
  
## <a name="performance-shortcuts"></a>Atalhos de desempenho  
 Se a depuração for iniciada na interface do usuário do Visual Studio (pela tecla F5 ou pela escolha de **Depurar** > **Iniciar Depuração** na barra de menus), o processo de build usará uma rápida verificação de atualização para melhorar o desempenho. Em alguns casos nos quais builds personalizados criam arquivos que, por sua vez, são compilados, a verificação de atualização rápida não identificará os arquivos alterados corretamente. Projetos que precisam de verificações de atualização mais completas podem desligue a verificação rápida configurando a variável de ambiente `DISABLEFASTUPTODATECHECK=1`. Como alternativa, os projetos podem definir isso como uma propriedade de MSBuild no projeto ou em um arquivo importado pelo projeto.  
  
 A atualização rápida não se aplica a builds regulares no Visual Studio e o projeto será compilado como se o build tivesse sido invocado por meio do prompt de comando.  
  
## <a name="see-also"></a>Consulte também  
 [Como estender o processo de build do Visual Studio](../msbuild/how-to-extend-the-visual-studio-build-process.md)   
 [Iniciar um build pelo IDE](../msbuild/starting-a-build-from-within-the-ide.md)   
 [Registrar extensões do .NET Framework](../msbuild/registering-extensions-of-the-dotnet-framework.md)   
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)   
 [Elemento Item (MSBuild)](../msbuild/item-element-msbuild.md)   
 [Elemento Property (MSBuild)](../msbuild/property-element-msbuild.md)   
 [Elemento Target (MSBuild)](../msbuild/target-element-msbuild.md)   
 [Tarefa Csc](../msbuild/csc-task.md)   
 [Tarefa Vbc](../msbuild/vbc-task.md)