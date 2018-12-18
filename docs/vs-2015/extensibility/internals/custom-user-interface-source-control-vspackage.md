---
title: Interface do usuário personalizada (VSPackage de controle do código-fonte) | Microsoft Docs
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
- user interface, source control packages
- source control packages, user interface
ms.assetid: f35ddb24-53bf-461e-b34f-7414f657c082
caps.latest.revision: 29
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 237a79fe0225f54bd8be1f779f241bc54f13cd09
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51728533"
---
# <a name="custom-user-interface-source-control-vspackage"></a>Interface do usuário personalizada (VSPackage de controle do código-fonte)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um VSPackage declara seus itens de menu e seus estados padrão por meio do arquivo de tabela de comando do Visual Studio (. VSCT). O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE) exibe os itens de menu em seus estados padrão até que o VSPackage seja carregado. Subsequentemente, o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método é chamado para habilitar ou desabilitar itens de menu.  
  
 Um VSPackage pode definir uma chave do registro para que o VSPackage possa ser carregado automaticamente, dependendo do contexto de (UI) de interface de usuário um comando, embora geralmente controlam a uma fonte de VSPackage deve ser carregado sob demanda em vez de simplesmente alternar para um determinado contexto de interface do usuário. Para obter mais informações sobre a chave do registro AutoLoadPackages, consulte [gerenciar VSPackages](../../extensibility/managing-vspackages.md).  
  
## <a name="vspackage-ui"></a>Interface do usuário do VSPackage  
 Um pacote de controle do código-fonte é implementado como um VSPackage e não usa nenhuma interface do usuário do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Cada VSPackage de controle do código-fonte deve especificar seus próprios elementos de interface do usuário, como itens de menu, grupos de menus, janelas de ferramentas, barras de ferramentas e qualquer interface do usuário necessária para definir as opções específicas para o VSPackage de controle de origem. Esses elementos de interface do usuário podem ser habilitados estática ou dinamicamente. Elementos de interface do usuário estáticos são definidos em um arquivo. VSCT e são exibidos se o VSPackage está carregado ou não. Elementos de interface do usuário dinâmicos podem estar visíveis, dependendo do contexto de interface do usuário um comando específico, como <xref:EnvDTE.Constants.vsContextNoSolution>, ou como resultado de uma chamada para o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método. A visibilidade dos elementos de interface do usuário dinâmicas é compatível com a estratégia para carregamento atrasado de VSPackages.  
  
## <a name="ui-constraints-on-source-control-vspackages"></a>Restrições de interface do usuário em VSPackages de controle do código-fonte  
 Porque o VSPackage de controle de origem não é possível remover o IDE depois que ele for carregado, o VSPackage deve ser capaz de entrar em um estado inativo. Quando um VSPackage recebe a notificação de que ele não está mais ativo, o VSPackage desabilita sua interface do usuário e ignora qualquer interação externa do IDE. Implementação do VSPackage o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método deve ocultar comandos quando o VSPackage não está ativo.  
  
 Cada controle de origem VSPackage deve implementar o `IVsSccProvider` interface. Dois métodos na interface, <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A>, devem ser implementados por VSPackage.  
  
 O controle de fonte VSPackage pode se inscrever para vários eventos IDE, que são implementados pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>, <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>e assim por diante. Além disso, o VSPackage pode ter implementado interfaces habilitadas para registro de retorno de chamada, como o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>. Eles devem todos ser ignorados quando inativo.  
  
 A lista a seguir mostra as interfaces afetadas pelo estado ativo de um VSPackage de controle de origem:  
  
- Acompanhar eventos de documentos de projeto.  
  
- Eventos de solução.  
  
- Interfaces de persistência da solução. Quando estiver inativo, pacotes não devem gravar arquivos. sln e. suo.  
  
- Extensores de propriedade.  
  
  Exigida <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>, e também quaisquer interfaces opcionais associados ao controle do código-fonte, não são chamados quando o VSPackage de controle de origem está inativo.  
  
  Quando o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] é iniciado do IDE, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] define o contexto de interface do usuário do comando para a ID do controle de origem de padrão atual ID VSPackage. Isso faz com que a interface do usuário estática do controle de origem ativa VSPackage sejam exibidos no IDE sem realmente carregar o VSPackage. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] faz uma pausa para registrar com o VSPackage [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> antes que ele faz com que todas as chamadas para o VSPackage.  
  
  A tabela a seguir descreve detalhes específicos sobre como o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE oculta diferentes itens de interface do usuário.  
  
|Item de interface do usuário|Descrição|  
|-------------|-----------------|  
|Menus e barras de ferramentas|O pacote de controle de origem deve definir os estados iniciais de visibilidade de menu e barra de ferramentas para a ID de pacote de controle do código-fonte na [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) seção do arquivo. VSCT. Isso permite que o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE para definir o estado dos itens de menu adequadamente sem carregar o VSPackage e chamar uma implementação do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método.|  
|Janelas de ferramentas|O controle do código-fonte VSPackage oculta quaisquer janelas de ferramenta que possui quando ela se torna inativo.|  
|Páginas de opções específicas de VSPackage do controle de origem|A chave do registro HKLM\SOFTWARE\Microsoft\VisualStudio\X.Y\ToolsOptionsPages\VisibilityCmdUIContexts permite um VSPackage que definir os contextos em que ele requer que suas páginas de opções a serem exibidos. Uma entrada de registro sob essa chave precisa ser criada usando o serviço SID (ID) do serviço de controle de origem e atribuindo um valor DWORD de 1. Sempre que ocorrer um evento de interface do usuário em um contexto de VSPackage é registrado com o controle de origem, o VSPackage será chamado se ele estiver ativo.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>   
 <xref:EnvDTE.Constants.vsContextNoSolution>   
 [Gerenciar VSPackages](../../extensibility/managing-vspackages.md)

