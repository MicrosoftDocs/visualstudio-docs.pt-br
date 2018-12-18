---
title: Atualizando projetos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- upgrading VSPackages
- upgrading applications, strategies
- VSPackages, upgrade support
ms.assetid: e01cb44a-8105-4cf4-8223-dfae65f8597a
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: a3f045d947f968655923df16de8c02aafc12a34b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783753"
---
# <a name="upgrading-projects"></a>Atualizando projetos
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Altera para o modelo de projeto de uma versão do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para o próximo pode exigir que as soluções e projetos sejam atualizados para que eles podem executar a versão mais recente. O [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] fornece interfaces que podem ser usados para implementar o suporte à atualização em seus próprios projetos.  
  
## <a name="upgrade-strategies"></a>Estratégias de atualização  
 Para dar suporte a uma atualização, sua implementação do sistema de projeto deve definir e implementar uma estratégia de atualização. Para determinar sua estratégia, você pode optar por dar suporte a backup lado a lado (SxS), o backup de cópia ou ambos.  
  
-   Backup de SxS significa que um projeto copia somente os arquivos que precisam de atualização in loco, adicionando um sufixo de nome adequado do arquivo, por exemplo, ". old".  
  
-   Backup de cópia significa que um projeto copia todos os itens de projeto para um local de backup fornecido pelo usuário. Os arquivos relevantes no local original do projeto, em seguida, são atualizados.  
  
## <a name="how-upgrade-works"></a>Como a atualização funciona  
 Quando uma solução criada em uma versão anterior do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] é aberto em uma versão mais recente, as verificações IDE a solução de arquivo para determinar se ele precisa ser atualizado. Se a atualização for necessária, o **Assistente de atualização** é iniciado automaticamente para explicar ao usuário o processo de atualização.  
  
 Quando as necessidades de uma solução de atualização, ele consulta cada fábrica de projeto para sua estratégia de atualização. A estratégia determina se a fábrica de projeto dá suporte à cópia backup ou SxS. As informações são enviadas para o **Assistente de atualização**, que coleta as informações necessárias para o backup e apresenta as opções aplicáveis ao usuário.  
  
### <a name="multi-project-solutions"></a>Soluções multiprojeto  
 Se uma solução contiver vários projetos e as estratégias de atualização forem diferentes, como quando um projeto de C++ que só oferece suporte a backup de SxS e um projeto Web que só há suporte para backup de cópia, as fábricas de projeto devem negociar a estratégia de atualização.  
  
 A solução consulta cada fábrica de projeto para <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>. Em seguida, ele chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly%2A> para ver se os arquivos de projeto global precisam atualizar e determinar as estratégias de atualização com suporte. O **Assistente de atualização** , em seguida, é invocado.  
  
 Depois que o usuário conclui o assistente, <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> é chamado em cada fábrica de projeto para executar a atualização real. Para facilitar o backup, os métodos de IVsProjectUpgradeViaFactory fornecem o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> serviço para registrar em log os detalhes do processo de atualização. Esse serviço não pode ser armazenado em cache.  
  
 Depois de atualizar todos os arquivos globais relevantes, cada fábrica de projeto pode optar por criar uma instância de um projeto. A implementação do projeto deve dar suporte à <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> método é chamado para atualizar todos os itens de projeto relevantes.  
  
> [!NOTE]
>  O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> método não fornece o serviço SVsUpgradeLogger. Esse serviço pode ser obtido chamando <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>.  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Use o <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> serviço para verificar se você editar um arquivo antes de editá-lo e pode salvá-lo antes de salvá-lo. Isso ajudará o backup e implementações de atualização lidar com arquivos de projeto sob controle do código-fonte, arquivos com permissões insuficientes e assim por diante.  
  
 Use o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> durante todas as fases de backup de serviço e de atualização para fornecer informações sobre o êxito ou falha do processo de atualização.  
  
 Para obter mais informações sobre como fazer backup e atualização de projetos, consulte os comentários para IVsProjectUpgrade em vsshell2.idl.  
  
## <a name="see-also"></a>Consulte também  
 [Projetos](../../extensibility/internals/projects.md)   
 [Atualizando projetos personalizados](../../misc/upgrading-custom-projects.md)   
 [Atualizando Itens de Projeto](../../misc/upgrading-project-items.md)

