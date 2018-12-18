---
title: Interfaces (VSPackage de controle do código-fonte) e serviços relacionados | Microsoft Docs
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
- source control packages, interfaces
- interfaces, source control packages
ms.assetid: 3e96e838-5675-46bb-99cf-40d420086038
caps.latest.revision: 27
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8f308c0d8669bc8950578ffc615ebe64b91a4ea7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764322"
---
# <a name="related-services-and-interfaces-source-control-vspackage"></a>Serviços e interfaces relacionados (VSPackage de controle do código-fonte)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Esta seção lista todos o controle de fonte interfaces relacionadas à VSPackage no [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]. O VSPackage de controle de origem implementa algumas dessas interfaces e usa outras pessoas para realizar tarefas de controle do código-fonte.  
  
## <a name="interfaces-implemented-by-and-for-source-control-vspackages"></a>Interfaces implementadas por e para os VSPackages de controle do código-fonte  
 As seguintes interfaces são descritas no [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)], e o VSPackage de controle de origem implementa um subconjunto deles, dependendo de seu conjunto de recursos desejado. Algumas interfaces são marcados como obrigatório e deve ser implementado por cada VSPackage de controle de origem.  
  
 Para essas interfaces que não implementa um pacote, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] fornece uma implementação padrão. Observe que a implementação padrão é criada para o caso quando nenhum VSPackage é registrado e nenhum projeto é controlado. Um VSPackage de controle de fonte escrito adequadamente implementa interfaces necessários em vez de deixá-lo para a implementação padrão dessas interfaces.  
  
 Um VSPackage de controle do código-fonte deve implementar um serviço privado que encapsula a algumas ou todas as interfaces a seguir.  
  
 Interfaces são:  
  
-   Obrigatório: A entidade apropriada (controle de origem VSPackage, Stub de controle do código-fonte, projeto) deve implementar a interface.  
  
-   Recomendado: A entidade deve implementar essa interface; Caso contrário, a funcionalidade de controle do código-fonte pode ser limitada.  
  
-   Opcional: a entidade pode implementar essa interface para fornecer um conjunto mais rico de recursos.  
  
|Interface|Finalidade|Implementado por|Implementar?|  
|---------------|-------------|--------------------|----------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|Editores de chamar essa interface antes de modificar ou salvar um arquivo. O controle de fonte VSPackage pode fazer check-out do arquivo ou negar a operação se o check-out falhar.|Controle de fonte de VSPackage|Recomendado|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|Essa interface fornece funcionalidade de controle de origem básicos para projetos, como registrar e cancelar o registro de projetos com controle do código-fonte e fornecendo suporte para os glifos de controle de origem básicos.|Controle de fonte de VSPackage|Necessária|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|Essa interface é obtida a <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> usando o <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> função, ou ao simplesmente converter o objeto que implementa `IVsHierarchy` para `IVsSccProject2`. Ele é usado para obter os arquivos sob controle do código-fonte em um projeto ou para informar o projeto do status atual de controle de código-fonte ou local.|Projeto|Necessária|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>|O módulo de integração usa essa interface para definir o VSPackage ativo atual.|Controle de fonte de VSPackage|Necessária|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|Essa interface é baseada em um modelo de assinatura. Qualquer VSPackage pode sinalizar que deseja receber eventos de documento e ser avisado pelo shell em eventos que estão prestes a ocorrer. Ele é implementado e manipulado pelo [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], que por sua vez passa eventos Implementando o `IVsTrackProjectDocumentsEvents2` o VSPackage.|Stub de controle do código-fonte|Necessária|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3>|Essa interface fornece processamento em lotes, operações de leitura/gravação sincronizado e um avançado `OnQueryAddFiles` método.|Stub de controle do código-fonte|Necessária|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|**Gerenciador de soluções** e projetos de chamam essa interface quando novos arquivos são adicionados aos projetos ou quando arquivos e pastas são renomeadas ou excluídas dos projetos. O VSPackage de controle de origem pode fazer check-out do arquivo de projeto ou cancelar a operação.|Controle de fonte de VSPackage|Recomendado|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents3>|**Gerenciador de soluções** e projetos de chamar essa interface em resposta a chamadas feitas para os métodos da interface IVstrackProjectDocuments3. Operações de leitura/gravação o controle de fonte VSPackage pode rastrear a operações em lote, sincronizadas e trabalhar com um mais avançado `OnQueryAddFiles` método.|Controle de fonte de VSPackage|Recomendado|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccEnlistmentPathTranslation>|Essa interface oferece suporte a gerenciamento de inscrição para projetos Web.|Controle de fonte de VSPackage|Recomendado|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManagerTooltip>|Essa interface é usada para recuperar as dicas de ferramenta para os arquivos de controle do código-fonte nos projetos.|Controle de fonte de VSPackage|Opcional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccOpenFromSourceControl>|Essa interface oferece suporte à extensão do namespace.|Controle de fonte de VSPackage|Opcional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccControlNewSolution>|O VSPackage usa essa interface para integrar uma extensão do namespace para o **New**, **abra**, ou **salvar** caixas de diálogo. Consequentemente, projetos podem ser automaticamente adicionados ao controle do código-fonte na criação ou adicionados ao controle do código-fonte quando salvar operação está em vigor.|Controle de fonte de VSPackage|Opcional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>|O VSPackage usa essa interface para definir glifos adicionais como glifos de controle do código-fonte para nós em **Gerenciador de soluções**.|Controle de fonte de VSPackage|Opcional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccAddWebProjectFromSourceControl>|O **adicionar** caixa de diálogo para projetos Web usa essa interface. Ele fornece métodos para navegar para um local de controle de origem e para abrir um projeto Web adicionado anteriormente no repositório de controle de origem nesse local.|Controle de fonte de VSPackage|Recomendado|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc>|Essa interface fornece suporte para o carregamento assíncrono (em segundo plano) de projetos de controle de origem.|Controle de fonte de VSPackage|Opcional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromSccProjectEvents>|Essa interface permite que os projetos observar o progresso de carregamento assíncrono iniciado pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc>.|Projeto|Opcional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions>|Essa interface permite que o IDE consultar o VSPackage de controle de origem ativa. O IDE consulta o valor de configurações de controle de origem que têm significado, mesmo quando não há nenhum controle de origem ativa que VSPackage é registrado. Essa interface é implementada e tratada pelo [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].|Stub de controle do código-fonte|Necessária|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>|Essa interface é usada no registro o VSPackage de controle de origem.|Stub de controle do código-fonte|Necessária|  
|<xref:EnvDTE.SourceControl>|Essa interface é usada na automação. Como tal, ele expõe apenas as funções que podem ser executadas sem exibir nenhuma interface do usuário.|Controle de fonte de VSPackage|Opcional|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>|Essa interface é usada para salvar as configurações de controle de fonte de no arquivo de solução (. sln). As configurações incluem o local de controle do código-fonte e os sinalizadores de status de controle do código-fonte.|Controle de fonte de VSPackage|Recomendado|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>|Essa interface é usada para salvar as configurações de controle do código-fonte no arquivo de opções (. suo) da solução. Isso pode incluir configurações de controle de origem específicas do usuário, como local de inscrição do usuário atual.|Controle de fonte de VSPackage|Recomendado|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>|Essa interface é usada para monitorar eventos para executar operações como a verificação em arquivos de projeto antes de fechar soluções ou obtendo novos arquivos de controle de origem ao abrir um projeto.|Controle de fonte de VSPackage|Recomendado|  
  
## <a name="see-also"></a>Consulte também  
 [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)

