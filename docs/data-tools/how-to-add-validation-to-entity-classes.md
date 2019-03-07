---
title: Como adicionar validação a classes de entidade
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 61107da9-7fa3-4dba-b101-ae46536f52c4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 5f4f2f5e44ea95137f53019f52de94a5389fa6d8
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55913490"
---
# <a name="how-to-add-validation-to-entity-classes"></a>Como adicionar validação a classes de entidade
*Validar* classes de entidade é o processo que confirma que os valores inseridos em objetos de dados estão de acordo com as restrições do esquema de um objeto e também as regras estabelecidas para o aplicativo. Validar dados antes de enviar atualizações para o base de dados subjacente é uma boa prática que reduz erros. Também reduz o número potencial de processamentos entre um aplicativo e o base de dados.

 O [LINQ to SQL das ferramentas no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md) fornece os métodos parciais que permitem aos usuários estender o código gerado pelo designer que é executado durante inserções, atualizações e exclusões de entidades completos e também durante e após a coluna individual alterações.

> [!NOTE]
>  Este tópico fornece as etapas básicas para adicionar validação a classes de entidade usando o **Relational Designer**. Porque ele pode ser difícil seguir essas etapas genéricos sem se referir a uma classe de entidade específica, é fornecida um passo a passo que usa dados reais.

## <a name="add-validation-for-changes-to-the-value-in-a-specific-column"></a>Adicionar validação para alterações ao valor em uma coluna específica
 Este procedimento mostra como validar dados quando o valor em uma coluna é alterado. Uma vez que a validação é executada na definição de classe (em vez de na interface do usuário), será lançada uma exceção se o valor causar a falha da validação. Implementar manipulação de erro para o código em seu aplicativo que tenta alterar os valores de coluna.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-validate-data-during-a-columns-value-change"></a>Para validar dados durante o valor de uma coluna alterar

1.  Abra ou crie um novo arquivo LINQ to SQL Classes (**dbml** arquivo) na **Relational Designer**. (Clique duas vezes no arquivo **.dbml** em **Gerenciador de Soluções**.)

2.  No **Designer Relacional de Objetos**, clique com o botão direito do mouse na classe para qual você deseja adicionar validação e clique em **Exibir Código**.

     O editor de códigos abre com uma classe parcial para a classe de entidade selecionada.

3.  Coloque o cursor na classe parcial.

4.  Para projetos do Visual Basic:

    1.  Expanda a lista **Nome do Método**.

    2.  Localize o **OnCOLUMNNAMEChanging** método para a coluna que você deseja adicionar validação a.

    3.  Um método `OnCOLUMNNAMEChanging` é adicionado à classe parcial.

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

1.  Abra ou crie um novo arquivo LINQ to SQL Classes (**dbml** arquivo) na **Relational Designer**. (Clique duas vezes no arquivo **.dbml** em **Gerenciador de Soluções**.)

2.  Clique com o botão direito do mouse em uma área vazia no **Designer Relacional de Objetos** e clique em **Exibir Código**.

     O editor de códigos abre com uma classe parcial para `DataContext`.

3.  Coloque o cursor na classe parcial para `DataContext`.

4.  Para projetos do Visual Basic:

    1.  Expanda a lista **Nome do Método**.

    2.  Clique em **UpdateENTITYCLASSNAME**.

    3.  Um método `UpdateENTITYCLASSNAME` é adicionado à classe parcial.

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

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Validando dados](../data-tools/validate-data-in-datasets.md)
- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)