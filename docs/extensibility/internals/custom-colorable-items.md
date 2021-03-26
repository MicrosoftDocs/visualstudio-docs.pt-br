---
title: Itens personalizáveis personalizados | Microsoft Docs
description: Saiba como criar itens coloridos personalizados como parte de um serviço de idioma, substituindo itens na caixa de diálogo fontes e cores, como palavras-chave e comentários.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- colorable items
- language services, custom colorable items
ms.assetid: b4d0ddee-c04b-48dc-ba82-f6068570cef0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f08c5c9e533e3a21ec4b87e7d148c3022ee0fed1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056786"
---
# <a name="custom-colorable-items"></a>Itens coloridos personalizados
Você pode substituir a lista de tipos para coloração, como palavras-chave e comentários, implementando itens colorable personalizados como parte do seu serviço de idioma.

## <a name="user-settings-of-colorable-items"></a>Configurações de usuário de itens coloráveis
 Você pode exibir a caixa de diálogo **fontes e cores** selecionando **Opções** no menu **ferramentas** e, em seguida, selecionando **fontes e cores** em **ambiente**. Quando você seleciona uma exibição, como o **Editor de texto** ou a **janela de comando**, a caixa de listagem **Exibir itens** mostra todos os itens coloráveis para essa exibição. Você pode exibir e alterar a fonte, o tamanho, a cor de primeiro plano e a cor da tela de fundo de cada item que pode ser colorido. Suas opções são armazenadas em um cache no registro e acessadas pelo nome de item com cores.

## <a name="presentation-of-colorable-items"></a>Apresentação de itens coloráveis
 Como o IDE trata as substituições de usuários de itens coloráveis na caixa de diálogo **fontes e cores** , você precisa fornecer apenas cada item Colorable personalizado com um nome. Esse nome é o que aparece na lista **Exibir itens** . Os itens coloráveis aparecem em ordem alfabética. Para agrupar os itens personalizáveis personalizados do serviço de idioma, você pode iniciar cada nome com o nome do idioma, por exemplo **NewLanguage-comment** e **NewLanguage-keyword**.

> [!CAUTION]
> Você deve incluir o nome do idioma no nome do item Colorable para evitar colisões com nomes de item Colorable existentes. Se você alterar o nome de um dos seus itens coloráveis durante o desenvolvimento, deverá redefinir o cache que foi criado na primeira vez em que os itens colorable foram acessados. Você pode redefinir o cache experimental com a ferramenta **CreateExpInstance** , que é instalada com o SDK do Visual Studio, normalmente no diretório:
>
> *C:\Arquivos de programas (x86) \Microsoft Visual Studio 14.0 \ VSSDK\VisualStudioIntegration\Tools\Bin*
>
> Para redefinir o cache, digite **CreateExpInstance/Reset reiniciar**. Para obter mais informações sobre **CreateExpInstance**, consulte [utilitário CreateExpInstance](../../extensibility/internals/createexpinstance-utility.md).

 O primeiro item na lista de itens coloráveis nunca é referenciado. O primeiro item corresponde a um índice de item colorável de 0 e [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] sempre fornece as cores de texto padrão e os atributos para esse item. A maneira mais fácil de lidar com esse item não referenciado é fornecer um item de espaço reservado em cores na sua lista como o primeiro item.

## <a name="implement-custom-colorable-items"></a>Implementar itens colorable personalizados

1. Defina o que deve ser colorido em seu idioma, por exemplo, palavra-chave, operador e identificador.

2. Crie uma enumeração desses itens coloráveis.

3. Associe os tipos de token retornados de um analisador ou scanner com os valores enumerados.

    Por exemplo, os valores que representam os tipos de token podem ser os mesmos valores na enumeração de itens colorable personalizados.

4. Em sua implementação do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> método em seu <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> objeto, preencha a lista de atributos com os valores de sua enumeração de itens colorable personalizados correspondentes aos tipos de token retornados do analisador ou do scanner.

5. Na mesma classe que implementa a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> interface, implemente a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> interface e seus dois métodos, <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> .

6. Implemente a interface <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>.

7. Se você quiser oferecer suporte a valores de cores de 24 ou de cor alta, também implemente a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interface.

8. No seu objeto de serviço de idioma, crie uma lista que contém seus <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> objetos, uma para cada item que pode ser colorido que seu analisador ou scanner possa identificar.

    Você pode acessar cada item na lista usando o valor correspondente da enumeração de itens colorable personalizados. Use os valores de enumeração como um índice na lista. O primeiro item da lista nunca é acessado, pois corresponde ao estilo de texto padrão que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] sempre se manipula. Você pode compensar isso inserindo um item de espaço reservado no início da lista.

9. Em sua implementação do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetItemCount%2A> método, retorne o número de itens na sua lista de itens colorable personalizados.

10. Em sua implementação do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> método, retorne o item Colorable solicitado da sua lista.

    Para obter um exemplo de como implementar as <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interfaces e, consulte <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> .

## <a name="see-also"></a>Confira também
- [Modelo de um serviço de linguagem herdado](../../extensibility/internals/model-of-a-legacy-language-service.md)
- [Cores de sintaxe em editores personalizados](../../extensibility/syntax-coloring-in-custom-editors.md)
- [Cores de sintaxe em um serviço de idioma herdado](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [Implementar a cor da sintaxe](../../extensibility/internals/implementing-syntax-coloring.md)
- [Como: usar itens de cores internos](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
