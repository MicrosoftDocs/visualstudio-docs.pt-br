---
title: Como compilar destinos específicos em soluções usando o MSBuild.exe | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, building specific targets in a solution
- msbuild.exe, building specific targets in a solution
- MSBuild, msbuild.exe
ms.assetid: f46feb9b-4c16-4fec-b6e1-36a959692ba3
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fb1dc2885d64999ac9f4d12568fd7da29a783d8e
ms.sourcegitcommit: 71218ffc33da325cc1b886f69ff2ca50d44f5f33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48880650"
---
# <a name="how-to-build-specific-targets-in-solutions-by-using-msbuildexe"></a>Como criar destinos específicos em soluções usando o MSBuild.exe
Use o *MSBuild.exe* para criar destinos específicos de projetos específicos em uma solução.  
  
#### <a name="to-build-a-specific-target-of-a-specific-project-in-a-solution"></a>Para criar um destino específico de um projeto específico em uma solução  
  
1.  Na linha de comando, digite `MSBuild.exe <SolutionName>.sln`, em que `<SolutionName>` corresponde ao nome de arquivo da solução que contém o destino que você deseja executar.  
  
2. Especifique o destino após a opção `-target:` no formato \<NomeProjeto>:\<NomeDestino>. Se o nome do projeto contiver algum dos caracteres `%`, `$`, `@`, `;`, `.`, `(`, `)` ou `'`, substitua-os por um `_` no nome de destino especificado.
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir executa o destino `Rebuild` do projeto `NotInSlnFolder` e, em seguida, executa o destino `Clean` do projeto `InSolutionFolder`, que está localizado na pasta de solução *NewFolder*.  
  
```cmd
msbuild SlnFolders.sln -target:NotInSlnfolder:Rebuild;NewFolder\InSolutionFolder:Clean
```

## <a name="troubleshooting"></a>Solução de problemas

Se quiser examinar as opções disponíveis para você, será possível usar uma opção de depuração fornecida pelo MSBuild para fazer isso. Defina a variável de ambiente `MSBUILDEMITSOLUTION=1` e crie sua solução. Isso produzirá um arquivo do MSBuild chamado *\<NomeSolução>.sln.metaproj* que mostra a exibição interna do MSBuild da solução no momento do build. Você pode inspecionar esta exibição para determinar quais destinos estão disponíveis para build.

Não compile com essa variável de ambiente definida a menos que precise dessa exibição interna. Essa configuração pode causar problemas ao criar projetos na sua solução.

## <a name="see-also"></a>Consulte também  
 [Referência de linha de comando](../msbuild/msbuild-command-line-reference.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [MSBuild](../msbuild/msbuild.md)  
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)
