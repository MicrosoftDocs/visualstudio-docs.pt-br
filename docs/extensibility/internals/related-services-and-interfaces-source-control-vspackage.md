---
title: Serviços e interfaces relacionados (VSPackage de controle do código-fonte)
titleSuffix: ''
description: Saiba mais sobre as interfaces relacionadas ao controle do código-fonte no SDK do Visual Studio. O pacote implementa algumas interfaces e usa outras para controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control packages, interfaces
- interfaces, source control packages
ms.assetid: 3e96e838-5675-46bb-99cf-40d420086038
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6385307c91541204d58228b489160888f79dec85
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903327"
---
# <a name="related-services-and-interfaces-source-control-vspackage"></a>Serviços e interfaces relacionados (VSPackage de controle do código-fonte)

Esta seção lista todas as interfaces relacionadas a VSPackage de controle do código-fonte no [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] . O VSPackage de controle do código-fonte implementa algumas dessas interfaces e usa outras para realizar tarefas de controle do código-fonte.

## <a name="interfaces-implemented-by-and-for-source-control-vspackages"></a>Interfaces implementadas pelo e para o controle do código-fonte VSPackages

 As interfaces a seguir são descritas no [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] , e o controle do código-fonte VSPackage implementa um subconjunto deles dependendo de seu conjunto de recursos desejado. Algumas interfaces são marcadas como obrigatórias e devem ser implementadas por cada VSPackage de controle do código-fonte.

 Para as interfaces que um pacote não implementa, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] fornece uma implementação padrão. Observe que a implementação padrão é projetada para o caso quando nenhum VSPackage é registrado e nenhum projeto é controlado. Um controle de código-fonte gravado corretamente implementa todas as interfaces necessárias em vez de deixá-la para a implementação padrão dessas interfaces.

 Um VSPackage de controle do código-fonte deve implementar um serviço privado que encapsula algumas ou todas as interfaces a seguir.

 As interfaces são:

- Obrigatório: a entidade apropriada (controle do código-fonte VSPackage, stub de controle do código-fonte, projeto) deve implementar a interface.

- Recomendado: a entidade deve implementar essa interface; caso contrário, a funcionalidade de controle do código-fonte poderá ser limitada.

- Opcional: a entidade pode implementar essa interface para fornecer um conjunto de recursos mais rico.

