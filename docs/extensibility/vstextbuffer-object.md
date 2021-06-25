---
title: Objeto VSTextBuffer | Microsoft Docs
description: O objeto VSTextBuffer representa um fluxo de texto Unicode, que geralmente está associado a um arquivo. Este artigo lista as interfaces do VSTextBuffer.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VSTextBuffer
helpviewer_keywords:
- VSTextBuffer object, reference
- views [Visual Studio SDK], VSTextBuffer object
ms.assetid: c5f94b45-7249-4e1f-a53d-1d2a1c61e0ef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b3660a8dbb4a0a1280d5a3f428f73f3498244af7
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905170"
---
# <a name="vstextbuffer-object"></a>Objeto VSTextBuffer
O objeto de buffer de texto representa um fluxo de texto Unicode, que geralmente está associado a um arquivo. Um <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> objeto pode ser usado fora do contexto do editor principal, como em um assistente.

 A tabela a seguir mostra as interfaces de `VSTextBuffer` .

|Método|Descrição|
|------------|-----------------|
|[IOleCommandTarget](/windows/desktop/api/docobj/nn-docobj-iolecommandtarget)|Interface OLE padrão. Usado para desfazer/refazer tratamento no buffer.|
|[Ipersistfile](/windows/desktop/api/objidl/nn-objidl-ipersistfile)|Interface OLE padrão.|
|[Ipersiststream](/windows/desktop/api/objidl/nn-objidl-ipersiststream)|Interface OLE padrão.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|Permite a criação de ações de compostos (ou seja, ações agrupadas em uma única unidade de desfazer/refazer).|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|Habilita a persistência de dados de documento gerenciados pelo buffer de texto.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|Fornece serviços básicos; usado por muitos clientes.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextFind>|Usado para pesquisar um buffer.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|Fornece recursos de leitura e gravação usando coordenadas bidimensionais. Herdada de `IVsTextBuffer`.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|Fornece recursos de leitura e gravação usando coordenadas unidimensionais. Herdada de `IVsTextBuffer`.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|Fornece acesso rápido, orientado a fluxo e sequencial ao texto no buffer.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|Fornece acesso a uma coleção genérica de propriedades. A propriedade mais importante é o nome ou moniker do buffer. Você pode armazenar seus próprios dados aleatórios no buffer com essa interface criando um GUID e usando-os como uma chave.|
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|Dá suporte a pontos de conexão para eventos.|

## <a name="remarks"></a>Comentários
 O `VSTextBuffer` geralmente é encontrado por uma chamada em `QueryInterface` `IVsTextBuffer` . Para obter mais informações, consulte [Buffer de texto](/previous-versions/visualstudio/visual-studio-2015/extensibility/accessing-the-text-buffer-by-using-the-legacy-api?preserve-view=true&view=vs-2015).

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>
- <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>
- [Edição de figuras](https://www.microsoft.com/download/details.aspx?id=55984)