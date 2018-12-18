---
title: Itens de coloração personalizados | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, custom colorable items
ms.assetid: b4d0ddee-c04b-48dc-ba82-f6068570cef0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 037cd62bea7051e8341101a888bd428b7f78e828
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49878786"
---
# <a name="custom-colorable-items"></a>Itens de coloração personalizados
Você pode substituir a lista de tipos para colorir, como palavras-chave e comentários, com a implementação de itens de coloração personalizados como parte de seu serviço de linguagem.  
  
## <a name="user-settings-of-colorable-items"></a>Configurações de usuário de itens de coloração  
 Você pode exibir o **fontes e cores** caixa de diálogo selecionando **opções** no **ferramentas** menu e selecionando **fontes e cores** sob **ambiente**. Quando você seleciona uma exibição, como **Editor de texto** ou **janela de comando**, o **exibir itens** caixa de listagem exibe todos os itens que pode ser coloridos que exibem. Você pode exibir e alterar a fonte, tamanho, cor de primeiro plano e cor de plano de fundo para cada item que pode ser colorido. Suas opções são armazenadas em cache no registro e acessadas pelo nome do item que pode ser colorido.  
  
## <a name="presentation-of-colorable-items"></a>Apresentação dos itens de coloração  
 Porque o IDE manipula substituições do usuário de itens de coloração na **fontes e cores** caixa de diálogo, você precisa apenas fornecer a cada item personalizado que pode ser colorido com um nome. Esse nome é o que aparece na **exibir itens** lista. Os itens de coloração aparecem em ordem alfabética. Para agrupar itens de coloração personalizados do seu serviço de linguagem, você pode começar cada nome com seu nome de idioma, por exemplo **NewLanguage - comentário** e **NewLanguage - palavra-chave**.  
  
> [!CAUTION]
>  Você deve incluir o nome do idioma no nome do item que pode ser colorido para evitar colisões com nomes existentes de item que pode ser colorido. Se você alterar o nome de um dos itens de coloração durante o desenvolvimento, você deve redefinir o cache que foi criado na primeira vez em que seus itens de coloração foram acessado. Você pode redefinir o cache experimental com as **CreateExpInstance** ferramenta, que é instalada com o SDK do Visual Studio, normalmente no diretório:  
>   
>  *C:\Program arquivos (x86) \Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin*
>   
>  Para redefinir o cache, digite **CreateExpInstance /Reset**. Para obter mais informações sobre **CreateExpInstance**, consulte [utilitário CreateExpInstance](../../extensibility/internals/createexpinstance-utility.md).  
  
 O primeiro item na sua lista de itens de coloração nunca é referenciado. O primeiro item corresponde a um índice do item que pode ser colorido 0, e [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] sempre fornece a cores de texto padrão e os atributos para aquele item. A maneira mais fácil de lidar com esse item não referenciado é fornecer um item que pode ser colorido de espaço reservado na sua lista como o primeiro item.  
  
## <a name="implement-custom-colorable-items"></a>Implementar itens de coloração personalizados  
  
1. Defina o que deve ser colorido em seu idioma, por exemplo, palavra-chave, operador e identificador.  
  
2. Crie uma enumeração desse itens de coloração.  
  
3. Associe os tipos de token retornados de um analisador ou um scanner com valores enumerados.  
  
    Por exemplo, os valores que representam os tipos de token pode ser os mesmos valores na enumeração de itens de coloração personalizados.  
  
4. Em sua implementação do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método no seu <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> de objeto, preencher a lista de atributos com os valores de enumeração seus itens de coloração personalizados que correspondentes aos tipos de token retornados do analisador ou scanner.  
  
5. Na mesma classe que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface, implemente o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> e seus dois métodos, <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>.  
  
6. Implementar a interface <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>.  
  
7. Se você quiser dar suporte a valores de cor de 24 bits ou alto, também implementam a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interface.  
  
8. No seu objeto de serviço de linguagem, crie uma lista que contém seu <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> objetos, um para cada item que pode ser colorido pode identificar o seu analisador ou um scanner.  
  
    Você pode acessar cada item na lista usando o valor correspondente a enumeração de itens de coloração personalizados. Use os valores de enumeração como um índice na lista. O primeiro item na lista nunca é acessado, pois ele corresponde ao texto padrão de estilo que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] sempre manipula em si. Você pode compensar isso inserindo um item de espaço reservado que pode ser colorido no início de sua lista.  
  
9. Em sua implementação do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> método, retornar o número de itens em sua lista de itens de coloração personalizados.  
  
10. Em sua implementação do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> método, retornar o item que pode ser colorido solicitado da sua lista.  
  
    Para obter um exemplo de como implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interfaces, consulte <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>.  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de um serviço de linguagem herdado](../../extensibility/internals/model-of-a-legacy-language-service.md)   
 [Coloração de sintaxe em editores personalizados](../../extensibility/syntax-coloring-in-custom-editors.md)   
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)   
 [Coloração de sintaxe de implementar](../../extensibility/internals/implementing-syntax-coloring.md)   
 [Como: usar itens de coloração internos](../../extensibility/internals/how-to-use-built-in-colorable-items.md)