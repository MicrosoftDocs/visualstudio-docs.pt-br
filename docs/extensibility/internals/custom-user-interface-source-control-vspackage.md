---
title: Interface do usuário personalizada (VSPackage de controle do código-fonte) | Microsoft Docs
description: Saiba como criar uma interface do usuário (IU) personalizada no Visual Studio usando um VSPackage de controle do código-fonte para especificar os elementos da interface.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interface, source control packages
- source control packages, user interface
ms.assetid: f35ddb24-53bf-461e-b34f-7414f657c082
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1239b11e814ba08e4e481358f5e7fdd0e5dc666b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091026"
---
# <a name="custom-user-interface-source-control-vspackage"></a>Interface do usuário personalizada (VSPackage de controle do código-fonte)
Um VSPackage declara seus itens de menu e seus Estados padrão por meio do arquivo de tabela de comando (*. vsct*) do Visual Studio. O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado) exibe os itens de menu em seus Estados padrão até que o VSPackage seja carregado. Subsequentemente, o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método é chamado para habilitar ou Desabilitar itens de menu.

 Um VSPackage pode definir uma chave do registro para que o VSPackage possa ser carregado automaticamente dependendo de um contexto de interface do usuário do comando, embora normalmente um controle do código-fonte VSPackage deva ser carregado sob demanda em vez de apenas alternar para um contexto de interface de usuário específico. Para obter mais informações sobre a chave do registro **AutoLoadPackages** , consulte [Manage VSPackages](../../extensibility/managing-vspackages.md).

## <a name="vspackage-ui"></a>Interface do usuário do amVSPackage
 Um pacote de controle do código-fonte é implementado como um VSPackage e não usa nenhuma interface do usuário do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Cada VSPackage de controle do código-fonte deve especificar seus próprios elementos de interface do usuário, como itens de menu, grupos de menus, janelas de ferramentas, barras de ferramentas e qualquer interface do usuário necessária para definir opções específicas para o controle do código-fonte VSPackage. Esses elementos da interface do usuário podem ser habilitados estaticamente ou dinamicamente. Os elementos estáticos da interface do usuário são definidos em um arquivo *. vsct* e são exibidos independentemente de o VSPackage ser carregado ou não. Elementos de interface do usuário dinâmicos podem ser visíveis dependendo de um contexto de interface do usuário de comando específico, como <xref:EnvDTE.Constants.vsContextNoSolution> , ou como resultado de uma chamada para o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método. A visibilidade dos elementos dinâmicos da interface do usuário está em conformidade com a estratégia de carregamento atrasado de VSPackages.

## <a name="ui-constraints-on-source-control-vspackages"></a>Restrições de interface do usuário no controle do código-fonte VSPackages
 Como o VSPackage de controle do código-fonte não pode ser removido do IDE após ser carregado, o VSPackage deve ser capaz de inserir um estado inativo. Quando um VSPackage recebe uma notificação informando que ele não está mais ativo, o VSPackage desabilita sua interface do usuário e ignora qualquer interação de IDE externa. A implementação do VSPackage do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método deve ocultar comandos quando o VSPackage não estiver ativo.

 Cada VSPackage de controle do código-fonte deve implementar a `IVsSccProvider` interface. Dois métodos na interface <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> devem ser implementados pelo VSPackage.

 O VSPackage de controle do código-fonte pode ter se inscrito em vários eventos do IDE, que são implementados pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> , <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> e assim por diante. Além disso, o VSPackage pode ter implementado interfaces de retorno de chamada habilitadas para o registro, como o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> . Essas interfaces devem ser ignoradas quando inativas.

 A lista a seguir mostra as interfaces afetadas pelo estado ativo de um VSPackage de controle do código-fonte:

- Acompanhe eventos de documentos do projeto.

- Eventos da solução.

- Interfaces de persistência da solução. Quando inativo, os pacotes não devem gravar em arquivos *. sln* e *. suo* .

- Extensores de propriedade.

  As interfaces obrigatórias <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> , e também qualquer interface opcional associada ao controle do código-fonte, não são chamadas quando o controle do código-fonte VSPackage está inativo.

  Quando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE é iniciado, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] define o contexto da interface do usuário do comando como a ID da ID do VSPackage do controle do código-fonte padrão atual. Isso faz com que a interface do usuário estática do VSPackage de controle do código-fonte ativo apareça no IDE sem realmente carregar o VSPackage. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] pausa o VSPackage para se registrar com o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] antes de <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> fazer qualquer chamada para o VSPackage.

  A tabela a seguir descreve detalhes específicos sobre como o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE oculta diferentes itens da interface do usuário.

| Item da interface do usuário | Descrição |
| - | - |
| Menus e barras de ferramentas | O pacote de controle do código-fonte deve definir o menu inicial e os Estados de visibilidade da barra de ferramentas para a ID do pacote de controle do código-fonte na seção [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) do arquivo *. vsct* . Isso permite que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE defina o estado dos itens de menu adequadamente sem carregar o VSPackage e chamar uma implementação do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método. |
| Janelas da ferramenta | O controle do código-fonte VSPackage oculta todas as janelas de ferramentas que ela possui quando se torna inativa. |
| Páginas de opções específicas do controle do código-fonte VSPackage | A chave do registro **HKLM\SOFTWARE\Microsoft\VisualStudio\X.Y\ToolsOptionsPages\VisibilityCmdUIContexts** permite que um VSPackage defina os contextos nos quais é necessário que suas páginas de opções sejam exibidas. Uma entrada de registro sob essa chave teria que ser criada usando a ID de serviço (SID) do serviço de controle do código-fonte e atribuindo a ela um valor DWORD de 1. Sempre que um evento de interface do usuário ocorre em um contexto no qual o VSPackage de controle do código-fonte está registrado, o VSPackage será chamado se estiver ativo. |

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>
- <xref:EnvDTE.Constants.vsContextNoSolution>
- [Gerenciar VSPackages](../../extensibility/managing-vspackages.md)
