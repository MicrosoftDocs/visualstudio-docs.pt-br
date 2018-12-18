---
title: Fazendo linting de código em R
description: Como trabalhar com o suporte de linting interno do Visual Studio para R, incluindo opções do linter.
ms.date: 07/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.text_editor.r.lint
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: 4eaeb0165c049b035555fa63130746baa5fa208f
ms.sourcegitcommit: e5a382de633156b85b292f35e3d740f817715d47
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38978291"
---
# <a name="lint-r-code-in-visual-studio"></a>Fazer lint do código R no Visual Studio

O linter analisa o código para revelar possíveis erros, problemas de formatação e outros ruídos no código, como espaço em branco diferente. O uso de um linter também ajuda a incentivar determinadas convenções de codificação, como a maneira como os identificadores são nomeados. Essas convenções são úteis dentro das equipes e de outras situações colaborativas.

As RTVS (Ferramentas do R para Visual Studio) fornecem um linter interno para o R, cujo comportamento é controlado por meio de várias opções descritas neste artigo. Essas opções estão localizadas em **Ferramentas** > **Opções** > **Editor de Texto** > **R** > **Lint**.

O lint está desabilitado por padrão. Para habilitar o lint, defina a opção **Tudo** > **Habilitar lint** como **True**.

Quando estiver habilitado, o linter será executado no editor durante a digitação. Os problemas são exibidos como rabiscos verdes. No gráfico a seguir, por exemplo, as RTVS identificaram seis problemas de lint, incluindo o uso de `=` em vez de `<-` para uma atribuição, a falta de espaçamento em torno dos argumentos de função, o uso de identificadores em PascalCase e em maiúsculas e o uso de um ponto e vírgula. Passar o mouse sobre um problema fornece uma descrição.

![Exemplos de saída do linter para o código R](media/linting-01.png)

Geralmente, você altera as opções do linter dependendo das necessidades de um projeto ou um arquivo. Por exemplo, o código de exemplo de um curso online pode usar `=` em vez de `<-`, junto com identificadores de formatação Pascal. Esse código mostra avisos frequentes do linter, pois as opções padrão do linter sinalizam esses casos. Ao trabalhar com esse código, é possível desabilitar as opções em vez de gastar tempo corrigindo cada instância.

## <a name="assignment-group"></a>Grupo de atribuição

| Opção | Valor padrão | Efeito de lint |
| --- | --- | --- |
| **Impor \<-** | **True** | Identifica quando `<-` não é usado para a atribuição. |

## <a name="naming-group"></a>Grupo de nomenclatura

Essas opções sinalizam identificadores que usam diferentes convenções de nomenclatura:

| Opção | Valor padrão | Efeito de lint |
| --- | --- | --- |
| **Sinalizar camelCase** | **False** | Sinaliza identificadores que usam camelCase. |
| **Sinalizar nomes longos** | **False** | Sinaliza os identificadores cujos nomes excedem a configuração de **Tamanho máximo do nome**. |
| **Sinalizar vários pontos** | **True** | Sinaliza identificadores que usam vários pontos. |
| **Sinalizar PascalCase** | **True** | Sinaliza identificadores que usam PascalCase. |
| **Sinalizar snake_case** | **False** | Sinaliza identificadores que usam sublinhados. |
| **Sinalizar MAIÚSCULAS** | **True** | Sinaliza identificadores que usam todas maiúsculas. |
| **Tamanho máximo do nome** | **32** | O tamanho aplicado com a configuração **Sinalizar nomes longos**. |

## <a name="spacing-group"></a>Grupo de espaçamento

Essas opções, definidas como **True** por padrão, controlam o local em que o linter identifica problemas de espaçamento: após nomes de função, em torno de vírgulas, em torno de operadores, posições da chave de abertura e de fechamento, espaço antes de ( e espaço dentro de ().

## <a name="statements-group"></a>Grupo de instruções

| Opção | Valor padrão | Efeito de lint |
| --- | --- | --- |
| **Vários** | **True** | Identifica quando várias instruções estão na mesma linha. |
| **Ponto e vírgulas** | **True** | Identifica os usos de ponto e vírgula. |

## <a name="text-group"></a>Grupo de texto

| Opção | Valor padrão | Efeito de lint |
| --- | --- | --- |
| **Limite de tamanho da linha** | **False** | Define se o linter sinaliza linhas maiores que a opção **Tamanho máximo da linha**. |
| **Tamanho máximo da linha** | **80** | Define o tamanho da linha aplicado pela opção **Limite de tamanho da linha**. |

## <a name="whitespace-group"></a>Grupo de espaços em branco

Essas opções, definidas como **True** por padrão, controlam o local em que o linter identifica problemas de espaço em branco: uso de tabulações, uso de aspas duplas, linhas vazias à direita e espaço em branco à direita.