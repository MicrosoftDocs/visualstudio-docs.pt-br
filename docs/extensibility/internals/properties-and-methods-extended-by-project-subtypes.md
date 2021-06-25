---
title: Propriedades e métodos estendidos por subtipos de projeto | Microsoft Docs
description: Saiba mais sobre os recursos que os subtipos de projeto podem melhorar ou modificar, o que permite que você personalize o comportamento dos sistemas de projeto do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project subtypes, extended methods
- project subtypes, extended properties
ms.assetid: 2b9833bf-8551-4ae1-93db-197ba645c65e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8ddcf020cf0b3e3e4f0f4a7c61ff1f15ce9ded5e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903535"
---
# <a name="properties-and-methods-extended-by-project-subtypes"></a>Propriedades e métodos estendidos por subtipos de projeto
Um subtipo de projeto tem muita potência para influenciar o comportamento do projeto, pois ele é construído como um agregador de um projeto base. Esta seção resume alguns dos recursos que podem ser aprimorados ou modificados por subtipos de projeto.

## <a name="features-gained-by-aggregation"></a>Recursos obtidos pela agregação
 A tabela a seguir resume muitos dos métodos que a agregação permite que os subtipos de projeto sejam substituídos em projetos base.

|Métodos substituídos por agregação|Subtipo de projeto|
|---------------------------------------|---------------------|
|De <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetGuidProperty%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetGuidProperty%2A>|Habilita um subtipo de projeto para<br /><br /> -Alterar a legenda e o ícone do nó do projeto.<br />– Substituir completamente o `Browse` objeto Project.<br />-Controlar se o projeto pode ser renomeado.<br />-Ordem de classificação de controle.<br />-Controle o contexto do usuário para obter ajuda dinâmica.|
|De <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>:<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetItemContext%2A>|Habilita um subtipo de projeto para controlar quais serviços contextuais são fornecidos aos designers e editores.|
|De <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>:<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A>|Habilita um subtipo de projeto para<br /><br /> -Participar do comando roteamento de comandos de projeto.<br />-Adicionar, remover ou desabilitar os comandos de ambiente do projeto e Gerenciador de Soluções comandos ativos.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>|Habilita o subtipo de projeto para filtrar o que o usuário vê na caixa de diálogo **Adicionar novo item** .|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGeneratorFactory>|Habilita um subtipo de projeto para<br /><br /> -Determinar o gerador padrão fornecido por uma extensão de arquivo.<br />-Mapeie um nome de gerador legível por humanos para um objeto COM.|

## <a name="properties-used-by-project-subtypes"></a>Propriedades usadas por subtipos de projeto
 O ambiente e o sistema de projeto base podem usar as propriedades <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID> e <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> enumerações detalhadas na tabela a seguir para habilitar um subtipo de projeto para controlar vários recursos do sistema de projeto.

|Propriedade VSHPROPID|Subtipo de projeto|
|------------------------|---------------------|
|`AddItemTemplatesGuid`|Permite que um subtipo de projeto controle o conteúdo da caixa de diálogo **Adicionar item** . O subtipo de projeto pode fornecer uma nova especificação de diretórios de modelo, adicionar novos tipos de itens, remover itens existentes e reorganizar um subconjunto dos itens na caixa de diálogo **Adicionar item** do projeto base.|
|`PropertyPagesCLSIDList`|Permite que um subtipo de projeto adicione ou remova páginas de propriedades independentes de configuração.|
|`CfgPropertyPagesCLSIDList`|Permite que um subtipo de projeto adicione ou remova páginas de propriedades dependentes de configuração.|
|`ExtObjectCATID`|Permite que um subtipo de projeto forneça um extensor de automação para os objetos de projeto ou item de projeto sabendo o CATID do extensor. Por exemplo, um subtipo de projeto pode fornecer um `Project.Extender("<subtype>")` objeto personalizado.|
|`BrowseObjectCATID`|Permite que um subtipo de projeto forneça um extensor de automação para o `Browse` objeto sabendo o CATID do extensor. Por exemplo, um subtipo de projeto pode adicionar propriedades extras à <xref:EnvDTE.Project.Properties%2A> coleção.|
|`CfgBrowseObjectCATID`|Permite que um subtipo de projeto forneça um extensor de automação para o objeto de procura de configuração de projeto. Por exemplo, um subtipo de projeto pode adicionar propriedades extras à <xref:EnvDTE.Configuration.Properties%2A> coleção.|
|`CfgExtObjectCATID`|Permite que um subtipo de projeto forneça um extensor de automação para o objeto de configuração.|
|`DefaultPlatformName`|Permite que um subtipo de projeto determine o nome da plataforma para os objetos de configuração do projeto.|

 O projeto base fornece uma implementação padrão das propriedades acima. O projeto base Obtém esses dados chamando `QueryInterface` por <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> no subtipo de projeto mais externo, permitindo que o subtipo de projeto substitua a implementação das propriedades.

## <a name="see-also"></a>Confira também
- [Design de subtipos de projeto](../../extensibility/internals/project-subtypes-design.md)