| Interface | Finalidade | Implementado por | Implementar? |
| - | - |--------------------------|-------------|
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | Os editores chamam essa interface antes de modificar ou salvar um arquivo. O VSPackage de controle do código-fonte pode fazer check-out no arquivo ou negar a operação se o check-out falhar. | VSPackage de controle do código-fonte | Recomendado |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | Essa interface fornece funcionalidade básica de controle do código-fonte para projetos, como registro e cancelamento de registro de projetos com controle do código-fonte e fornecimento de suporte para glifos de controle do código-fonte básico. | VSPackage de controle do código-fonte | Obrigatório |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> | Essa interface é obtida do <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> usando a <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> função ou simplesmente convertendo o objeto que está implementando `IVsHierarchy` para o `IVsSccProject2` . Ele é usado para obter os arquivos sob controle do código-fonte em um projeto ou para informar o projeto do status ou do local do controle do código-fonte atual. | Project | Obrigatório |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> | O módulo de integração usa essa interface para definir o VSPackage ativo atual. | VSPackage de controle do código-fonte | Obrigatório |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> | Essa interface é baseada em um modelo de assinatura. Qualquer VSPackage pode sinalizar que deseja receber eventos de documento e ser avisado pelo shell sobre eventos que estão prestes a acontecer. Ele é implementado e manipulado pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , que, por sua vez, passa eventos que implementam o `IVsTrackProjectDocumentsEvents2` para o VSPackage. | Stub de controle do código-fonte | Obrigatório |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | Essa interface fornece processamento em lotes, operações sincronizadas de leitura/gravação e um `OnQueryAddFiles` método avançado. | Stub de controle do código-fonte | Obrigatório |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> | **Gerenciador de soluções** e Projects chamam essa interface quando novos arquivos são adicionados aos projetos, ou quando arquivos e pastas são renomeados ou excluídos dos projetos. O VSPackage de controle do código-fonte pode fazer check-out do arquivo de projeto ou cancelar a operação. | VSPackage de controle do código-fonte | Recomendado |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents3> | **Gerenciador de soluções** e Projects chamam essa interface em resposta a chamadas feitas para os métodos da interface IVstrackProjectDocuments3. O VSPackage de controle do código-fonte pode acompanhar operações em lote, operações sincronizadas de leitura/gravação e trabalhar com um método mais avançado `OnQueryAddFiles` . | VSPackage de controle do código-fonte | Recomendado |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccEnlistmentPathTranslation> | Essa interface fornece suporte ao gerenciamento de inscrição para projetos Web. | VSPackage de controle do código-fonte | Recomendado |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManagerTooltip> | Essa interface é usada para recuperar dicas de ferramenta para os arquivos de origem controlada nos projetos. | VSPackage de controle do código-fonte | Opcional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccOpenFromSourceControl> | Essa interface fornece suporte à extensão de namespace. | VSPackage de controle do código-fonte | Opcional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccControlNewSolution> | O VSPackage usa essa interface para integrar uma extensão de namespace nas caixas de diálogo **novo**, **abrir** ou **salvar** . Consequentemente, os projetos podem ser adicionados automaticamente ao controle do código-fonte na criação ou adicionados ao controle do código-fonte quando uma operação de salvamento estiver em vigor. | VSPackage de controle do código-fonte | Opcional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> | O VSPackage usa essa interface para definir glifos adicionais como glifos de controle do código-fonte para nós no **Gerenciador de soluções**. | VSPackage de controle do código-fonte | Opcional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccAddWebProjectFromSourceControl> | A caixa de diálogo **Adicionar** para projetos Web usa essa interface. Ele fornece métodos para procurar um local de controle do código-fonte e para abrir um projeto Web adicionado anteriormente no repositório do controle do código-fonte nesse local. | VSPackage de controle do código-fonte | Recomendado |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> | Essa interface dá suporte ao carregamento assíncrono (em segundo plano) de projetos do controle do código-fonte. | VSPackage de controle do código-fonte | Opcional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromSccProjectEvents> | Essa interface permite que os projetos assistam ao progresso do carregamento assíncrono iniciado pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> . | Project | Opcional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | Essa interface permite que o IDE consulte o controle do código-fonte ativo VSPackage. O IDE consulta o valor das configurações de controle do código-fonte que têm significado, mesmo quando não há nenhum VSPackage de controle do código-fonte ativo registrado. Essa interface é implementada e manipulada pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . | Stub de controle do código-fonte | Obrigatório |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> | Essa interface é usada para registrar o VSPackage de controle do código-fonte. | Stub de controle do código-fonte | Obrigatório |
| <xref:EnvDTE.SourceControl> | Essa interface é usada na automação. Assim, ele expõe apenas funções que podem ser executadas sem exibir nenhuma interface do usuário. | VSPackage de controle do código-fonte | Opcional |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> | Essa interface é usada para salvar as configurações de controle do código-fonte no arquivo da solução (. sln). As configurações incluem os sinalizadores local do controle do código-fonte e status do controle do código-fonte. | VSPackage de controle do código-fonte | Recomendado |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> | Essa interface é usada para salvar as configurações de controle do código-fonte no arquivo de opções de solução (. suo). Isso pode incluir configurações de controle do código-fonte específicas do usuário, como o local de inscrição do usuário atual. | VSPackage de controle do código-fonte | Recomendado |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> | Essa interface é usada para monitorar eventos a fim de executar operações, como verificação de arquivos de projeto antes de fechar soluções ou obter novos arquivos do controle do código-fonte ao abrir um projeto. | VSPackage de controle do código-fonte | Recomendado |

## <a name="see-also"></a>Confira também
- [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)
