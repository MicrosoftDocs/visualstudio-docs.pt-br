---
title: Cores de sintaxe em um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring
- language services, syntax coloring
ms.assetid: f65ff67e-8c20-497a-bebf-5e2a5b5b012f
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 172f06f4e30f1320b6e17332cb2b54af91f7ed01
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31136049"
---
# <a name="syntax-coloring-in-a-legacy-language-service"></a>Cores de sintaxe em um serviço de linguagem herdado

O Visual Studio usa um serviço de cores para identificar elementos da linguagem e exibi-los com as cores especificadas em um editor.

## <a name="colorizer-model"></a>Modelo de colorizador
 A idioma serviço implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> interface, que é usado por editores. Essa implementação é um objeto separado do serviço de idioma, conforme mostrado na ilustração a seguir:

 ![Gráfico do colorizador SVC](../../extensibility/internals/media/figlgsvccolorizer.gif)

> [!NOTE]
>  O serviço de cores de sintaxe é separado do mecanismo de Visual Studio geral para colorir o texto. Para obter mais informações sobre o geral [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] mecanismo suporte coloração, consulte [usando fontes e cores](../../extensibility/using-fonts-and-colors.md).

 Além de colorizador, o serviço de linguagem pode fornecer itens pode ser coloridos personalizados que são usados pelo editor de anúncios que fornece itens personalizados de pode ser coloridos. Você pode fazer isso com a implementação de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> interface no mesmo objeto que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface. Retorna o número de itens pode ser coloridos personalizados quando o editor chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> método e retorna um item pode ser colorido personalizado individual quando chama o editor de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> método.

 O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> método retorna um objeto que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> interface. Se o serviço de linguagem dá suporte a valores de cor de 24 bits ou alto, ele deve implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interface no mesmo objeto, como o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> interface.

## <a name="how-a-vspackage-uses-a-language-service-colorizer"></a>Como um VSPackage usa um colorizador de serviço de linguagem

1.  O VSPackage deve obter o serviço de idioma apropriado, o que requer que o serviço de linguagem VSPackage para fazer o seguinte:

    1.  Usar um objeto que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> interface para obter o texto a ser coloridos.

         Texto geralmente é exibido usando um objeto que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface.

    2.  Obter o serviço de linguagem ao consultar o provedor de serviços de VSPackage para o GUID do serviço de linguagem. Serviços de idioma são identificados no registro pela extensão de arquivo.

    3.  Associar o serviço de linguagem com o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> chamando seu <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.SetLanguageServiceID%2A> método.

2.  O VSPackage pode obter e usar o objeto colorizador da seguinte maneira:

    > [!NOTE]
    > VSPackages que use o editor de núcleo não precisa obter uma linguagem de objetos de colorizador do serviço explicitamente. Assim que uma instância do editor de núcleo obtém um serviço de idioma apropriado, ele executa todas as tarefas de colorização mostradas aqui.

    1.  Obter o objeto de colorizador do serviço de linguagem, que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>, e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer2> interfaces, chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> método do serviço de linguagem <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> objeto.

    2.  Chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método para obter as informações de colorizador para um determinado intervalo de texto.

         <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> Retorna uma matriz de valores, um para cada caractere na extensão de texto que está sendo colorido. Os valores são índices em uma lista de item pode ser colorido é a lista de item pode ser colorido padrão mantidas pelo editor de núcleo ou uma lista de item personalizado que pode ser colorido mantido pelo serviço de idioma em si.

    3.  Use as informações de colorização retornadas pelo <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método para exibir o texto selecionado.

> [!NOTE]
>  Além de usar um colorizador de serviço de linguagem, um VSPackage também pode usar o texto do Visual Studio para fins gerais cores mecanismo. Para obter mais informações sobre esse mecanismo, consulte [usando fontes e cores](../../extensibility/using-fonts-and-colors.md).

## <a name="in-this-section"></a>Nesta seção
 [Implementando a coloração de sintaxe](../../extensibility/internals/implementing-syntax-coloring.md) aborda como um editor acessa um serviço de linguagem coloração de sintaxe e que o serviço de linguagem deve implementar para dar suporte a cores de sintaxe.

 [Como: usar itens internos de pode ser colorido](../../extensibility/internals/how-to-use-built-in-colorable-items.md) demonstra como usar itens pode ser coloridos internos do serviço de linguagem.

 [Itens personalizados de pode ser colorido](../../extensibility/internals/custom-colorable-items.md) aborda a implementação de itens pode ser coloridos personalizados.

## <a name="see-also"></a>Consulte também

- [Usando fontes e cores](../../extensibility/using-fonts-and-colors.md)