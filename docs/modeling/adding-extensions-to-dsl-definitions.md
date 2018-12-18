---
title: Adicionando extensões a definições de DSL
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: dc764df3037baeba36666ce896549018d86c2a21
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31947528"
---
# <a name="add-extensions-to-dsl-definitions"></a>Adicionar extensões a definições de DSL

Extensão de definição de DSL permite que você crie um pacote de extensões para uma domínio específico DSL (linguagem). Extensão de DSL, que está contido em um Visual Studio Integration extensão (VSIX), pode ser instalado no computador do usuário da mesma maneira como uma DSL. Os recursos adicionais podem ser habilitados e desabilitados em tempo de execução dinamicamente. DSLs não precisam ser explicitamente criado para a extensão e as extensões podem ser criadas mais tarde, ou por terceiros, sem alterar o DSL estendida.

Extensões DSL podem incluir os seguintes recursos:

-   Propriedades de elementos de modelo e apresentação

-   Decoradores para formas e conectores

-   Classes, relacionamentos, formas e conectores

-   Restrições de validação

-   Guias e itens de caixa de ferramentas

Um usuário de uma DSL estendido pode criar e salvar um modelo que contém as instâncias dos recursos adicionais. O modelo pode ser lido por outros usuários que tenham instalado a extensão apropriada. Os usuários que não instalaram a extensão não é possível usar os recursos adicionais, mas eles podem atualizar e salvar um modelo sem perder os recursos adicionais.

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>Consulte também

- [Postagens de blog relacionados](https://blogs.msdn.microsoft.com/visualstudioalm/tag/code-index/)
