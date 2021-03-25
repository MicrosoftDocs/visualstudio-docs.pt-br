---
title: Modelo de um serviço de linguagem herdado | Microsoft Docs
description: Use esse modelo de um serviço de linguagem mínimo para o editor principal do Visual Studio como um guia para criar seu próprio serviço de linguagem.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, model
ms.assetid: d8ae1c0c-ee3d-4937-a581-ee78d0499793
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 216bfaf9400847c265820e4bb5967fd3c992caa7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063208"
---
# <a name="model-of-a-legacy-language-service"></a>Modelo de um serviço de linguagem herdado
Um serviço de linguagem define os elementos e recursos para um idioma específico e é usado para fornecer ao editor informações específicas para esse idioma. Por exemplo, o editor precisa saber os elementos e as palavras-chave do idioma para dar suporte à cor da sintaxe.

 O serviço de linguagem trabalha em conjunto com o buffer de texto gerenciado pelo editor e a exibição que contém o editor. A opção de **informações rápidas** do Microsoft IntelliSense é um exemplo de um recurso fornecido por um serviço de linguagem.

## <a name="a-minimal-language-service"></a>Um serviço de linguagem mínima
 O serviço de linguagem mais básico contém os dois objetos a seguir:

- O *serviço de linguagem* implementa a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface. Um serviço de linguagem tem informações sobre a linguagem, incluindo seu nome, extensões de nome de arquivo, Gerenciador de janelas de código e Colorizer.

- O *Colorizer* implementa a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> interface.

  O desenho conceitual a seguir mostra um modelo de um serviço de linguagem básico.

  ![Gráfico de modelo do serviço de linguagem](../../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel") Modelo de serviço de linguagem básica

  A janela do documento hospeda a *exibição de documento* do editor, neste caso, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] editor principal. O modo de exibição de documento e o buffer de texto pertencem ao editor. Esses objetos funcionam com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o por meio de uma janela de documento especializada chamada de *janela de código*. A janela de código está contida em um <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> objeto que é criado e controlado pelo IDE.

  Quando um arquivo com uma determinada extensão é carregado, o editor localiza o serviço de idioma associado a essa extensão e passa para ele a janela de código chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> método. O serviço de linguagem retorna um *Gerenciador de janelas de código*, que implementa a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> interface.

  A tabela a seguir fornece uma visão geral dos objetos no modelo.

| Componente | Objeto | Função |
|------------------| - | - |
| Buffer de texto | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> | Um fluxo de texto de leitura/gravação Unicode. É possível que o texto use outras codificações. |
| Janela de código | <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> | Uma janela de documento que contém uma ou mais exibições de texto. Quando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o está no modo MDI (interface de vários documentos), a janela de código é um filho MDI. |
| Exibição de texto | <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> | Uma janela que permite ao usuário navegar e exibir texto usando o teclado e o mouse. Uma exibição de texto é exibida para o usuário como um editor. Você pode usar modos de exibição de texto em janelas de editor comuns, na janela saída e na janela imediata. Além disso, você pode configurar uma ou mais exibições de texto em uma janela de código. |
| Gerenciador de texto | Gerenciado pelo <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> serviço, do qual você obtém um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> ponteiro | Um componente que mantém informações comuns compartilhadas por todos os componentes descritos anteriormente. |
| Serviço de linguagem | Dependente de implementação; implementa <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> | Um objeto que fornece ao editor informações específicas de idioma, como realce de sintaxe, conclusão de instrução e correspondência de chaves. |

## <a name="see-also"></a>Confira também
- [Dados de documentos e exibição de documentos em editores personalizados](../../extensibility/document-data-and-document-view-in-custom-editors.md)
