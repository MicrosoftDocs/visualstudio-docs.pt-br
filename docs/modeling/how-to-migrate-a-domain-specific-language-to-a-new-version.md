---
title: Como migrar uma linguagem específica do domínio para uma nova versão
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: f736a8d5b8e09bbb1c5a894e3f0f450de19fd02f
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967019"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>Como migrar uma linguagem específica do domínio para uma nova versão
Você pode migrar os projetos que definem e usam a linguagem específica de domínio para [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] da versão do [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] que foi distribuído com [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)].

 Uma ferramenta de migração é fornecida como parte do [!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)]. A ferramenta converte as soluções que usam ou definem as ferramentas DSL e projetos do Visual Studio.

 Você deve executar a ferramenta de migração explicitamente: ele não seja iniciado automaticamente quando você abre uma solução no Visual Studio. A ferramenta e o documento de diretrizes detalhadas podem ser encontradas no seguinte caminho:

 **% Programa Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>Antes de migrar seus projetos DSL
 A ferramenta de migração modifica os arquivos de projeto do Visual Studio (**. csproj**) e arquivos de solução (**. sln**).

#### <a name="to-prepare-projects-for-migration"></a>Para preparar os projetos para migração.

-   Verifique se o **. csproj** e **. sln** arquivos podem ser gravados. Se estiverem sob controle do código-fonte, certifique-se de que eles são check-out.

-   Faça uma cópia das pastas que você pretende migrar.

## <a name="migrating-a-collection-of-projects"></a>Migrar uma coleção de projetos

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>Migrar soluções e projetos DSL para Visual Studio 2010

1. Inicie a ferramenta de migração de DSL.

   -   Você pode clicar duas vezes a ferramenta no Windows Explorer (ou Explorador de arquivos) ou iniciar a ferramenta de prompt de comando. A ferramenta é neste local:

        **%ProgramFiles%\Microsoft visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

2. Escolha uma pasta que contém as soluções e projetos que você deseja converter.

   - Insira o caminho na caixa na parte superior da ferramenta, ou clique em **procurar**.

     A ferramenta de migração exibe uma árvore de projetos que definem ou usar DSLs. A árvore inclui cada projeto que usa o **Microsoft.VisualStudio.Modeling.Sdk** ou **TextTemplating** assemblies.

3. Examine a árvore de projetos e desmarque a opção de projetos que você não deseja converter.

   -   Selecione um projeto ou solução para ver uma lista das alterações que fará com que a ferramenta.

       > [!NOTE]
       >  As caixas de seleção que aparecem ao lado dos nomes de pasta não têm nenhum efeito. Você deve expandir as pastas para inspecionar os projetos e soluções.

4. Converta os projetos.

   1.  Clique em **converter**.

        Antes de cada arquivo de projeto é convertido, uma cópia da _project_**. csproj** é salvo como _projeto_**. vs2008.csproj**

        Uma cópia de cada _solution_**. sln** é salvo como _solução_**. vs2008.sln**

   2.  Investigue as conversões com falha que são relatadas.

        Falhas são relatadas na janela de texto. Além disso, o modo de exibição de árvore mostra um sinalizador vermelho em cada nó que falhou ao converter. Você pode clicar no nó para obter mais informações sobre essa falha.

5. **Transformar todos os modelos** em soluções que contêm com êxito convertidos em projetos.

   1.  Abra a solução.

   2.  Clique o **transformar todos os modelos** botão no cabeçalho do Gerenciador de soluções.

       > [!NOTE]
       >  Você pode fazer essa etapa desnecessária. Para obter mais informações, consulte [como automatizar a transformar todos os modelos](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\)).

6. Atualize seu código personalizado nos projetos convertidos.

   -   Tentativa de compilar os projetos e investigar quaisquer falhas.

   -   Teste seu designer.


[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>Consulte também

- [Postagens de blogs relacionadas](https://blogs.msdn.microsoft.com/visualstudioalm/tag/code-index/)