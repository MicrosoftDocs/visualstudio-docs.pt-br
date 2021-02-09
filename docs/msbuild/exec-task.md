---
title: Tarefa Exec | Microsoft Docs
description: Aprenda a usar a tarefa de execução do MSBuild para executar um programa ou comando especificado usando os argumentos especificados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 785d1bcfb8fdce5b09e749dcca17ff476a5d3f48
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99877155"
---
# <a name="exec-task"></a>tarefa Exec

Executa o programa ou comando especificado pelo uso dos argumentos especificados.

## <a name="parameters"></a>parâmetros

A tabela a seguir descreve os parâmetros da tarefa `Exec`.

|Parâmetro|Descrição|
|---------------|-----------------|
|`Command`|Parâmetro `String` obrigatório.<br /><br /> Os comandos a executar. Eles podem ser comandos do sistema, como attrib, ou um executável, como *program.exe*, *runprogram.bat* ou *setup.msi*.<br /><br /> Esse parâmetro pode conter várias linhas de comandos. Como alternativa, você pode colocar vários comandos em um arquivo em lotes e executá-lo por meio desse parâmetro.|
|`ConsoleOutput`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Cada item de saída é uma linha do fluxo de saída padrão ou de erro padrão emitido pela ferramenta. Isso será capturado somente se `ConsoleToMsBuild` for definido como `true`.|
|`ConsoleToMsBuild`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa vai capturar o erro padrão e a saída padrão da ferramenta e disponibilizá-los no parâmetro de saída `ConsoleOutput`.<br /><br />Padrão: `false`.|
|`CustomErrorRegularExpression`|Parâmetro `String` opcional.<br /><br /> Especifica uma expressão regular que é usada para identificar linhas de erro na saída da ferramenta. Isso é útil para ferramentas que produzem saída com formação incomum.<br /><br />Padrão: `null` (nenhum processamento personalizado).|
|`CustomWarningRegularExpression`|Parâmetro `String` opcional.<br /><br /> Especifica uma expressão regular que é usada para identificar linhas de aviso na saída da ferramenta. Isso é útil para ferramentas que produzem saída com formação incomum.<br /><br />Padrão: `null` (nenhum processamento personalizado).|
|`EchoOff`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa não emitirá a forma expandida do `Command` no log do MSBuild.<br /><br />Padrão: `false`.|
|`ExitCode`|Parâmetro de saída opcional somente leitura `Int32`.<br /><br /> Especifica o código de saída que é fornecido pelo comando executado, exceto que se a tarefa tiver registrado erros, mas o processo tiver um código de saída 0 (êxito), `ExitCode` será definido como-1.|
|`IgnoreExitCode`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa ignora o código de saída fornecido pelo comando executado. Caso contrário, a tarefa retorna `false` se o comando executado retorna um código de saída diferente de zero.<br /><br />Padrão: `false`.|
|`IgnoreStandardErrorWarningFormat`|Parâmetro `Boolean` opcional.<br /><br /> Se `false`, seleciona linhas na saída que correspondem ao formato de aviso/erro padrão e registra-as em log como erros e avisos. Se `true`, desabilite esse comportamento.<br /><br />Padrão: `false`.|
|`Outputs`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém os itens de saída da tarefa. A tarefa `Exec` não define esses itens. Em vez disso, você pode fornecê-los como se ela os tivesse definido, para que eles podem ser usados posteriormente no projeto.|
|`StdErrEncoding`|Parâmetro de saída `String` opcional.<br /><br /> Especifica a codificação do fluxo de erro padrão de tarefa capturada. O padrão é a codificação de saída do console atual.|
|`StdOutEncoding`|Parâmetro de saída `String` opcional.<br /><br /> Especifica a codificação do fluxo de saída padrão de tarefa capturada. O padrão é a codificação de saída do console atual.|
|`WorkingDirectory`|Parâmetro `String` opcional.<br /><br /> Especifica o diretório no qual o comando será executado.<br /><br />Padrão: o diretório de trabalho atual do projeto.|

[!INCLUDE [ToolTaskExtension arguments](includes/tooltaskextension-base-params.md)]

## <a name="remarks"></a>Comentários

Essa tarefa é útil quando uma tarefa do MSBuild específica para o trabalho que você deseja executar não está disponível. Entretanto, a tarefa `Exec`, diferente de tarefas mais específicas, não pode realizar operações adicionais de processamento ou condicionais com base no resultado da ferramenta ou do comando executado.

A `Exec` tarefa chama *cmd.exe* em vez de invocar diretamente um processo.

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

## <a name="see-also"></a>Confira também

- [Tarefas](../msbuild/msbuild-tasks.md)
- [Referência de tarefas](../msbuild/msbuild-task-reference.md)
