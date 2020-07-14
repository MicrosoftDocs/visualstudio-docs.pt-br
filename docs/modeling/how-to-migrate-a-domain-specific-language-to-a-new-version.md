---
title: Como migrar uma linguagem específica do domínio para uma nova versão
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8bdaea1267d0bf69078aec5739291e72db8dfda
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532605"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>Como migrar uma linguagem específica do domínio para uma nova versão
Você pode migrar projetos que definem e usam a linguagem específica de domínio para a [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] partir da versão do [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] que foi distribuída com o [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] .

 Uma ferramenta de migração é fornecida como parte do [!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)] . A ferramenta converte projetos e soluções do Visual Studio que usam ou definem ferramentas DSL.

 Você deve executar a ferramenta de migração explicitamente: ela não é iniciada automaticamente quando você abre uma solução no Visual Studio. A ferramenta e o documento de orientação detalhada podem ser encontrados neste caminho:

 **% Program Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>Antes de migrar seus projetos de DSL
 A ferramenta de migração modifica arquivos de projeto do Visual Studio (**. csproj**) e arquivos de solução (**. sln**).

#### <a name="to-prepare-projects-for-migration"></a>Para preparar projetos para migração.

- Verifique se os arquivos **. csproj** e **. sln** podem ser gravados. Se eles estiverem sob controle do código-fonte, verifique se eles estão com check-out.

- Faça uma cópia das pastas que você pretende migrar.

## <a name="migrating-a-collection-of-projects"></a>Migrando uma coleção de projetos

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>Para migrar projetos e soluções de DSL para o Visual Studio 2010

1. Inicie a ferramenta de migração de DSL.

   - Você pode clicar duas vezes na ferramenta no Windows Explorer (ou explorador de arquivos) ou iniciar a ferramenta em um prompt de comando. A ferramenta está neste local:

        **%ProgramFiles%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

2. Escolha uma pasta que contenha soluções e projetos que você deseja converter.

   - Insira o caminho na caixa na parte superior da ferramenta ou clique em **procurar**.

     A ferramenta de migração exibe uma árvore de projetos que definem ou usam DSLs. A árvore inclui todos os projetos que usam os assemblies **Microsoft. VisualStudio. Modeling. SDK** ou **TextTemplating** .

3. Examine a árvore de projetos e desmarque os projetos que você não deseja converter.

   - Selecione um projeto ou solução para ver uma lista de alterações que a ferramenta fará.

       > [!NOTE]
       > As caixas de seleção que aparecem ao lado de nomes de pasta não têm nenhum efeito. Você deve expandir as pastas para inspecionar os projetos e as soluções.

4. Converta os projetos.

   1. Clique em **converter**.

        Antes de cada arquivo de projeto ser convertido, uma cópia de _Project_**. csproj** é salva como _Project_**. VS2008. csproj**

        Uma cópia de cada _solução_**. sln** é salva como _Solution_**. VS2008. sln**

   2. Investigue todas as conversões com falha que são relatadas.

        As falhas são relatadas na janela de texto. Além disso, o modo de exibição de árvore mostra um sinalizador vermelho em cada nó que falhou ao converter. Você pode clicar no nó para obter mais informações sobre essa falha.

5. **Transforme todos os modelos** em soluções que contenham projetos convertidos com êxito.

   1. Abra a solução.

   2. Clique no botão **transformar todos os modelos** no cabeçalho de Gerenciador de soluções.

       > [!NOTE]
       > Você pode tornar essa etapa desnecessária. Para obter mais informações, consulte [como automatizar a transformação de todos os modelos](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\)).

6. Atualize seu código personalizado nos projetos convertidos.

   - Tente compilar os projetos e investigue as falhas.

   - Teste seu designer.

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>Confira também

- [Postagens de blogs relacionadas](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)