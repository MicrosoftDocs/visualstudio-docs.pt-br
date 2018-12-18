---
title: 'Como: migrar uma linguagem específica de domínio para uma nova versão | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6a1ae073-443e-45ca-8bc9-9b944362b449
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 52d8cb794b205631e7cc455241f48bcc78b879b9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49844465"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>Como migrar uma linguagem específica do domínio para uma nova versão
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode migrar os projetos que definem e usam a linguagem específica de domínio para [!INCLUDE[vs2010](../includes/vs2010-md.md)] da versão do [!INCLUDE[dsl](../includes/dsl-md.md)] que foi distribuído com [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)].  
  
 Uma ferramenta de migração é fornecida como parte do [!INCLUDE[vssdk_current_long](../includes/vssdk-current-long-md.md)]. A ferramenta converte [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projetos e soluções que usam ou definem as ferramentas DSL.  
  
 Você deve executar a ferramenta de migração explicitamente: ele não seja iniciado automaticamente quando você abre uma solução em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. A ferramenta e o documento de diretrizes detalhadas podem ser encontradas no seguinte caminho:  
  
 **% Programa Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**  
  
## <a name="before-you-migrate-your-dsl-projects"></a>Antes de migrar seus projetos DSL  
 A ferramenta de migração modifica [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] arquivos de projeto (**. csproj**) e arquivos de solução (**. sln**).  
  
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
       >  Você pode fazer essa etapa desnecessária. Para obter mais informações, consulte [como automatizar a transformar todos os modelos](http://msdn.microsoft.com/en-us/b63cfe20-fe5e-47cc-9506-59b29bca768a).  
  
6. Atualize seu código personalizado nos projetos convertidos.  
  
   -   Tentativa de compilar os projetos e investigar quaisquer falhas.  
  
   -   Teste seu designer.  
  
## <a name="see-also"></a>Consulte também  
 [Novidades no SDK de Visualização e Modelagem](../misc/what-s-new-in-visualization-and-modeling-sdk.md)



