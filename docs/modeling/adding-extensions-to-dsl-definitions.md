---
title: Adicionando extensões a definições de DSL
description: Saiba como a extensão de Definição de DSL permite que você crie um pacote de extensões para uma DSL (linguagem específica do domínio).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4d9f1c92ebb879517d497af41fe98cec4492bd95
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384883"
---
# <a name="add-extensions-to-dsl-definitions"></a>Adicionar extensões a definições de DSL

A extensão definição de DSL permite que você crie um pacote de extensões para uma DSL (linguagem específica do domínio). A extensão DSL, que está contida em uma VSIX (Extensão de Integração Visual Studio), pode ser instalada no computador de um usuário da mesma maneira que uma DSL. Os recursos adicionais podem ser habilitados e desabilitados dinamicamente em tempo de executar. As DSLs não devem ser projetadas explicitamente para extensão e as extensões podem ser projetadas posteriormente ou por terceiros, sem alterar a DSL estendida.

As extensões DSL podem incluir os seguintes recursos:

- Propriedades para elementos de modelo e apresentação

- Decoradores para formas e conectores

- Classes, relações, formas e conectores

- Restrições de validação

- Guias e itens da caixa de ferramentas

Um usuário de uma DSL estendida pode criar e salvar um modelo que contém instâncias dos recursos adicionais. O modelo pode ser lido por outros usuários que instalaram a extensão apropriada. Os usuários que não instalaram a extensão não podem usar os recursos adicionais, mas podem atualizar e salvar um modelo sem perder os recursos adicionais.

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>Confira também

- [Postagens de blogs relacionadas](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)
