---
title: Tarefa Exec | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Exec
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Exec task [MSBuild]
- MSBuild, Exec task
ms.assetid: c9b7525a-b1c9-40fc-8bce-77a5b8f960d8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bbefb90cad3b2aa3e6e7b0870548d44567ea8914
ms.sourcegitcommit: 56f3c31f1a06f6a6d2a8793b1abfa60cdf482497
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2018
ms.locfileid: "48817315"
---
# <a name="exec-task"></a>tarefa Exec
Executa o programa ou comando especificado pelo uso dos argumentos especificados.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `Exec`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`Command`|Parâmetro `String` obrigatório.<br /><br /> Os comandos a executar. Eles podem ser comandos do sistema, como attrib, ou um executável, como *program.exe*, *runprogram.bat* ou *setup.msi*.<br /><br /> Esse parâmetro pode conter várias linhas de comandos. Como alternativa, você pode colocar vários comandos em um arquivo em lotes e executá-lo por meio desse parâmetro.|  
|`ConsoleOutput`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Cada item de saída é uma linha do fluxo de saída padrão ou de erro padrão emitido pela ferramenta. Isso será capturado somente se `ConsoleToMsBuild` for definido como `true`.|
|`ConsoleToMsBuild`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa vai capturar o erro padrão e a saída padrão da ferramenta e disponibilizá-los no parâmetro de saída `ConsoleOutput`.<br /><br />Padrão: `false`.|  
|`CustomErrorRegularExpression`|Parâmetro `String` opcional.<br /><br /> Especifica uma expressão regular que é usada para identificar linhas de erro na saída da ferramenta. Isso é útil para ferramentas que produzem saída com formação incomum.<br /><br />Padrão: `null` (nenhum processamento personalizado).|  
|`CustomWarningRegularExpression`|Parâmetro `String` opcional.<br /><br /> Especifica uma expressão regular que é usada para identificar linhas de aviso na saída da ferramenta. Isso é útil para ferramentas que produzem saída com formação incomum.<br /><br />Padrão: `null` (nenhum processamento personalizado).|  
|`EchoOff`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa não emitirá a forma expandida do `Command` no log do MSBuild.<br /><br />Padrão: `false`.|
|`ExitCode`|Parâmetro somente leitura de saída `Int32` opcional.<br /><br /> Especifica o código de saída fornecido pelo comando executado.|  
|`IgnoreExitCode`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa ignora o código de saída fornecido pelo comando executado. Caso contrário, a tarefa retorna `false` se o comando executado retorna um código de saída diferente de zero.<br /><br />Padrão: `false`.|  
|`IgnoreStandardErrorWarningFormat`|Parâmetro `Boolean` opcional.<br /><br /> Se `false`, seleciona linhas na saída que correspondem ao formato de aviso/erro padrão e registra-as em log como erros e avisos. Se `true`, desabilite esse comportamento.<br /><br />Padrão: `false`.|  
|`Outputs`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém os itens de saída da tarefa. A tarefa `Exec` não define esses itens. Em vez disso, você pode fornecê-los como se ela os tivesse definido, para que eles podem ser usados posteriormente no projeto.|  
|`StdErrEncoding`|Parâmetro de saída `String` opcional.<br /><br /> Especifica a codificação do fluxo de erro padrão de tarefa capturada. O padrão é a codificação de saída do console atual.|  
|`StdOutEncoding`|Parâmetro de saída `String` opcional.<br /><br /> Especifica a codificação do fluxo de saída padrão de tarefa capturada. O padrão é a codificação de saída do console atual.|  
|`WorkingDirectory`|Parâmetro `String` opcional.<br /><br /> Especifica o diretório no qual o comando será executado.<br /><br />Padrão: o diretório de trabalho atual do projeto.|  
  
## <a name="remarks"></a>Comentários  
 Essa tarefa é útil quando uma tarefa [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] específica do trabalho que você deseja executar não está disponível. Entretanto, a tarefa `Exec`, diferente de tarefas mais específicas, não pode realizar operações adicionais de processamento ou condicionais com base no resultado da ferramenta ou do comando executado.
  
 A tarefa `Exec` chama *cmd.exe* em vez de invocar um processo diretamente.  
  
 Além dos parâmetros listados neste documento, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.ToolTaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.ToolTask>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base ToolTaskExtension](../msbuild/tooltaskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `Exec` para executar um comando.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Binaries Include="*.dll;*.exe"/>  
    </ItemGroup>  
  
    <Target Name="SetACL">  
        <!-- set security on binaries-->  
        <Exec Command="echo y| cacls %(Binaries.Identity) /G everyone:R"/>  
    </Target>  
</Project>  
```

## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)
