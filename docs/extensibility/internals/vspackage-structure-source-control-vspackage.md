---
title: Estrutura VSPackage (controle do código-fonte VSPackage) | Microsoft Docs
description: Saiba mais sobre o SDK do pacote de controle do código-fonte, que fornece diretrizes para um VSPackage com um implementador de controle do código-fonte para integração com o Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, structure
- source control packages, VSPackage overview
ms.assetid: 92722be7-b397-48c3-a7a7-0b931a341961
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ae037e3bda4ca09ee11969325b67ff0f8323722d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060686"
---
# <a name="vspackage-structure-source-control-vspackage"></a>Estrutura do VSPackage (VSPackage de controle do código-fonte)

O SDK do pacote de controle do código-fonte fornece diretrizes para criar um VSPackage que permite que um implementador de controle do código-fonte integre sua funcionalidade de controle do código-fonte com o ambiente do Visual Studio. Um VSPackage é um componente COM que normalmente é carregado sob demanda pelo IDE (ambiente de desenvolvimento integrado) do Visual Studio com base nos serviços anunciados pelo pacote em suas entradas de registro. Cada VSPackage deve implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> . Um VSPackage normalmente consome os serviços oferecidos pelo IDE do Visual Studio e proffers alguns serviços próprios.

Um VSPackage declara seus itens de menu e estabelece um estado de item padrão por meio do arquivo. vsct. O IDE do Visual Studio exibe os itens de menu nesse estado até que o VSPackage seja carregado. Subsequentemente, a implementação do VSPackage do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método é chamada para habilitar ou Desabilitar itens de menu.

## <a name="source-control-package-characteristics"></a>Características do pacote de controle do código-fonte

Um VSPackage de controle do código-fonte está profundamente integrado ao Visual Studio. A semântica VSPackage inclui:

- Interface a ser implementada em virtude de ser um VSPackage (a `IVsPackage` interface)

- Implementação do comando de interface do usuário (arquivo. vsct e implementação da <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface)

- Registro do VSPackage com o Visual Studio.

O VSPackage de controle do código-fonte deve se comunicar com essas outras entidades do Visual Studio:

- Projetos

- Editores

- Soluções

- Windows

- A tabela de documentos em execução

### <a name="visual-studio-environment-services-that-may-be-consumed"></a>Serviços de ambiente do Visual Studio que podem ser consumidos

<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>

Serviço SVsRegisterScciProvider

<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>

### <a name="vsip-interfaces-implemented-and-called"></a>Interfaces VSIP implementadas e chamadas

Um pacote de controle do código-fonte é um VSPackage e, portanto, pode interagir diretamente com outros VSPackages registrados com o Visual Studio. Para fornecer a amplitude completa da funcionalidade de controle do código-fonte, um VSPackage de controle do código-fonte pode lidar com interfaces fornecidas por projetos ou pelo shell.

Cada projeto do Visual Studio deve implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> para ser reconhecido como um projeto no IDE do Visual Studio. No entanto, essa interface não é especializada o suficiente para controle do código-fonte. Projetos que devem estar sob a implementação do controle do código-fonte <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> . Essa interface é usada pelo VSPackage de controle do código-fonte para consultar um projeto quanto ao seu conteúdo e fornecer glifos e informações de associação (as informações necessárias para estabelecer uma conexão entre o local do servidor e o local do disco de um projeto que está sob controle do código-fonte).

O VSPackage de controle do código-fonte implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> , que por sua vez permite que os projetos se registrem para controle do código-fonte e recupere seus glifos de status.

Para obter uma lista completa das interfaces que um VSPackage de controle do código-fonte deve considerar, consulte [serviços e interfaces relacionadas](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md).

## <a name="see-also"></a>Confira também

- [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)
- [Interfaces e serviços relacionados](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
