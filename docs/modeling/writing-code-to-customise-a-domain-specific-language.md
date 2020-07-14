---
title: Personalizar uma Linguagem Específica de Domínio
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b67a50623eb1924c4a18b57524c409f7eba6ab20
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546868"
---
# <a name="write-code-to-customize-a-domain-specific-language"></a>Escrever o código para personalizar uma Linguagem Específica de Domínio

Esta seção mostra como usar o código personalizado para acessar, modificar ou criar um modelo em uma linguagem específica de domínio.

Há vários contextos nos quais você pode escrever código que funciona com uma DSL:

- **Comandos personalizados.** Você pode criar um comando que os usuários podem invocar clicando com o botão direito do mouse no diagrama e que podem modificar o modelo. Para obter mais informações, consulte [como: adicionar um comando ao menu de atalho](../modeling/how-to-add-a-command-to-the-shortcut-menu.md).

- **Confirmação.** Você pode escrever código que verifica se o modelo está em um estado correto. Para obter mais informações, consulte [validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md).

- **Substituindo o comportamento padrão.** Você pode modificar muitos aspectos do código que é gerado a partir de DslDefinition. DSL. Para obter mais informações, consulte [substituindo e estendendo as classes geradas](../modeling/overriding-and-extending-the-generated-classes.md).

- **Transformação de texto.** Você pode escrever modelos de texto que contenham código que acesse um modelo e gere um arquivo de texto, por exemplo, para gerar código de programa. Para obter mais informações, consulte [gerando código de uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md).

- **Outras extensões do Visual Studio.** Você pode gravar extensões VSIX separadas que lêem e modificam modelos. Para obter mais informações, consulte [como: abrir um modelo do arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md)

As instâncias das classes que você define em DslDefinition. DSL são mantidas em uma estrutura de dados chamada IMS ( *repositório na memória* ) ou *Store*. As classes que você define em uma DSL sempre tomam um armazenamento como um argumento para o construtor. Por exemplo, se a sua DSL definir uma classe chamada exemplo:

`Example element = new Example (theStore);`

manter os objetos na loja (em vez de objetos comuns) fornece vários benefícios.

- **Transações**. Você pode agrupar uma série de alterações relacionadas em uma transação:

     `using (Transaction t = store.TransactionManager.BeginTransaction("updates"))`

     `{`

     `// make several changes to Store elements here`

     `t.Commit();`

     `}`

     Se ocorrer uma exceção durante as alterações, para que a confirmação final () não seja executada, o repositório será redefinido para seu estado anterior. Isso ajuda a garantir que os erros não deixem o modelo em um estado inconsistente. Para obter mais informações, consulte [navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

- **Relações binárias**. Se você definir uma relação entre duas classes, as instâncias em ambas as extremidades terão uma propriedade que navega para a outra extremidade. Os dois finais são sempre sincronizados. Por exemplo, se você definir uma relação de Parenthood com funções nomeadas pais e filhos, poderá escrever:

     `John.Children.Add(Mary)`

     As duas expressões a seguir agora são verdadeiras:

     `John.Children.Contains(Mary)`

     `Mary.Parents.Contains(John)`

     Você também pode obter o mesmo efeito escrevendo:

     `Mary.Parents.Add(John)`

     Para obter mais informações, consulte [navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

- **Regras e eventos**. Você pode definir regras que são acionadas sempre que são feitas alterações especificadas. As regras são usadas, por exemplo, para manter as formas do diagrama atualizadas com os elementos de modelo que eles apresentam. Para obter mais informações, consulte [respondendo e propagando alterações](../modeling/responding-to-and-propagating-changes.md).

- **Serialização**. O repositório fornece uma maneira padrão de serializar os objetos que ele contém em um arquivo. Você pode personalizar as regras para serialização e desserialização. Para obter mais informações, consulte [Personalizando o armazenamento de arquivos e a serialização de XML](../modeling/customizing-file-storage-and-xml-serialization.md).

## <a name="see-also"></a>Confira também

- [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md)