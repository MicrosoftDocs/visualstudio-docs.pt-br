---
title: 'Como: usar o Visualizador de árvore do WPF | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0a478eae1e576ba2556d48f6527f6c9e2dab4ef6
ms.sourcegitcommit: 99d097d82ee4f9eff6f588e5ebb6b17d8f724b04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2018
ms.locfileid: "42902157"
---
# <a name="how-to-use-the-wpf-tree-visualizer"></a>Como usar o Visualizador de Árvore WPF
Você pode usar o visualizador de árvore do WPF para explorar a árvore visual de um objeto do WPF e exibir as propriedades de dependência do WPF para os objetos contidos nessa árvore. Para obter mais informações sobre árvores visuais, consulte [árvores no WPF](/dotnet/framework/wpf/advanced/trees-in-wpf). Para obter mais informações sobre propriedades de dependência, consulte [visão geral das propriedades de dependência](/dotnet/framework/wpf/advanced/dependency-properties-overview).  
  
 Quando você abre o Visualizador de árvore do WPF, você verá dois painéis: o **árvore Visual** à esquerda e o **propriedades de** _nome_**:**  _Tipo_ painel à direita. Selecione qualquer objeto na **árvore Visual** painel e o **propriedades de** _nome_**:**_tipo_ é painel atualizado automaticamente para mostrar as propriedades desse objeto.  
  
### <a name="to-open-the-wpf-tree-visualizer"></a>Para abrir o visualizador de árvore do WPF  
  
1.  Em um DataTip **Watch** janela **Autos** janela, ou **locais** janela, ao lado de um nome de objeto do WPF, clique na seta adjacente ao ícone de lupa.  
  
     Uma lista de visualizadores é exibida.  
  
2.  Clique em **Visualizador de árvore WPF**.  
  
### <a name="to-search-the-visual-tree"></a>Para pesquisar a árvore visual  
  
-   No **árvore Visual** painel, digite a cadeia de caracteres que você deseja procurar na **pesquisa** caixa.  
  
     O visualizador de árvore do WPF localiza imediatamente o primeiro objeto na árvore visual que corresponde à cadeia de caracteres digitada. Digite mais caracteres para localizar uma correspondência mais precisa.  
  
    -   Para ir para a próxima correspondência na árvore visual, clique em **próxima**.  
  
    -   Para voltar à correspondência anterior, clique em **Prev**.  
  
    -   Para limpar os critérios de pesquisa, clique em **limpar**.  
  
### <a name="to-search-the-properties-list"></a>Para pesquisar a lista de propriedades  
  
-   No **propriedades de** _nome_**:**_tipo_ painel, digite a cadeia de caracteres que você deseja procurar no **filtrar**caixa.  
  
     O visualizador de árvore do WPF localiza imediatamente as propriedades que correspondem à cadeia de caracteres digitada; agora, a lista exibe apenas as propriedades que correspondem à cadeia de caracteres digitada. Digite mais caracteres para localizar uma correspondência mais precisa.  
  
    -   Para limpar os critérios de pesquisa, clique em **limpar**.  
  
### <a name="to-close-the-visualizer"></a>Para fechar o visualizador  
  
-   Clique o **fechar** ícone no canto superior direito da caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)   
 [Árvores no WPF](/dotnet/framework/wpf/advanced/trees-in-wpf)   
 [Visão geral das propriedades da dependência](/dotnet/framework/wpf/advanced/dependency-properties-overview)
