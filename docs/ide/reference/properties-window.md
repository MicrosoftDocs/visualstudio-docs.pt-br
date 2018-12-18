---
title: Janela Propriedades
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- properties [Visual Studio], Properties Window
- handler functions, Properties window
- handlers, Properties window
- Windows messages
- properties [Visual Studio], setting at design time
- properties [Visual Studio], editing
- Property Browser
- Windows messages, adding message handlers
- Properties window, overrides
- virtual functions, Properties window
- Properties window
ms.assetid: e6e0fa4f-75c4-4a52-af15-281cd61876ca
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2848a8197dfe62836918de51ae6e7d01677dac6d
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31947294"
---
# <a name="properties-window"></a>Janela Propriedades
Use esta janela para exibir e alterar as propriedades de tempo de design e os eventos dos objetos selecionados localizados em editores e designers. Você também pode usar a janela **Propriedades** para editar e exibir as propriedades do arquivo, do projeto e da solução. Você pode encontrar a janela **Propriedades** no menu **Exibir**. Também pode abri-la pressionando F4 ou digitando **Propriedades** na janela **Início Rápido**.

 A janela **Propriedades** exibe os diferentes tipos de campos de edição, dependendo das necessidades de uma determinada propriedade. Esses campos de edição incluem caixas de edição, listas suspensas e links a caixas de diálogo do editor personalizado. As propriedades mostradas em cinza são somente leitura.

## <a name="uielement-list"></a>Lista UIElement
 Nome do objeto

 Lista o objeto ou os objetos atualmente selecionados. Somente objetos do editor ou do designer ativo estão visíveis. Quando você seleciona vários objetos, somente as propriedades comuns a todos os objetos selecionados são exibidas.

 Categorizado

 Lista todas as propriedades e valores de propriedade para o objeto selecionado, por categoria. Você pode recolher uma categoria para reduzir várias propriedades visíveis. Ao expandir ou recolher uma categoria, você vê um sinal de mais (+) ou menos (-) à esquerda do nome da categoria. As categorias são listadas em ordem alfabética.

 Alfabético

 Classifica em ordem alfabética todas as propriedades e eventos de tempo de design para os objetos selecionados. Para editar uma propriedade não esmaecida, clique na célula à direita e insira as alterações.

 Páginas de propriedade

 Exibe a caixa de diálogo **Páginas de Propriedade** ou **Designer de Projeto** para o item selecionado. Páginas de Propriedades exibem um subconjunto, as mesmas ou um superconjunto das propriedades disponíveis na janela **Propriedades**. Use esse botão para exibir e editar propriedades relacionadas à configuração ativa do projeto.

 Propriedades

 Exibe as propriedades de um objeto. Muitos objetos também têm eventos que podem ser exibidos usando a janela **Propriedades**.

 Classificar por Fonte da Propriedade

 Agrupa propriedades por fonte, como herança, estilos aplicados e associações. Disponível somente ao editar arquivos XAML no designer.

 Eventos

 Exibe os eventos de um objeto.

> [!NOTE]
> Esse controle de barra de ferramentas da janela **Propriedades** só está disponível quando um formulário ou designer de controle está ativo no contexto de um projeto [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]. Ao editar arquivos XAML, os eventos são exibidos em uma guia separada da janela Propriedades.


 Mensagens

 Lista todas as mensagens do Windows. Permite adicionar ou excluir funções especificadas do manipulador para as mensagens fornecidas para a classe selecionada.

> [!NOTE]
> Esse controle de barra de ferramentas da janela **Propriedades** está disponível somente quando **Modo de Exibição de Classe** é a janela ativa no contexto de um projeto [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)].


 Substituições

 Lista todas as funções virtuais para a classe selecionada e permite adicionar ou excluir funções de substituição.

> [!NOTE]
> Esse controle de barra de ferramentas da janela **Propriedades** está disponível somente quando **Modo de Exibição de Classe** é a janela ativa no contexto de um projeto [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)].


 Painel de descrição

 Mostra o tipo de propriedade e uma breve descrição da propriedade. Você pode ativar e desativar a descrição da propriedade usando o comando Descrição no menu de atalho.

> [!NOTE]
> Esse controle de barra de ferramentas da janela **Propriedades** não está disponível ao editar arquivos XAML no designer.


 Exibição de miniatura

 Mostra uma representação visual do elemento selecionado no momento ao editar arquivos XAML no designer.

 Pesquisar

 Fornece uma função de Pesquisa de propriedades e eventos ao editar arquivos XAML no designer. A caixa de pesquisa responde a pesquisas de palavras parciais e atualiza os resultados da pesquisa à medida que você digita.

## <a name="see-also"></a>Consulte também

- [Referência de Propriedades do Projeto](../../ide/reference/project-properties-reference.md)
- [Personalizando layouts de janela](../../ide/customizing-window-layouts-in-visual-studio.md)