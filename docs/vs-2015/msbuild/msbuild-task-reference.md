---
title: Referência da Tarefa do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tasks
ms.assetid: b3144b27-a426-4259-b8ae-5f7991b202b6
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b6f1767ce1c572e1e3d8eacae8ba3a60f3593476
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49193980"
---
# <a name="msbuild-task-reference"></a>Referência das tarefas do MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Tarefas fornecem o código que é executado durante o processo de compilação. As tarefas na lista a seguir são incluídas com [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]. Quando [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] é instalado, há tarefas adicionais disponíveis, que são usadas para compilar projetos [!INCLUDE[vcprvc](../includes/vcprvc-md.md)]. Para obter mais informações, consulte [Tarefas do Visual C++](../msbuild/msbuild-tasks-specific-to-visual-cpp.md).  
  
 Além dos parâmetros listados nos tópicos nesta seção, cada tarefa também tem os parâmetros a seguir:  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`Condition`|Parâmetro `String` opcional.<br /><br /> A expressão `Boolean` que o mecanismo [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] usa para determinar se essa tarefa será executada. Para obter informações sobre as condições que são suportadas pelo [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)], confira [Condições](../msbuild/msbuild-conditions.md).|  
|`ContinueOnError`|Parâmetro opcional. Pode conter um dos seguintes valores:<br /><br /> -   **WarnAndContinue** ou **true**. Quando uma tarefa falha, as tarefas subsequentes no elemento de [Destino](../msbuild/target-element-msbuild.md) e o build continuam em execução e todos os erros da tarefa são tratados como avisos.<br />-   **ErrorAndContinue**. Quando uma tarefa falha, as tarefas subsequentes no elemento de `Target` e o build continuam em execução e todos os erros da tarefa são tratados como erros.<br />-   **ErrorAndStop** ou **false** (padrão). Quando uma tarefa falha, as tarefas restantes do elemento de `Target` e o build não são executadas e todo o elemento de `Target` e o build são considerados como em falha.<br /><br /> As versões do .NET Framework antes da 4.5 ofereciam suporte somente aos valores `true` e `false`.<br /><br /> Para obter mais informações, confira [Como: ignorar erros em tarefas](../msbuild/how-to-ignore-errors-in-tasks.md).|  
  
