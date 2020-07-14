---
title: Como usar o Visualizador de árvore do WPF | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- WPF, debugging
- debugging, WPF
ms.assetid: 2a1bf1cd-90f9-4d06-9fb4-1bfc925afef3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8e210d41541ef2fe0f7f8da149c23dc17645e44f
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348490"
---
# <a name="how-to-use-the-wpf-tree-visualizer"></a>Como usar o Visualizador de Árvore WPF
Você pode usar o visualizador de árvore do WPF para explorar a árvore visual de um objeto do WPF e exibir as propriedades de dependência do WPF para os objetos contidos nessa árvore. Para obter mais informações sobre árvores visuais, consulte [árvores no WPF](/dotnet/framework/wpf/advanced/trees-in-wpf). Para obter mais informações sobre propriedades de dependência, consulte [visão geral das propriedades de dependência](/dotnet/framework/wpf/advanced/dependency-properties-overview).

 Ao abrir o Visualizador de árvore do WPF, você verá dois painéis: a **árvore visual** à esquerda e as **Propriedades do** _painel nome_**:**_tipo_ à direita. Selecione qualquer objeto no painel de **árvore visual** e as **Propriedades do** painel _nome_**:**_tipo_ serão atualizadas automaticamente para mostrar as propriedades desse objeto.

 > [!NOTE]
 > Você também pode usar a [árvore visual dinâmica e o Gerenciador de propriedades ao vivo](../xaml-tools/inspect-xaml-properties-while-debugging.md) para examinar a árvore visual de objetos do WPF. O Visualizador de árvore do WPF é um recurso herdado e não está em desenvolvimento ativo.

### <a name="to-open-the-wpf-tree-visualizer"></a>Para abrir o visualizador de árvore do WPF

1. Em uma DataTip, em uma janela **Inspeção**, **Autos** ou **Locais**, ao lado do nome do objeto do WPF, clique na seta adjacente ao ícone de lupa.

     Uma lista de visualizadores é exibida.

2. Clique em **Visualizador de árvore do WPF**.

### <a name="to-search-the-visual-tree"></a>Para pesquisar a árvore visual

- No painel **Árvore Visual**, digite a cadeia de caracteres que deseja pesquisar na caixa **Pesquisar**.

  O visualizador de árvore do WPF localiza imediatamente o primeiro objeto na árvore visual que corresponde à cadeia de caracteres digitada. Digite mais caracteres para localizar uma correspondência mais precisa.

  - Para ir para a próxima correspondência na árvore visual, clique em **Avançar**.

  - Para voltar à correspondência anterior, clique em **Ant**.

  - Para limpar os critérios de pesquisa, clique em **Limpar**.

### <a name="to-search-the-properties-list"></a>Para pesquisar a lista de propriedades

- No painel **Propriedades do** _nome_**:**_tipo_ , digite a cadeia de caracteres que você deseja pesquisar na caixa de **filtro** .

  O visualizador de árvore do WPF localiza imediatamente as propriedades que correspondem à cadeia de caracteres digitada; agora, a lista exibe apenas as propriedades que correspondem à cadeia de caracteres digitada. Digite mais caracteres para localizar uma correspondência mais precisa.

  - Para limpar os critérios de pesquisa, clique em **Limpar**.

### <a name="to-close-the-visualizer"></a>Para fechar o visualizador

- Clique no ícone **Fechar** no canto superior direito da caixa de diálogo.

## <a name="see-also"></a>Veja também
- [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)
- [Árvores no WPF](/dotnet/framework/wpf/advanced/trees-in-wpf)
- [Visão geral das propriedades de dependência](/dotnet/framework/wpf/advanced/dependency-properties-overview)
