---
title: Ir para arquivo, ir para símbolo, ir para linha
ms.date: 08/14/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code editor, go to
- code editor, go to line
- go to line
- go to
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8d9ceeb7c4d24871bc0f2ddfc743c2c65e087205
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49907047"
---
# <a name="find-code-using-go-to-commands"></a>Localizar código usando comandos Ir Para

Os comandos **Ir Para** do Visual Studio executam uma pesquisa restrita no código para ajudá-lo a localizar rapidamente os itens especificados. É possível ir para uma linha, um tipo, um símbolo, um arquivo e um membro específico usando uma interface simples e unificada. Esse recurso existe no Visual Studio 2017 e posterior.

## <a name="how-to-use-it"></a>Como usá-lo

Entrada | Função
------------ | ---
**Teclado** | Pressione **Ctrl**+**T** ou **Ctrl**+**,**
**Mouse** | Selecione **Editar** > **Ir para** > **Ir para Todos**

Uma janela pequena é exibida na parte superior direita do editor de código.

![Janela Ir Para Todos](media/go-to-all.png)

Conforme você digita na caixa de texto, os resultados aparecem na lista suspensa abaixo da caixa de texto. Para ir até um elemento, escolha-o na lista.

![Janela Navegar Para](../ide/media/vside_navigatetowindow.png)

Também é possível inserir um ponto de interrogação (**?**) para obter ajuda adicional.

![Ajuda de Ir Para Todos](media/go-to-all-help.png)

## <a name="filtered-searches"></a>Pesquisas filtradas

Por padrão, o item especificado é pesquisado em todos os itens de solução. No entanto, é possível limitar sua pesquisa de código para tipos de elementos específicos ao preceder os termos de pesquisa com determinados caracteres. Também é possível alterar rapidamente o filtro de pesquisa ao escolher botões na barra de ferramentas da caixa de diálogo **Ir para**. Os botões que alteram os filtros de tipo estão do lado esquerdo e os botões que alteram o escopo da pesquisa estão do lado direito.

![Ir para membros](../ide/media/vside_navigation_toolbar.png)

### <a name="filter-to-a-specific-type-of-code-element"></a>Filtrar por um tipo específico de elemento de código

Para restringir sua pesquisa para um tipo de elemento de código específico, especifique um prefixo na caixa de pesquisa ou selecione um dos cinco ícones de filtro:

Prefixo | Ícone | Atalho | Descrição
:-: | - | - | -
:| ![Ícone de linha](media/gotoall-line-icon.png) | **Ctrl**+**G** | Ir para o número de linha especificado
f| ![Ícone de arquivos](media/gotoall-files-icon.png) | **Ctrl**+**1**, **Ctrl**+**F** | Ir para o arquivo especificado
r| ![Ícone de arquivos recentes](media/gotoall-recent-files-icon.png) | **Ctrl**+**1**, **Ctrl**+**R** | Ir para o arquivo visitado recentemente especificado
t| ![Ícone de tipos](media/gotoall-types-icon.png) | **Ctrl**+**1**, **Ctrl**+**T** | Ir para o tipo especificado
m| ![Ícone de membros](media/gotoall-members-icon.png) | **Ctrl**+**1**, **Ctrl**+**M** | Ir para o membro especificado
\#| ![Ícone de símbolos](media/gotoall-symbols-icon.png) | **Ctrl**+**1**, **Ctrl**+**S** | Ir para o símbolo especificado

### <a name="filter-to-a-specific-location"></a>Filtrar por um local específico

Para restringir sua pesquisa para um local específico, selecione um dos dois ícones de documentos:

Ícone | Descrição
---- | ---
![Documento Atual](media/gotoall_currentdocument.png) | Pesquisar apenas o documento atual
![Documentos Externos](media/gotoall_external.png) | Pesquisar documentos externos além daqueles localizados no projeto/solução

## <a name="camel-casing"></a>Concatenação com maiúsculas e minúsculas

Se você usar [concatenação com maiúsculas e minúsculas](https://en.wikipedia.org/wiki/Camel_case) em seu código, será possível encontrar elementos de código com mais rapidez, inserindo somente as letras maiúsculas do nome do elemento de código. Por exemplo, se o código tem um tipo chamado `CredentialViewModel`, é possível refinar a pesquisa escolhendo o filtro **Tipo** (**t**) e, em seguida, inserindo apenas as letras maiúsculas do nome (`CVM`) na caixa de diálogo Ir Para. Esse recurso pode ser útil caso seu código tenha nomes longos.

![Janela Navegar Para – pesquisando com letras maiúsculas](../ide/media/vside_capitalsearch.png)

## <a name="settings"></a>Configurações

Selecionando o ícone de engrenagem ![Ícone de engrenagem](media/gotoall_gear.png) permite que você altere como esse recurso funciona:

Configuração | Descrição
------- | ---
Usar guia de visualização | Exibir o item selecionado imediatamente na guia de visualização do IDE
Mostrar detalhes | Exibir informações do projeto, do arquivo, da linha e de resumo dos comentários da documentação na janela
Centralizar janela | Mover esta janela para a parte superior central do editor de códigos e não para a parte superior direita

## <a name="see-also"></a>Consulte também

- [Navegar pelo código](../ide/navigating-code.md)
- [Caixa de diálogo Ir Para Linha](../ide/reference/go-to-line.md)
- [Ir para Definição e Definição de Pico](../ide/go-to-and-peek-definition.md)