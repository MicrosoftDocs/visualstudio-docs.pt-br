---
title: Tarefa SGen | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#SGen
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- SGen task [MSBuild]
- MSBuild, SGen task
ms.assetid: 22c5ade4-4159-4667-b891-0c1aa06f4df5
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 89a5285e304e74aba01f81d8ec9bfc5017677a7b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49919176"
---
# <a name="sgen-task"></a>tarefa SGen
Cria um assembly de serialização de XML para tipos no assembly especificado. A tarefa encapsula a Ferramenta geradora de serializador de XML (*Sgen.exe*). Para saber mais, confira [Ferramenta geradora de serializador de XML (Sgen.exe)](/dotnet/framework/serialization/xml-serializer-generator-tool-sgen-exe).  

## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `SGen`.  


| Parâmetro | Descrição |
|-----------------------------| - |
| `BuildAssemblyName` | Parâmetro `String` obrigatório.<br /><br /> Defina o assembly para o qual gerar código de serialização. |
| `BuildAssemblyPath` | Parâmetro `String` obrigatório.<br /><br /> O caminho para o assembly para o qual gerar código de serialização. |
| `DelaySign` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, especificará que você deseja um assembly totalmente com sinal. Se for `false`, especificará que você apenas deseja colocar a chave pública no assembly.<br /><br /> Esse parâmetro não terá nenhum efeito a menos que seja usado com o parâmetro `KeyFile` ou `KeyContainer`. |
| `KeyContainer` | Parâmetro `String` opcional.<br /><br /> Especifica um contêiner que mantém um par de chaves. Isso assinará o assembly inserindo uma chave pública no manifesto do assembly. A tarefa assinará então o assembly final com a chave privada. |
| `KeyFile` | Parâmetro `String` opcional.<br /><br /> Especifica um par de chaves ou uma chave pública a usar para assinar um assembly. O compilador insere a chave pública no manifesto do assembly e, em seguida, assina o assembly final com a chave privada. |
| `Platform` | Parâmetro `String` opcional.<br /><br /> Obtém ou define a plataforma do compilador usado para gerar o assembly de saída. Esse parâmetro pode ter um valor igual a `x86`, `x64` ou `anycpu`. O padrão é `anycpu`. |
| `References` | Parâmetro `String[]` opcional.<br /><br /> Especifica os assemblies que são referenciados pelos tipos que exigem a serialização de XML. |
| `SdkToolsPath` | Parâmetro `String` opcional.<br /><br /> Especifica o caminho para o SDK Tools, como *resgen.exe*. |
| `SerializationAssembly` | Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém o assembly de serialização gerado. |
| `SerializationAssemblyName` | Parâmetro `String` opcional.<br /><br /> Especifica o nome do assembly de serialização gerado. |
| `ShouldGenerateSerializer` | Parâmetro `Boolean` obrigatório.<br /><br /> Se `true`, a tarefa SGen deve gerar um assembly de serialização. |
| `Timeout` | Parâmetro `Int32` opcional.<br /><br /> Especifica a quantidade de tempo em milissegundos após o qual o executável da tarefa é encerrado. O valor padrão é `Int.MaxValue`, indicando que não há período de tempo limite. |
| `ToolPath` | Parâmetro `String` opcional.<br /><br /> Especifica o local de onde tarefa carregará o arquivo executável subjacente (*sgen.exe*). Se esse parâmetro não for especificado, a tarefa usará o caminho de instalação do SDK correspondente à versão da estrutura que está executando [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. |
| `Types` | Parâmetro `String[]` opcional.<br /><br /> Obtém ou define uma lista de tipos específicos para os quais gerar código de serialização. O SGen gerará o código de serialização somente para esses tipos. |
| `UseProxyTypes` | Parâmetro `Boolean` obrigatório.<br /><br /> Se `true`, a tarefa SGen gera o código de serialização somente para os tipos de proxy de serviço Web XML. |

## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.ToolTaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.ToolTask>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base ToolTaskExtension](../msbuild/tooltaskextension-base-class.md).  

## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)