## <a name="in-this-section"></a>Nesta seção  
 [Classe base Task](../msbuild/task-base-class.md)  
 Adiciona vários parâmetros para as tarefas que derivam da classe <xref:Microsoft.Build.Utilities.Task>.  
  
 [Classe base TaskExtension](../msbuild/taskextension-base-class.md)  
 Adiciona vários parâmetros para as tarefas que derivam da classe <xref:Microsoft.Build.Tasks.TaskExtension>.  
  
 [Classe base ToolTaskExtension](../msbuild/tooltaskextension-base-class.md)  
 Adiciona vários parâmetros para as tarefas que derivam da classe <xref:Microsoft.Build.Tasks.ToolTaskExtension>.  
  
 [Tarefa AL (Assembly Linker)](../msbuild/al-assembly-linker-task.md)  
 Cria um assembly com um manifesto com base em um ou mais arquivos que são arquivos de recurso ou módulos.  
  
 [Tarefa AspNetCompiler](../msbuild/aspnetcompiler-task.md)  
 Encapsula aspnet_compiler.exe, um utilitário para pré-compilar aplicativos ASP.NET.  
  
 [Tarefa AssignCulture](../msbuild/assignculture-task.md)  
 Atribui os identificadores de cultura a itens.  
  
 [Tarefa AssignProjectConfiguration](../msbuild/assignprojectconfiguration-task.md)  
 Aceita uma lista de cadeias de caracteres de configuração e as atribui a projetos especificados.  
  
 [Tarefa AssignTargetPath](../msbuild/assigntargetpath-task.md)  
 Aceita uma lista de arquivos e adiciona atributos `<TargetPath>` se eles ainda não foram especificados.  
  
 [Tarefa CallTarget](../msbuild/calltarget-task.md)  
 Invoca um destino no arquivo de projeto.  
  
 [Tarefa CombinePath](../msbuild/combinepath-task.md)  
 Combina os caminhos especificados em um único caminho.  
  
 [Tarefa ConvertToAbsolutePath](../msbuild/converttoabsolutepath-task.md)  
 Converte uma referência ou caminho relativo em um caminho absoluto.  
  
 [Tarefa Copy](../msbuild/copy-task.md)  
 Copia os arquivos para um novo local.  
  
 [Tarefa CreateCSharpManifestResourceName](../msbuild/createcsharpmanifestresourcename-task.md)  
 Cria um nome de manifesto de estilo [!INCLUDE[csprcs](../includes/csprcs-md.md)] de um nome de arquivo .resx fornecido ou de outro recurso.  
  
 [Tarefa CreateItem](../msbuild/createitem-task.md)  
 Popula as coleções de itens dos itens de entrada, permitindo que os itens sejam copiados de uma lista para outra.  
  
 [Tarefa CreateProperty](../msbuild/createproperty-task.md)  
 Popula as propriedades de valores de entrada, permitindo que os valores sejam copiados de uma propriedade ou cadeia de caracteres para outra.  
  
 [Tarefa CreateVisualBasicManifestResourceName](../msbuild/createvisualbasicmanifestresourcename-task.md)  
 Cria um nome de manifesto de estilo [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] de um nome de arquivo .resx fornecido ou de outro recurso.  
  
 [Tarefa Csc](../msbuild/csc-task.md)  
 Chama o Compilador do Visual C# para produzir arquivos executáveis, bibliotecas de vínculo dinâmico ou módulos de código.  
  
 [Tarefa Delete](../msbuild/delete-task.md)  
 Exclui os arquivos especificados.  
  
 [Tarefa Error](../msbuild/error-task.md)  
 Interrompe um build e registra um erro com base em uma instrução condicional avaliada.  
  
 [tarefa Exec](../msbuild/exec-task.md)  
 Executa o programa ou comando especificado com os argumentos especificados.  
  
 [Tarefa FindAppConfigFile](../msbuild/findappconfigfile-task.md)  
 Localiza o arquivo app.config, se houver, nas listas fornecidas.  
  
 [Tarefa FindInList](../msbuild/findinlist-task.md)  
 Localiza um item em uma lista especificada com o itemspec correspondente.  
  
 [Tarefa FindUnderPath](../msbuild/findunderpath-task.md)  
 Determina quais itens na coleção de itens especificados existem na pasta especificada ou suas subpastas.  
  
 [Tarefa FormatUrl](../msbuild/formaturl-task.md)  
 Converte uma URL em um formato de URL correto.  
  
 [Tarefa FormatVersion](../msbuild/formatversion-task.md)  
 Acrescenta o número de revisão ao número de versão.  
  
 [Tarefa GenerateApplicationManifest](../msbuild/generateapplicationmanifest-task.md)  
 Gera um manifesto do aplicativo ou um manifesto nativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)].  
  
 [Tarefa GenerateBootstrapper](../msbuild/generatebootstrapper-task.md)  
 Fornece uma forma automatizada de detectar, baixar e instalar um aplicativo e seus pré-requisitos.  
  
 [Tarefa GenerateDeploymentManifest](../msbuild/generatedeploymentmanifest-task.md)  
 Gera um manifesto de implantação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)].  
  
 [Tarefa GenerateResource](../msbuild/generateresource-task.md)  
 Converte arquivos .txt e .resx em arquivos .resources binários do Common Language Runtime.  
  
 [Tarefa GenerateTrustInfo](../msbuild/generatetrustinfo-task.md)  
 Gera a confiança do aplicativo do manifesto base e dos parâmetros `TargetZone` e `ExcludedPermissions`.  
  
 [Tarefa GetAssemblyIdentity](../msbuild/getassemblyidentity-task.md)  
 Recupera as identidades do assembly dos arquivos especificados e gera como saída as informações de identidade.  
  
 [Tarefa GetFrameworkPath](../msbuild/getframeworkpath-task.md)  
 Recupera o caminho para os assemblies [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
 [Tarefa GetFrameworkSdkPath](../msbuild/getframeworksdkpath-task.md)  
 Recupera o caminho para o [!INCLUDE[winsdklong](../includes/winsdklong-md.md)].  
  
 [Tarefa GetReferenceAssemblyPaths](../msbuild/getreferenceassemblypaths-task.md)  
 Retorna os caminhos do assembly de referência de diversas estruturas.  
  
 [Tarefa LC](../msbuild/lc-task.md)  
 Gera um arquivo .license de um arquivo .licx.  
  
 [Tarefa MakeDir](../msbuild/makedir-task.md)  
 Cria diretórios e, se necessário, qualquer diretório pai.  
  
 [Tarefa de mensagem](../msbuild/message-task.md)  
 Registra uma mensagem em log durante um build.  
  
 [Tarefa Move](../msbuild/move-task.md)  
 Move os arquivos para um novo local.  
  
 [Tarefa MSBuild](../msbuild/msbuild-task.md)  
 Compila projetos [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] de outro projeto [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)].  
  
 [Tarefa ReadLinesFromFile](../msbuild/readlinesfromfile-task.md)  
 Lê uma lista de itens de um arquivo de texto.  
  
 [Tarefa RegisterAssembly](../msbuild/registerassembly-task.md)  
 Lê os metadados dentro do assembly especificado e adiciona as entradas necessárias ao Registro.  
  
 [Tarefa RemoveDir](../msbuild/removedir-task.md)  
 Remove os diretórios especificados e todos os seus arquivos e subdiretórios.  
  
 [Tarefa RemoveDuplicates](../msbuild/removeduplicates-task.md)  
 Remove itens duplicados da coleção do item especificado.  
  
 [Tarefa RequiresFramework35SP1Assembly](../msbuild/requiresframework35sp1assembly-task.md)  
 Determina se o aplicativo requer o .NET Framework 3.5 SP1.  
  
 Tarefa ResGen  
 Obsoleto. Use a [Tarefa GenerateResource](../msbuild/generateresource-task.md) para converter arquivos .txt e .resx em arquivos .resources binários do Common Language Runtime.  
  
 [Tarefa ResolveAssemblyReference](../msbuild/resolveassemblyreference-task.md)  
 Determina todos os assemblies que dependem dos assemblies especificados.  
  
 [Tarefa ResolveComReference](../msbuild/resolvecomreference-task.md)  
 Obtém uma lista de um ou mais nomes de bibliotecas de tipo ou arquivos .tlb e resolve essas bibliotecas de tipo em locais no disco.  
  
 [Tarefa ResolveKeySource](../msbuild/resolvekeysource-task.md)  
 Determina a origem da chave de nome forte  
  
 [Tarefa ResolveManifestFiles](../msbuild/resolvemanifestfiles-task.md)  
 Resolve os seguintes itens no processo de build para arquivos de geração de manifesto: itens compilados, dependências, satélites, conteúdo, símbolos de depuração e documentação.  
  
 [Tarefa ResolveNativeReference](../msbuild/resolvenativereference-task.md)  
 Resolve referências nativas.  
  
 [Tarefa ResolveNonMSBuildProjectOutput](../msbuild/resolvenonmsbuildprojectoutput-task.md)  
 Determina os arquivos de saída para referências de projeto não MSBuild.  
  
 [Tarefa SGen](../msbuild/sgen-task.md)  
 Cria um assembly de serialização de XML para tipos no assembly especificado.  
  
 [Tarefa SignFile](../msbuild/signfile-task.md)  
 Assina o arquivo especificado usando o certificado especificado.  
  
 [Tarefa Touch](../msbuild/touch-task.md)  
 Define os horários de modificação e acesso aos arquivos.  
  
 [Tarefa UnregisterAssembly](../msbuild/unregisterassembly-task.md)  
 Cancela o registro os assemblies especificados para fins de interoperabilidade COM.  
  
 [Tarefa UpdateManifest](../msbuild/updatemanifest-task.md)  
 Atualiza as propriedades selecionadas em um manifesto e assina-as novamente.  
  
 [Tarefa Vbc](../msbuild/vbc-task.md)  
 Invoca o compilador do Visual Basic para produzir arquivos executáveis, bibliotecas de vínculo dinâmico ou módulos de código.  
  
 [Tarefa Warning](../msbuild/warning-task.md)  
 Registra um aviso durante um build com base em uma instrução condicional avaliada.  
  
 [Tarefa WriteCodeFragment](../msbuild/writecodefragment-task.md)  
 Gera um arquivo de código temporário pelo uso do fragmento de código gerado especificado. Não exclui o arquivo.  
  
 [Tarefa WriteLinesToFile](../msbuild/writelinestofile-task.md)  
 Grava os itens especificados no arquivo de texto especificado.  
  
 [Tarefa XmlPeek](../msbuild/xmlpeek-task.md)  
 Retorna os valores conforme especificado por uma consulta de XPath em um arquivo XML.  
  
 [Tarefa XmlPoke](../msbuild/xmlpoke-task.md)  
 Define os valores conforme especificado por uma consulta de XPath em um arquivo XML.  
  
 [Tarefa XslTransformation](../msbuild/xsltransformation-task.md)  
 Transformações um XML de entrada usando um *XSLT (linguagem XSL Transformation)* ou XSLT compilado e saídas para um arquivo ou um dispositivo de saída.  
  
## <a name="see-also"></a>Consulte também  
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Escrevendo tarefas](../msbuild/task-writing.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)



