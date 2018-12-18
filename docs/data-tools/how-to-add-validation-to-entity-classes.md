---
title: 'Como: adicionar validação a classes de entidade'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 61107da9-7fa3-4dba-b101-ae46536f52c4
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: d102bdf20349d6bd4efdecd1c460f1e46646eb37
ms.sourcegitcommit: e9d1018a01af62c3dc5aeb6b325faba7e20bd496
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37089332"
---
# <a name="how-to-add-validation-to-entity-classes"></a>Como: adicionar validação a classes de entidade
*Validando* classes de entidade é o processo de confirmar que os valores inseridos em objetos de dados estão em conformidade com as restrições no esquema de um objeto e também as regras estabelecidas para o aplicativo. Validar dados antes de enviar atualizações para o base de dados subjacente é uma boa prática que reduz erros. Também reduz o número potencial de processamentos entre um aplicativo e o base de dados.

 O [LINQ to SQL das ferramentas no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md) fornece os métodos parciais que permitem aos usuários estender o código gerado pelo designer que é executado durante inserções, atualizações e exclusões de entidades completos e também durante e após a coluna individual alterações.

> [!NOTE]
>  Este tópico fornece as etapas básicas para adicionar validação a classes de entidade usando o **Relational Designer**. Porque ele pode ser difícil seguir essas etapas genéricos sem se referir a uma classe de entidade específica, é fornecida um passo a passo que usa dados reais.

## <a name="add-validation-for-changes-to-the-value-in-a-specific-column"></a>Adicionar validação para alterações ao valor em uma coluna específica
 Este procedimento mostra como validar dados quando o valor em uma coluna é alterado. Porque a validação é executada dentro da definição de classe (em vez de na interface do usuário), uma exceção é lançada se o valor faz com que a validação falhar. Implementar manipulação de erro para o código em seu aplicativo que tenta alterar os valores de coluna.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-validate-data-during-a-columns-value-change"></a>Para validar dados durante o valor de uma coluna alterar

1.  Abra ou crie um novo arquivo LINQ to SQL Classes (**dbml** arquivo) na **Relational Designer**. (Clique duas vezes o **dbml** de arquivo no **Gerenciador de soluções**.)

2.  No **Relational Designer**, a classe para o qual você deseja adicionar validação e, em seguida, clique com o botão direito **Exibir código**.

     O editor de códigos abre com uma classe parcial para a classe de entidade selecionada.

3.  Coloque o cursor na classe parcial.

4.  Para projetos do Visual Basic:

    1.  Expanda o **nome do método** lista.

    2.  Localize o **OnCOLUMNNAMEChanging** método para a coluna que você deseja adicionar validação a.

    3.  Um `OnCOLUMNNAMEChanging` método é adicionado à classe parcial.

    4.  Adicione o seguinte código para primeiro verificar que um valor está inserido e para garantir em que o valor inserido para a coluna é aceitável para seu aplicativo. O argumento de `value` contém o valor proposto, para adicionar a lógica para confirmar que é um valor válido:

        ```vb
        If value.HasValue Then
            ' Add code to ensure that the value is acceptable.
            ' If value < 1 Then
            '    Throw New Exception("Invalid data!")
            ' End If
        End If
        ```

    Para projetos C#:

    Porque os projetos c# não gerenciar automaticamente manipuladores de eventos, você pode usar o IntelliSense para criar os métodos parciais de alteração de coluna. Tipo `partial` e um espaço para acessar a lista de métodos parciais disponíveis. Clique no método de alteração para a coluna que você deseja adicionar validação para. O seguinte código lembra o código que é gerado quando você seleciona um método parcial de alteração de coluna:

    ```csharp
    partial void OnCOLUMNNAMEChanging(COLUMNDATATYPE value)
        {
           throw new System.NotImplementedException();
        }
    ```

## <a name="add-validation-for-updates-to-an-entity-class"></a>Adicionar validação para atualizações a uma classe de entidade
 Além de verificar valores alterações pendentes, você também pode validar dados quando é feita uma tentativa de atualizar uma classe completa de entidade. A validação durante uma atualização tentada permite que você comparar valores em várias colunas se as regras comerciais exigem esta. O procedimento a seguir mostra como validar quando é feita uma tentativa de atualizar uma classe completa de entidade.

> [!NOTE]
>  O código de validação para que as atualizações terminem classes de entidade é executado na classe parcial de <xref:System.Data.Linq.DataContext> (em vez de na classe parcial de uma classe específica de entidade).

### <a name="to-validate-data-during-an-update-to-an-entity-class"></a>Para validar dados durante uma atualização para uma entidade

1.  Abra ou crie um novo arquivo LINQ to SQL Classes (**dbml** arquivo) na **Relational Designer**. (Clique duas vezes o **dbml** de arquivo no **Gerenciador de soluções**.)

2.  Com o botão direito em uma área vazia na **Relational Designer** e clique em **Exibir código**.

     O editor de códigos abre com uma classe parcial para `DataContext`.

3.  Coloque o cursor na classe parcial para `DataContext`.

4.  Para projetos do Visual Basic:

    1.  Expanda o **nome do método** lista.

    2.  Clique em **UpdateENTITYCLASSNAME**.

    3.  Um `UpdateENTITYCLASSNAME` método é adicionado à classe parcial.

    4.  Acessar valores de colunas individuais usando o argumento de `instance` , conforme mostrado no código o seguir:

        ```vb
        If (instance.COLUMNNAME = x) And (instance.COLUMNNAME = y) Then
            Dim ErrorMessage As String = "Invalid data!"
            Throw New Exception(ErrorMessage)
        End If
        ```

    Para projetos C#:

    Porque os projetos c# não gerenciar automaticamente manipuladores de eventos, você pode usar o IntelliSense para criar parcial `UpdateCLASSNAME` método. Tipo `partial` e um espaço para acessar a lista de métodos parciais disponíveis. Clique no método de atualização para a classe na qual você deseja adicionar validação. O seguinte código lembra o código que é gerado quando você seleciona um `UpdateCLASSNAME` método parcial:

    ```csharp
    partial void UpdateCLASSNAME(CLASSNAME instance)
    {
        if ((instance.COLUMNNAME == x) && (instance.COLUMNNAME = y))
        {
            string ErrorMessage = "Invalid data!";
            throw new System.Exception(ErrorMessage);
        }
    }
    ```

## <a name="see-also"></a>Consulte também

- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Validando dados](../data-tools/validate-data-in-datasets.md)
- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)