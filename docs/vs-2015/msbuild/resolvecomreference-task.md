---
title: Tarefa ResolveComReference | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ResolveComReference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, ResolveCOMReference task
- ResolveCOMReference task [MSBuild]
ms.assetid: c9bf5fcf-6453-40ea-b50f-a212adc3e9b5
caps.latest.revision: 29
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bf70e5c2fe77f275f31ed9966df262d64ed2c23d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49179355"
---
# <a name="resolvecomreference-task"></a>Tarefa ResolveComReference
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Obtém uma lista de um ou mais nomes de bibliotecas de tipo ou arquivos .tlb e resolve essas bibliotecas de tipo em locais no disco.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `ResolveCOMReference`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`DelaySign`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, coloca a chave pública no assembly. Se `false`, assina totalmente o assembly.|  
|`EnvironmentVariables`|Parâmetro `String[]` opcional.<br /><br /> Matriz de pares de variáveis de ambiente, separadas por sinais de igual. Essas variáveis são passadas para os tlbimp.exe e aximp.exe gerados além do bloqueio de ambiente regular ou substituindo-o seletivamente.|  
|`ExecuteAsTool`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, executa tlbimp.exe e aximp.exe da estrutura de destino apropriada fora de processo para gerar os assemblies de wrapper necessários. Esse parâmetro habilita multiplataformas.|  
|`IncludeVersionInInteropName`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a versão de typelib será incluída no nome do wrapper. O padrão é `false`.|  
|`KeyContainer`|Parâmetro `String` opcional.<br /><br /> Especifica um contêiner que contém um par de chaves<br /><br /> público/privado.|  
|`KeyFile`|Parâmetro `String` opcional.<br /><br /> Especifica um item que contém um par de chaves<br /><br /> público/privado.|  
|`NoClassMembers`|Parâmetro `Boolean` opcional.|  
|`ResolvedAssemblyReferences`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Especifica as referências do assembly resolvidas.|  
|`ResolvedFiles`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Especifica os arquivos totalmente qualificados no disco que correspondem aos locais físicos das bibliotecas de tipo que foram fornecidas como entrada para esta tarefa.|  
|`ResolvedModules`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.|  
|`SdkToolsPath`|Opcional [String] (<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) parâmetro.<br /><br /> Se `ExecuteAsTool` for `true`, esse parâmetro deverá ser definido como o caminho de ferramentas do SDK para a versão da estrutura de destino.|  
|`StateFile`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica o arquivo de cache dos carimbos de hora/hora de componente COM. Se não existir, cada execução regenerará todos os invólucros.|  
|`TargetFrameworkVersion`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica a versão da estrutura de destino do projeto.<br /><br /> O padrão é `String.Empty`. o que significa que não há nenhuma filtragem para uma referência com base na estrutura de destino.|  
|`TargetProcessorArchitecture`|Parâmetro <!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  --> opcional.<br /><br /> Especifica a arquitetura do processador de destino preferencial. Passado para o sinalizador de /machine tlbimp.exe após a tradução.<br /><br /> O valor do parâmetro deve ser um membro de <xref:Microsoft.Build.Utilities.ProcessorArchitecture>.|  
|`TypeLibFiles`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica o caminho do arquivo de biblioteca de tipo para referências COM. Itens incluídos nesse parâmetro podem conter metadados do item. Para obter mais informações, consulte a seção “Metadados do Item TypeLibFiles” abaixo.|  
|`TypeLibNames`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica os nomes da biblioteca de tipos a serem resolvidos. Itens incluídos nesse parâmetro devem conter alguns metadados do item. Para obter mais informações, consulte a seção “Metadados do Item TypeLibNames” abaixo.|  
|`WrapperOutputDirectory`|Parâmetro `String` opcional.<br /><br /> O local no disco no qual o assembly de interoperabilidade gerado é colocado. Se esses metadados de item não forem especificados, a tarefa usará o caminho absoluto do diretório em que o arquivo de projeto está localizado.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="typelibnames-item-metadata"></a>Metadados de Item TypeLibNames  
 A tabela a seguir descreve os metadados de item disponíveis para itens passados para o parâmetro `TypeLibNames`.  
  
|Metadados|Descrição|  
|--------------|-----------------|  
|`GUID`|Metadados obrigatórios do item.<br /><br /> O GUID para a biblioteca de tipos. Se esses metadados de item não forem especificados, a tarefa falhará.|  
|`VersionMajor`|Metadados obrigatórios do item.<br /><br /> A versão principal da biblioteca de tipos. Se esses metadados de item não forem especificados, a tarefa falhará.|  
|`VersionMinor`|Metadados obrigatórios do item.<br /><br /> A versão secundária da biblioteca de tipos. Se esses metadados de item não forem especificados, a tarefa falhará.|  
|`LocaleIdentifier`|Metadados opcionais do item.<br /><br /> O LCID (ID de localidade) da biblioteca de tipos. Isso é especificado como um valor de 32 bits que identifica o idioma humano preferido por um usuário, região ou aplicativo. Se esses metadados de item não forem especificados, a tarefa usará uma ID de localidade de “0”.|  
|`WrapperTool`|Metadados opcionais do item.<br /><br /> Especifica a ferramenta wrapper que é usada para gerar o wrapper do assembly para esta biblioteca de tipos. Se esses metadados de item não forem especificados, a tarefa usará uma ferramenta wrapper padrão de “tlbimp”. As opções de typelibs disponíveis que não diferenciam maiúsculas e minúsculas são:<br /><br /> -   `Primary`: use essa ferramenta wrapper quando desejar usar um assembly de interoperabilidade primário já gerado para o componente COM. Quando você usar essa ferramenta wrapper, não especifique um diretório de saída do wrapper, pois isso fará com que a tarefa falhe.<br />-   `TLBImp`: use essa ferramenta wrapper quando desejar gerar um assembly de interoperabilidade para o componente COM.<br />-   `AXImp`: use essa ferramenta wrapper quando desejar gerar um assembly de interoperabilidade para um Controle ActiveX.|  
  
## <a name="typelibfiles-item-metadata"></a>Metadados de Item TypeLibFiles  
 A tabela a seguir descreve os metadados de item disponíveis para itens passados para o parâmetro `TypeLibFiles`.  
  
|Metadados|Descrição|  
|--------------|-----------------|  
|`WrapperTool`|Metadados opcionais do item.<br /><br /> Especifica a ferramenta wrapper que é usada para gerar o wrapper do assembly para esta biblioteca de tipos. Se esses metadados de item não forem especificados, a tarefa usará uma ferramenta wrapper padrão de “tlbimp”. As opções de typelibs disponíveis que não diferenciam maiúsculas e minúsculas são:<br /><br /> -   `Primary`: use essa ferramenta wrapper quando desejar usar um assembly de interoperabilidade primário já gerado para o componente COM. Quando você usar essa ferramenta wrapper, não especifique um diretório de saída do wrapper, pois isso fará com que a tarefa falhe.<br />-   `TLBImp`: use essa ferramenta wrapper quando desejar gerar um assembly de interoperabilidade para o componente COM.<br />-   `AXImp`: use essa ferramenta wrapper quando desejar gerar um assembly de interoperabilidade para um Controle ActiveX.|  
  
> [!NOTE]
>  Quanto mais informações você fornece para identificar uma biblioteca de tipos com exclusividade, maior a possibilidade de que a tarefa será resolvida para o arquivo correto no disco.  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Tarefa de Classe Base](../msbuild/task-base-class.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



