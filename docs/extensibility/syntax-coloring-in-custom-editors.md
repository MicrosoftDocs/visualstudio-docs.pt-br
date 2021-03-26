---
title: Cores de sintaxe em editores personalizados | Microsoft Docs
description: Saiba mais sobre a cor da sintaxe nos editores personalizados do SDK do ambiente do Visual Studio, que exibe as cores especificadas para uma determinada exibição de documento.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - syntax coloring
ms.assetid: 74900b9a-baef-432a-8231-4568fb5e19ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 06cd4ae1db1187cc650a4fd9486f4b1686c6b015
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063689"
---
# <a name="syntax-coloring-in-custom-editors"></a>Coloração de sintaxe em editores personalizados
Os editores do SDK do ambiente do Visual Studio, incluindo o editor principal, usam os serviços de linguagem para identificar itens sintáticos específicos e os exibem com cores especificadas para uma determinada exibição de documento.

## <a name="colorization-requirements"></a>Requisitos de colorização
 Todos os editores que implementam o Colorizer de um serviço de linguagem devem:

1. Use um objeto que implementa <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> para gerenciar o texto a ser colorido e um objeto que está implementando <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para fornecer uma exibição de documento do texto.

2. Obtenha uma interface para um serviço de idioma específico consultando o provedor de serviços do VSPackage usando o GUID de identificação do serviço de idiomas.

3. Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> método de implementação do objeto <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> . Esse método associa o serviço de linguagem à <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> implementação que o VSPackage usa para gerenciar o texto a ser colorido.

## <a name="core-editor-usage-of-a-language-services-colorizer"></a>Uso do editor de núcleo do Colorizer de um serviço de linguagem
 Quando um serviço de linguagem com um Colorizer é obtido por uma instância do editor principal, a análise e renderização de texto por um Colorizer de serviço de linguagem ocorre automaticamente sem a necessidade de nenhuma intervenção adicional de sua parte.

 O IDE de forma transparente:

- Chama o Colorizer conforme necessário para analisar e analisar o texto à medida que ele é adicionado ou modificado na implementação do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> .

- Garante que a exibição fornecida pelo modo de exibição de documento fornecido pela <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> implementação seja atualizada e repintada usando as informações retornadas pelo Colorizer.

## <a name="non-core-editor-usage-of-a-language-services-colorizer"></a>Uso de editor não núcleo de Colorizer de um serviço de linguagem
 As instâncias de editor não núcleo também podem usar um serviço de colorização de sintaxe de serviço de linguagem, mas devem recuperar e aplicar explicitamente o Colorizer do serviço e redesenhar suas próprias exibições de documento.

 Para fazer isso, um editor não principal deve:

1. Obtenha um objeto Colorizer do serviço de linguagem (que implementa <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2> ). O VSPackage faz isso chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> método na interface do serviço de linguagem.

2. Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método para solicitar que um determinado trecho de texto seja colorido.

     O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método retorna uma matriz de valores, um para cada letra no intervalo de texto que está sendo colorido. Ele também identifica o trecho de texto como um tipo específico de item colorable, como um comentário, uma palavra-chave ou um tipo de dados.

3. Use as informações de colorização retornadas por <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> para redesenhar e exibir seu texto.

> [!NOTE]
> Além de usar o Colorizer de um serviço de linguagem, um VSPackage pode optar por usar o mecanismo de coloração de texto do SDK do ambiente do Visual Studio para fins gerais. Para obter mais informações sobre esse mecanismo, consulte [usando fontes e cores](/previous-versions/visualstudio/visual-studio-2015/extensibility/using-fonts-and-colors?preserve-view=true&view=vs-2015).

## <a name="see-also"></a>Confira também

- [Coloração de sintaxe em um serviço de linguagem herdado](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [Implementando a coloração de sintaxe](../extensibility/internals/implementing-syntax-coloring.md)
- [Como usar itens de coloração internos](../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [Itens personalizados que podem ser coloridos](../extensibility/internals/custom-colorable-items.md)