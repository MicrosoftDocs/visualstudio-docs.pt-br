---
title: Caixa de diálogo da linha de comando do evento de pré-build/pós-build | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cs.ProjectPropertiesBuildEventsBuilder
- vb.ProjectPropertiesBuildEventsBuilder
helpviewer_keywords:
- $(SolutionExt)
- $(ProjectDir)
- $(TargetPath)
- $(ProjectExt)
- $(TargetFileName)
- $(PlatformName)
- $(SolutionName)
- macros, build events
- $(SolutionPath)
- $(ProjectPath)
- $(ProjectFileName)
- $(DevEnvDir)
- $(TargetName)
- $(TargetDir)
- $(SolutionDir)
- $(TargetExt)
- $(OutDir)
- $(ConfigurationName)
- $(SolutionFileName)
- $(ProjectName)
- build events, macros
ms.assetid: d49b2c57-24bf-4fb2-8351-5c4b6cca938f
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f4c2f0297195dc1a9be23a1dd8aca980a6e32958
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49202508"
---
# <a name="pre-build-eventpost-build-event-command-line-dialog-box"></a>Caixa de diálogo Evento de Pré-build/Linha de Comando do Evento de Pós-build
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Você pode digitar eventos de pré ou de pós-build para a [Página de Eventos de Build, Designer de Projeto (C#)](../../ide/reference/build-events-page-project-designer-csharp.md) diretamente na caixa Editar, ou pode selecionar macros pré e pós-build em uma lista de macros disponíveis.  
  
> [!NOTE]
>  Eventos de pré-build não serão executados se o projeto estiver atualizado e nenhum build será disparado.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface de usuário  
 **Caixa de edição de linha de comando**  
 Contém os eventos a serem executados para pré ou pós-build.  
  
> [!NOTE]
>  Adicione uma instrução `call` antes de todos os comandos pós-build que executam arquivos .bat. Por exemplo, `call C:\MyFile.bat` ou `call C:\MyFile.bat call C:\MyFile2.bat`.  
  
 **Macros**  
 Expande a caixa de edição para exibir uma lista de macros para inserir na caixa de edição de linha de comando.  
  
 **Tabela de macros**  
 Lista as macros disponíveis e o valor delas. Consulte Macros abaixo para obter uma descrição de cada uma. Você pode selecionar somente uma macro por vez para inserir na caixa de edição de linha de comando.  
  
 **Inserir**  
 Insere na caixa de edição de inserções na linha de comando a macro selecionada na tabela de macros.  
  
### <a name="macros"></a>Macros  
 Você pode usar qualquer uma dessas macros para especificar locais de arquivos ou obter o nome real do arquivo de entrada no caso de várias seleções. Essas macros não diferenciam maiúsculas de minúsculas.  
  
|Macro|Descrição|  
|-----------|-----------------|  
|`$(ConfigurationName)`|O nome da configuração do projeto atual, por exemplo, “Depurar”.|  
|`$(OutDir)`|Caminho para o diretório do arquivo de saída com relação ao diretório do projeto. Isso é resolvido para o valor da propriedade Diretório de Saída. Inclui a barra invertida “\\”.|  
|`$(DevEnvDir)`|O diretório de instalação do Visual Studio (definido com a unidade e o caminho); inclui a barra invertida “\\” à direita.|  
|`$(PlatformName)`|O nome da plataforma de destino atual. Por exemplo, "AnyCPU".|  
|`$(ProjectDir)`|O diretório do projeto (definido com a unidade e o caminho); inclui a barra invertida “\\” à direita.|  
|`$(ProjectPath)`|O nome de caminho absoluto do projeto (definido com a unidade, o caminho, o nome de base e a extensão de arquivo).|  
|`$(ProjectName)`|O nome de base do projeto.|  
|`$(ProjectFileName)`|O nome de arquivo do projeto (definido com a extensão de arquivo e nome de base).|  
|`$(ProjectExt)`|A extensão de arquivo do projeto. Inclui o “.” antes da extensão de arquivo.|  
|`$(SolutionDir)`|O diretório da solução (definido com a unidade e o caminho); inclui a barra invertida “\\” à direita.|  
|`$(SolutionPath)`|O nome de caminho absoluto da solução (definido com a unidade, o caminho, o nome de base e a extensão de arquivo).|  
|`$(SolutionName)`|O nome de base da solução.|  
|`$(SolutionFileName)`|O nome de arquivo da solução (definido com a extensão de arquivo e nome de base).|  
|`$(SolutionExt)`|A extensão de arquivo da solução. Inclui o “.” antes da extensão de arquivo.|  
|`$(TargetDir)`|O diretório do arquivo de saída primária para o build (definido com a unidade e o caminho). Inclui a barra invertida “\\”.|  
|`$(TargetPath)`|O nome de caminho absoluto do arquivo de saída primária do build (definida com unidade, caminho, nome de base e extensão de arquivo).|  
|`$(TargetName)`|O nome base do arquivo de saída primária para o build.|  
|`$(TargetFileName)`|O nome do arquivo de saída primária do build (definido como nome de base e extensão de arquivo).|  
|`$(TargetExt)`|A extensão de arquivo do arquivo de saída primária para o build. Inclui o “.” antes da extensão de arquivo.|  
  
## <a name="see-also"></a>Consulte também  
 [Especificando eventos de build personalizados no Visual Studio](../../ide/specifying-custom-build-events-in-visual-studio.md)   
 [Página Eventos de Build, Designer de Projeto (C#)](../../ide/reference/build-events-page-project-designer-csharp.md)   
 [Como especificar eventos de build (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)   
 [Como especificar eventos de build (C#)](../../ide/how-to-specify-build-events-csharp.md)



