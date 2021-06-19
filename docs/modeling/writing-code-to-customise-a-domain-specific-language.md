---
title: Personalizar uma Linguagem Específica de Domínio
description: Saiba como usar código personalizado para acessar, modificar ou criar um modelo em uma linguagem específica do domínio (DSL).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2231ef94bee01558e2c26899a5d9a0c855489e94
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388042"
---
# <a name="write-code-to-customize-a-domain-specific-language"></a>Escrever o código para personalizar uma Linguagem Específica de Domínio

Esta seção mostra como usar código personalizado para acessar, modificar ou criar um modelo em um idioma específico do domínio.

Há vários contextos em que você pode escrever código que funciona com uma DSL:

- **Comandos personalizados.** Você pode criar um comando que os usuários podem invocar clicando com o botão direito do mouse no diagrama e que pode modificar o modelo. Para obter mais informações, [consulte Como adicionar um comando ao menu de atalho](../modeling/how-to-add-a-command-to-the-shortcut-menu.md).

- **Validação.** Você pode escrever um código que verifica se o modelo está em um estado correto. Para obter mais informações, consulte [Validação em uma linguagem Domain-Specific .](../modeling/validation-in-a-domain-specific-language.md)

- **Substituindo o comportamento padrão.** Você pode modificar muitos aspectos do código gerado de DslDefinition.dsl. Para obter mais informações, [consulte Substituindo e estendendo as classes geradas.](../modeling/overriding-and-extending-the-generated-classes.md)

- **Transformação texto.** Você pode escrever modelos de texto que contêm código que acessa um modelo e gera um arquivo de texto, por exemplo, para gerar o código do programa. Para obter mais informações, [consulte Gerando código de uma linguagem Domain-Specific .](../modeling/generating-code-from-a-domain-specific-language.md)

- **Outras Visual Studio extensões.** Você pode escrever extensões VSIX separadas que leem e modificam modelos. Para obter mais informações, [consulte Como abrir um modelo do arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md)

As instâncias das classes que você define em DslDefinition.dsl são mantidas em uma estrutura de dados chamada IMS *(Armazenamento* na Memória) ou *Armazenar*. As classes que você define em uma DSL sempre levam um Store como um argumento para o construtor. Por exemplo, se a DSL definir uma classe chamada Example:

`Example element = new Example (theStore);`

manter objetos no Store (em vez de apenas como objetos comuns) oferece vários benefícios.

- **Transações**. Você pode agrupar uma série de alterações relacionadas em uma transação:

     `using (Transaction t = store.TransactionManager.BeginTransaction("updates"))`

     `{`

     `// make several changes to Store elements here`

     `t.Commit();`

     `}`

     Se ocorrer uma exceção durante as alterações, para que o Commit() final não seja executado, o Store será redefinido para seu estado anterior. Isso ajuda você a garantir que os erros não deixe o modelo em um estado inconsistente. Para obter mais informações, [consulte Navegando e atualizando um modelo no código do programa.](../modeling/navigating-and-updating-a-model-in-program-code.md)

- **Relações binárias.** Se você definir uma relação entre duas classes, as instâncias em ambas as extremidades terão uma propriedade que navega para a outra extremidade. As duas extremidades sempre são sincronizadas. Por exemplo, se você definir uma relação de pai com funções chamadas Pais e Filhos, poderá escrever:

     `John.Children.Add(Mary)`

     As duas expressões a seguir agora são verdadeiras:

     `John.Children.Contains(Mary)`

     `Mary.Parents.Contains(John)`

     Você também pode obter o mesmo efeito escrevendo:

     `Mary.Parents.Add(John)`

     Para obter mais informações, [consulte Navegando e atualizando um modelo no código do programa.](../modeling/navigating-and-updating-a-model-in-program-code.md)

- **Regras e eventos**. Você pode definir regras que são a incêndio sempre que as alterações especificadas são feitas. As regras são usadas, por exemplo, para manter as formas no diagrama atualizadas com os elementos de modelo que elas apresentam. Para obter mais informações, consulte [Respondendo a e propagando alterações](../modeling/responding-to-and-propagating-changes.md).

- **Serialização**. O Store fornece uma maneira padrão de serializar os objetos que ele contém em um arquivo. Você pode personalizar as regras para serialização e resserção. Para obter mais informações, consulte [Personalização do armazenamento de arquivos e serialização XML.](../modeling/customizing-file-storage-and-xml-serialization.md)

## <a name="see-also"></a>Confira também

- [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md)