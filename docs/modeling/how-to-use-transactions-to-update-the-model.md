---
title: Como usar transações para atualizar o modelo
description: Saiba que as transações verificam se as alterações feitas no repositório são tratadas como um grupo e como usar transações para atualizar o modelo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e91e569573076d1614a9fa946b67f3bda01e6fba
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390536"
---
# <a name="how-to-use-transactions-to-update-the-model"></a>Como usar transações para atualizar o modelo
As transações verificam se as alterações feitas no repositório são tratadas como um grupo. As alterações que são agrupadas podem ser confirmadas ou revertidas como uma única unidade.

 Sempre que o código do programa modificar, adicionar ou excluir qualquer elemento na loja no SDK de visualização e modelagem do Visual Studio, ele deverá fazer isso dentro de uma transação. Deve haver uma instância ativa do <xref:Microsoft.VisualStudio.Modeling.Transaction> associada ao repositório quando a alteração acontece. Isso se aplica a todos os elementos de modelo, relações, formas, diagramas e suas propriedades.

 O mecanismo de transação ajuda a evitar Estados inconsistentes. Se ocorrer um erro durante uma transação, todas as alterações serão revertidas. Se o usuário executar um comando Undo, cada transação recente será tratada como uma única etapa. O usuário não pode desfazer partes de uma alteração recente, a menos que você as coloque explicitamente em transações separadas.

## <a name="opening-a-transaction"></a>Abrindo uma transação
 O método mais conveniente de gerenciar uma transação é com uma `using` instrução colocada em uma `try...catch` instrução:

```csharp
Store store; ...
try
{
  using (Transaction transaction =
    store.TransactionManager.BeginTransaction("update model"))
    // Outermost transaction must always have a name.
  {
    // Make several changes in Store:
    Person p = new Person(store);
    p.FamilyTreeModel = familyTree;
    p.Name = "Edward VI";
    // end of changes to Store

    transaction.Commit(); // Don't forget this!
  } // transaction disposed here
}
catch (Exception ex)
{
  // If an exception occurs, the Store will be
  // rolled back to its previous state.
}
```

 Se uma exceção que impede o final `Commit()` ocorrer durante as alterações, o repositório será redefinido para seu estado anterior. Isso ajuda a garantir que os erros não deixem o modelo em um estado inconsistente.

 Você pode fazer qualquer número de alterações dentro de uma transação. Você pode abrir novas transações dentro de uma transação ativa. As transações aninhadas devem ser confirmadas ou revertidas antes do término da transação que a contém. Para obter mais informações, consulte o exemplo para a <xref:Microsoft.VisualStudio.Modeling.Transaction.TransactionDepth%2A> propriedade.

 Para tornar as alterações permanentes, você deve fazer `Commit` a transação antes que ela seja descartada. Se ocorrer uma exceção que não é detectada dentro da transação, o repositório será redefinido para seu estado antes das alterações.

## <a name="rolling-back-a-transaction"></a>Revertendo uma transação
 Para garantir que o repositório permaneça ou seja revertido para seu estado antes da transação, você pode usar qualquer uma dessas táticas:

1. Gerar uma exceção que não é detectada dentro do escopo da transação.

2. Reverter a transação explicitamente:

    ```csharp
    this.Store.TransactionManager.CurrentTransaction.Rollback();
    ```

## <a name="transactions-do-not-affect-non-store-objects"></a>As transações não afetam objetos que não são de armazenamento
 As transações regem apenas o estado do repositório. Eles não podem desfazer alterações parciais que foram feitas em itens externos, como arquivos, bancos de dados ou objetos que você declarou com tipos comuns fora da definição de DSL.

 Se uma exceção puder deixar essa alteração inconsistente com a loja, você deverá lidar com essa possibilidade no manipulador de exceção. Uma maneira de garantir que os recursos externos permaneçam sincronizados com os objetos da loja é acoplar cada objeto externo a um elemento na loja usando manipuladores de eventos. Para obter mais informações, consulte [manipuladores de eventos propagar alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md).

## <a name="rules-fire-at-the-end-of-a-transaction"></a>As regras são acionadas no final de uma transação
 No final de uma transação, antes de a transação ser descartada, as regras anexadas aos elementos no repositório são acionadas. Cada regra é um método que é aplicado a um elemento de modelo que foi alterado. Por exemplo, há regras "corrigir" que atualizam o estado de uma forma quando seu elemento de modelo foi alterado e que cria uma forma quando um elemento de modelo é criado. Não há uma ordem de acionamento especificada. Uma alteração feita por uma regra pode disparar outra regra.

 Você pode definir suas próprias regras. Para obter mais informações sobre regras, consulte [respondendo e propagando alterações](../modeling/responding-to-and-propagating-changes.md).

 As regras não são acionadas após um comando Undo, refazer ou reversão.

## <a name="transaction-context"></a>Contexto de transação
 Cada transação tem um dicionário no qual você pode armazenar as informações desejadas:

 `store.TransactionManager`

 `.CurrentTransaction.TopLevelTransaction`

 `.Context.Add(aKey, aValue);`

 Isso é especialmente útil para transferir informações entre regras.

## <a name="transaction-state"></a>Estado da transação
 Em alguns casos, você precisa evitar a propagação de uma alteração se a alteração for causada por desfazer ou refazer uma transação. Isso pode acontecer, por exemplo, se você escrever um manipulador de valor de propriedade que possa atualizar outro valor na loja. Como a operação de desfazer redefine todos os valores na loja para seus Estados anteriores, não é necessário calcular os valores atualizados. Use este código:

```csharp
if (!this.Store.InUndoRedoOrRollback) {...}
```

 As regras podem ser acionadas quando o armazenamento é inicialmente carregado de um arquivo. Para evitar responder a essas alterações, use:

```csharp
if (!this.Store.InSerializationTransaction) {...}
```
