---
description: Use esta janela para exibir e alterar as propriedades de tempo de design e os eventos dos objetos selecionados localizados em editores e designers.
title: Janela Propriedades
ms.date: 11/04/2016
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
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ddbfb4d001f73e30296a35c2cff4aae0e0c527f9
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221113"
---
# <a name="properties-window"></a>Janela de Propriedades

Use esta janela para exibir e alterar as propriedades de tempo de design e os eventos dos objetos selecionados localizados em editores e designers. Você também pode usar a janela **Propriedades** para editar e exibir as propriedades do arquivo, do projeto e da solução. Você pode encontrar a janela **Propriedades** no menu **Exibir**. Também pode abri-la pressionando **F4** ou digitando **Propriedades** na janela de pesquisa.

A janela **Propriedades** exibe tipos diferentes de campos de edição, dependendo das necessidades de uma propriedade em particular. Esses campos de edição incluem caixas de edição, listas suspensas e links a caixas de diálogo do editor personalizado. As propriedades mostradas em cinza são somente leitura.

## <a name="uielement-list"></a>Lista de elementos de interface do usuário

Nome do objeto\
Relaciona o objeto ou os objetos atuais selecionados. Somente objetos do editor ou designer ativo ficam visíveis. Quando você seleciona vários objetos, somente as propriedades comuns a todos os objetos selecionados são exibidas.

Categorizado\
Relaciona todas as propriedades e os valores de propriedade do objeto selecionado, por categoria. Você pode recolher uma categoria para reduzir o número de propriedades visíveis. Ao expandir ou recolher uma categoria, você vê um sinal de mais (+) ou de menos (-) à esquerda do nome da categoria. As categorias são listadas em ordem alfabética.

Alfabético\
Classifica em ordem alfabética todas as propriedades de hora de criação e eventos dos objetos selecionados. Para editar uma propriedade não esmaecida, clique na célula à direita e insira as alterações.

Página de Propriedades\
Exibe a caixa de diálogo **Páginas de Propriedade** ou **Designer de Projeto** para o item selecionado. Páginas de Propriedades exibem um subconjunto, as mesmas ou um superconjunto das propriedades disponíveis na janela **Propriedades**. Use esse botão para exibir e editar propriedades relacionadas à configuração ativa do projeto.

Propriedades\
Exibe as propriedades de um objeto. Muitos objetos também têm eventos que podem ser exibidos usando a janela **Propriedades**.

Classificar por Fonte da Propriedade\
Agrupa propriedades por fonte, como herança, estilos aplicados e associações. Disponível somente ao editar arquivos XAML no designer.

Eventos\
Exibe os eventos de um objeto.

> [!NOTE]
> Esse controle de barra de ferramentas da janela **Propriedades** só está disponível quando um formulário ou designer de controle está ativo no contexto de um projeto [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]. Ao editar arquivos XAML, os eventos são exibidos em uma guia separada da janela Propriedades.

Mensagens\
Lista todas as mensagens do Windows. Permite adicionar ou excluir funções especificadas do manipulador para as mensagens fornecidas para a classe selecionada.

> [!NOTE]
> Esse controle de barra de ferramentas da janela **Propriedades** está disponível somente quando **Modo de Exibição de Classe** é a janela ativa no contexto de um projeto [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)].

Substituições\
Lista todas as funções virtuais para a classe selecionada e permite adicionar ou excluir funções de substituição.

> [!NOTE]
> Esse controle de barra de ferramentas da janela **Propriedades** está disponível somente quando **Modo de Exibição de Classe** é a janela ativa no contexto de um projeto [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)].

Painel de descrição\
Mostra o tipo de propriedade e uma breve descrição da propriedade. Você pode ativar e desativar a descrição da propriedade usando o comando Descrição no menu de atalho.

> [!NOTE]
> Esse controle de barra de ferramentas da janela **Propriedades** não está disponível ao editar arquivos XAML no designer.

Exibição de miniatura\
Mostra uma representação visual do elemento selecionado no momento ao editar arquivos XAML no designer.

Pesquisar\
Fornece uma função de Pesquisa de propriedades e eventos ao editar arquivos XAML no designer. A caixa de pesquisa responde a pesquisas de palavras parciais e atualiza os resultados da pesquisa à medida que você digita.

## <a name="see-also"></a>Confira também

- [Referência de propriedades do projeto](../../ide/reference/project-properties-reference.md)
- [Personalizando layouts de janela](../../ide/customizing-window-layouts-in-visual-studio.md)
