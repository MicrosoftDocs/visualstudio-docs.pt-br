---
title: Propriedades calculadas e de armazenamento personalizado
description: Saiba como todas as propriedades de domínio em uma DSL (linguagem específica de domínio) podem ser exibidas para o usuário no diagrama e no seu explorador de idiomas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain properties
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f98dca6759b9e4a77e71139b6d9ec9b394d99b04
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385416"
---
# <a name="calculated-and-custom-storage-properties"></a>Propriedades calculadas e de armazenamento personalizado
Todas as propriedades de domínio em uma DSL (linguagem específica de domínio) podem ser exibidas para o usuário no diagrama e no seu explorador de idiomas e podem ser acessadas pelo código do programa. No entanto, as propriedades diferem na maneira como seus valores são armazenados.

## <a name="kinds-of-domain-properties"></a>Tipos de propriedades de domínio
 Na Definição de DSL, você pode definir o **Tipo** de uma propriedade de domínio, conforme listado na tabela a seguir:

|Tipo de propriedade de domínio|Descrição|
|-|-|
|**Padrão** (Padrão)|Uma propriedade de domínio que é salva no *armazenamento e* serializada no arquivo.|
|**Calculadas**|Uma propriedade de domínio somente leitura que não é salva no armazenamento, mas é calculada com base em outros valores.<br /><br /> Por exemplo, `Person.Age` pode ser calculado de `Person.BirthDate` .<br /><br /> Você precisa fornecer o código que executa o cálculo. Normalmente, você calcula o valor de outras propriedades de domínio. No entanto, você também pode usar recursos externos.|
|**Armazenamento personalizado**|Uma propriedade de domínio que não é salva diretamente no armazenamento, mas pode ser get e set.<br /><br /> Você precisa fornecer os métodos que obter e definir o valor.<br /><br /> Por exemplo, `Person.FullAddress` pode ser armazenado em , e `Person.StreetAddress` `Person.City` `Person.PostalCode` .<br /><br /> Você também pode acessar recursos externos, por exemplo, para obter e definir valores de um banco de dados.<br /><br /> Seu código não deve definir valores no armazenamento quando `Store.InUndoRedoOrRollback` for true. Consulte [Transações e Setters Personalizados.](#setters)|

## <a name="providing-the-code-for-a-calculated-or-custom-storage-property"></a>Fornecendo o código para uma propriedade de armazenamento calculada ou personalizada
 Se você definir o Tipo de uma propriedade de domínio como Armazenamento Calculado ou Personalizado, será necessário fornecer métodos de acesso. Quando você criar sua solução, um relatório de erros informará o que é necessário.

#### <a name="to-define-a-calculated-or-custom-storage-property"></a>Para definir uma propriedade de armazenamento calculada ou personalizada

1. Em DslDefinition.dsl, selecione a propriedade de domínio no diagrama ou no **DSL Explorer.**

2. Na janela **Propriedades,** de definir o **campo Tipo** como **Armazenamento Calculado** **ou Personalizado.**

     Certifique-se de que você também definiu **seu Tipo** como o que você deseja.

3. Clique **em Transformar Todos os** Modelos na barra de ferramentas do **Gerenciador de Soluções**.

4. No menu **Compilar**, clique em **Compilar Solução**.

     Você recebe a seguinte mensagem de erro:*"YourClass* não contém uma definição para Get *YourProperty."*

5. Clique duas vezes na mensagem de erro.

     Dsl\GeneratedCode\DomainClasses.cs ou DomainRelationships.cs é aberto. Acima da chamada de método realçada, um comentário solicita que você forneça uma implementação para Get *YourProperty*().

    > [!NOTE]
    > Esse arquivo é gerado de DslDefinition.dsl. Se você editar esse arquivo, suas alterações serão perdidas na próxima vez que você clicar em **Transformar Todos os Modelos**. Em vez disso, adicione o método necessário em um arquivo separado.

6. Crie ou abra um arquivo de classe em uma pasta separada, por exemplo CustomCode \\ *YourDomainClass*.cs.

     Certifique-se de que o namespace seja o mesmo que no código gerado.

7. No arquivo de classe, escreva uma implementação parcial da classe de domínio. Na classe , escreva uma definição para o método `Get` ausente que se assemelha ao exemplo a seguir:

    ```
    namespace Company.FamilyTree
    {  public partial class Person
       {  int GetAgeValue()
          { return System.DateTime.Today.Year - this.BirthYear; }
    }  }
    ```

8. Se você definir **Tipo** como **Armazenamento Personalizado,** também será preciso fornecer um `Set` método . Por exemplo:

    ```
    void SetAgeValue(int value)
    { if (!Store.InUndoRedoOrRollback)
        this.BirthYear =
            System.DateTime.Today.Year - value; }
    ```

     Seu código não deve definir valores no armazenamento quando `Store.InUndoRedoOrRollback` for true. Consulte [Transações e Setters Personalizados.](#setters)

9. Compile e execute a solução.

10. Teste a propriedade . Certifique-se de tentar **Desfazer** **e Refazer.**

## <a name="transactions-and-custom-setters"></a><a name="setters"></a> Transações e setters personalizados
 No método Set da propriedade Armazenamento Personalizado, você não precisa abrir uma transação, pois o método geralmente é chamado dentro de uma transação ativa.

 No entanto, o método Set também poderá ser chamado se o usuário invocar Desfazer ou Refazer ou se uma transação estiver sendo relembolsada. Quando <xref:Microsoft.VisualStudio.Modeling.Store.InUndoRedoOrRollback%2A> for true, o método Set deverá se comportar da seguinte maneira:

- Ele não deve fazer alterações no armazenamento, como atribuir valores a outras propriedades de domínio. O gerenciador de desfazer definirá seus valores.

- No entanto, ele deve atualizar quaisquer recursos externos, como conteúdo de banco de dados ou arquivo ou objetos fora do armazenamento. Isso garantirá que eles sejam mantidos em sincronia com os valores no armazenamento.

  Por exemplo:

```
void SetAgeValue(int value)
{
  // If we are in Undo, no changes to Store objects:
  if (!this.Store.InUndoRedoOrRollback)
  {
    this.BirthYear = System.DateTime.Today.Year - value;
  }
  // But always update external objects:
  System.IO.File.WriteAllText(AgeFile, value);
}
```

 Para obter mais informações sobre transações, consulte Navegando e [atualizando um modelo no código do programa.](../modeling/navigating-and-updating-a-model-in-program-code.md)

## <a name="see-also"></a>Confira também

- [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Propriedades das propriedades de domínio](../modeling/properties-of-domain-properties.md)
- [Como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md)
