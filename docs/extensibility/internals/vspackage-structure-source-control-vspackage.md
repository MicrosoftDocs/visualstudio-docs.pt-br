---
title: Estrutura VSPackage (VSPackage de controle do código-fonte) | Microsoft Docs
description: Saiba mais sobre o SDK do Pacote de Controle do Código-Fonte, que fornece diretrizes para um VSPackage com um implementador de controle do código-fonte para integração com Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSPackages, structure
- source control packages, VSPackage overview
ms.assetid: 92722be7-b397-48c3-a7a7-0b931a341961
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b95c382342675d79c0c6e854b5fc087d495827e2
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898816"
---
# <a name="vspackage-structure-source-control-vspackage"></a>Estrutura do VSPackage (VSPackage de controle do código-fonte)

O SDK do Pacote de Controle do Código-Fonte fornece diretrizes para criar um VSPackage que permite que um implementador de controle do código-fonte integre sua funcionalidade de controle do código-fonte ao Visual Studio ambiente. Um VSPackage é um componente COM que normalmente é carregado sob demanda pelo IDE (ambiente de desenvolvimento integrado) do Visual Studio com base nos serviços anunciados pelo pacote em suas entradas do Registro. Cada VSPackage deve implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> . Um VSPackage normalmente consome serviços oferecidos pelo Visual Studio IDE e oferece alguns serviços próprios.

Um VSPackage declara seus itens de menu e estabelece um estado de item padrão por meio do arquivo .vsct. O Visual Studio IDE exibe os itens de menu nesse estado até que o VSPackage seja carregado. Posteriormente, a implementação do VSPackage do método <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> é chamada para habilitar ou desabilitar itens de menu.

## <a name="source-control-package-characteristics"></a>Características do pacote de controle do código-fonte

Um VSPackage de controle do código-fonte é profundamente integrado Visual Studio. A semântica vsPackage inclui:

- Interface a ser implementada em virtude de ser um VSPackage (a `IVsPackage` interface)

- Implementação de comando da interface do usuário (arquivo .vsct e implementação da <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface)

- Registro do VSPackage com Visual Studio.

O VSPackage do controle do código-fonte deve se comunicar com essas outras Visual Studio entidades:

- Projetos

- Editores

- Soluções

- Windows

- A tabela de documentos em execução

### <a name="visual-studio-environment-services-that-may-be-consumed"></a>Visual Studio serviços de ambiente que podem ser consumidos

<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>

Serviço SVsRegisterScciProvider

<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>

### <a name="vsip-interfaces-implemented-and-called"></a>Interfaces VSIP implementadas e chamadas

Um pacote de controle do código-fonte é um VSPackage e, portanto, ele pode interagir diretamente com outros VSPackages registrados com Visual Studio. Para fornecer toda a amplitude da funcionalidade de controle do código-fonte, um VSPackage de controle do código-fonte pode lidar com interfaces fornecidas por projetos ou pelo shell.

Todos os projetos Visual Studio devem ser implementados para serem reconhecidos como um <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> projeto no Visual Studio IDE. No entanto, essa interface não é especializada o suficiente para o controle do código-fonte. Projetos que devem estar sob controle do código-fonte implementam <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> . Essa interface é usada pelo VSPackage do controle do código-fonte para consultar um projeto quanto ao seu conteúdo e para fornecer a ele glifos e informações de associação (as informações necessárias para estabelecer uma conexão entre o local do servidor e o local do disco de um projeto que está sob controle do código-fonte).

O VSPackage do controle do código-fonte implementa , que, por sua vez, permite que os projetos se registrem para o controle do código-fonte e recuperem <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> seus glifos de status.

Para ver uma lista completa das interfaces que um VSPackage de controle do código-fonte deve considerar, consulte [Serviços e interfaces relacionadas.](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)

## <a name="see-also"></a>Confira também

- [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)
- [Interfaces e serviços relacionados](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
