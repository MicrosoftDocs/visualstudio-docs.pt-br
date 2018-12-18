---
title: -Clean (devenv.exe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- builds [Team System], cleaning files
- clean Devenv switch
- /clean Devenv switch
- Devenv, /clean switch
ms.assetid: 79929dfd-22c9-4cec-a0d0-a16f15b8f7e4
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c7827f11a93e517f81eb03cfe2e33305859b4d78
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948849"
---
# <a name="clean-devenvexe"></a>/Clean (devenv.exe)
Limpa todos os arquivos intermediários e diretórios de saída.

## <a name="syntax"></a>Sintaxe

```
devenv FileName /Clean [ /project projectnameorfile [/projectconfig name ] ]
```

## <a name="arguments"></a>Arguments
 `FileName`

 Necessário. O caminho completo e o nome do arquivo da solução ou do arquivo de projeto.

 /project `ProjName`

 Opcional. O caminho e o nome de um arquivo de projeto na solução. É possível inserir um caminho relativo da pasta `SolutionName` para o arquivo de projeto ou o nome de exibição do projeto ou o caminho completo e o nome do arquivo de projeto.

 /projectconfig `ProjConfigName`

 Opcional. O nome de uma configuração de build do projeto a ser usado ao limpar o `/project` nomeado.

## <a name="remarks"></a>Comentários
 Essa opção executa a mesma função que o comando de menu **Limpar Solução** dentro do IDE (ambiente de desenvolvimento integrado).

 Coloque as cadeias de caracteres que incluem espaços entre aspas duplas.

 As informações de resumo para limpezas e builds, incluindo erros, podem ser exibidas na janela **Comando** ou em qualquer arquivo de log especificado com a opção `/out`.

## <a name="example"></a>Exemplo
 O primeiro exemplo limpa a solução `MySolution`, usando a configuração padrão especificada no arquivo da solução.

 O segundo exemplo limpa o projeto `CSharpConsoleApp`, usando a configuração de build do projeto `Debug` dentro da configuração da solução `Debug` de `MySolution`.

```
Devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /Clean

devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /Clean /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig "Debug"
```

## <a name="see-also"></a>Consulte também

- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)