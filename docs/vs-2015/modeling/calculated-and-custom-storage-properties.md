---
title: Propriedades de armazenamento calculadas e personalizadas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, programming domain properties
ms.assetid: 42b785f9-2b0f-4f13-a6b4-246e5e0d477a
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 82d90d6965558ba6d28753fb71b3b227a84467a6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49852850"
---
# <a name="calculated-and-custom-storage-properties"></a>Propriedades calculadas e de armazenamento personalizado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Todas as propriedades de domínio em uma linguagem específica de domínio (DSL) podem ser exibidas para o usuário no diagrama e no Gerenciador de linguagem e podem ser acessadas pelo código do programa. No entanto, as propriedades são diferentes da maneira que seus valores são armazenados.  
  
## <a name="kinds-of-domain-properties"></a>Tipos de propriedades de domínio  
 Na definição de DSL, você pode definir as **tipo** de uma propriedade de domínio, conforme listado na tabela a seguir:  
  
|Tipo de propriedade de domínio|Descrição|  
|--------------------------|-----------------|  
|**Padrão** (padrão)|Uma propriedade de domínio que é salvo na *armazenar* e serializados para o arquivo.|  
|**Calculado**|Uma propriedade de domínio somente leitura que não é salvo no repositório, mas é calculada a partir de outros valores.<br /><br /> Por exemplo, `Person.Age` poderia ser calculado a partir `Person.BirthDate`.<br /><br /> Você precisa fornecer o código que executa o cálculo. Normalmente, você pode calcular o valor de outras propriedades de domínio. No entanto, você também pode usar recursos externos.|  
|**Armazenamento personalizado**|Uma propriedade de domínio que não é salvo diretamente no repositório, mas pode ser get e set.<br /><br /> Você precisa fornecer os métodos que obtém e definir o valor.<br /><br /> Por exemplo, `Person.FullAddress` pode ser armazenado no `Person.StreetAddress`, `Person.City`, e `Person.PostalCode`.<br /><br /> Você também pode acessar recursos externos, por exemplo, para obter e definir valores de um banco de dados.<br /><br /> Seu código não deve definir valores no repositório quando `Store.InUndoRedoOrRollback` é verdadeiro. Ver [transações e Setters personalizados](#setters).|  
  
## <a name="providing-the-code-for-a-calculated-or-custom-storage-property"></a>Fornecendo o código para uma propriedade de armazenamento calculado ou personalizado  
 Se você definir o tipo de uma propriedade de domínio como Calculated ou armazenamento personalizado, você precisa fornecer métodos de acesso. Quando você compila sua solução, um relatório de erros dirá o que é necessário.  
  
#### <a name="to-define-a-calculated-or-custom-storage-property"></a>Para definir uma calculado ou uma propriedade de armazenamento personalizado  
  
1.  Em Dsldefinition, selecione a propriedade de domínio no diagrama ou no **Gerenciador de DSL**.  
  
2.  No **propriedades** janela, defina as **tipo** campo **calculado** ou **armazenamento personalizado**.  
  
     Certifique-se de que você também tiver definido sua **tipo** que você deseja.  
  
3.  Clique em **transformar todos os modelos** na barra de ferramentas da **Gerenciador de soluções**.  
  
4.  No menu **Compilar**, clique em **Compilar Solução**.  
  
     A seguinte mensagem de erro: "*YourClass* não contém uma definição para Get*YourProperty*."  
  
5.  Clique duas vezes a mensagem de erro.  
  
     Dsl\generatedcode\domainclasses.cs. ou DomainRelationships.cs é aberto. Acima de chamada do método realçada, um comentário solicitará que você forneça uma implementação para Get*YourProperty*().  
  
    > [!NOTE]
    >  Esse arquivo é gerado de Dsldefinition. Se você editar esse arquivo, suas alterações serão perdidas na próxima vez que você clicar em **transformar todos os modelos**. Em vez disso, adicione o método necessário em um arquivo separado.  
  
6.  Criar ou abrir um arquivo de classe em uma pasta separada, por exemplo CustomCode\\*YourDomainClass*. cs.  
  
     Certifique-se de que o namespace é o mesmo do código gerado.  
  
7.  No arquivo de classe, escreva uma implementação parcial da classe de domínio. Na classe, escreva uma definição para o ausente `Get` método semelhante ao exemplo a seguir:  
  
    ```  
    namespace Company.FamilyTree  
    {  public partial class Person  
       {  int GetAgeValue()  
          { return System.DateTime.Today.Year - this.BirthYear; }  
    }  }  
    ```  
  
8.  Se você definir **tipo** à **armazenamento personalizado**, você também terá que fornecer um `Set` método. Por exemplo:  
  
    ```  
    void SetAgeValue(int value)  
    { if (!Store.InUndoRedoOrRollback)  
        this.BirthYear =   
            System.DateTime.Today.Year - value; }  
    ```  
  
     Seu código não deve definir valores no repositório quando `Store.InUndoRedoOrRollback` é verdadeiro. Ver [transações e Setters personalizados](#setters).  
  
9. Criar e executar a solução.  
  
10. A propriedade de teste. Certifique-se de que você tente **desfazer** e **Refazer**.  
  
##  <a name="setters"></a> Transações e Setters personalizados  
 No método conjunto de propriedade de armazenamento personalizado, você não precisa abrir uma transação, porque o método geralmente é chamado dentro de uma transação ativa.  
  
 No entanto, o método de conjunto também pode ser chamado se o usuário invoca desfazer ou refazer, ou se uma transação está sendo revertida. Quando <xref:Microsoft.VisualStudio.Modeling.Store.InUndoRedoOrRollback%2A> for true, seu método Set deve se comportar da seguinte maneira:  
  
- Ele não deve fazer alterações no repositório, como atribuindo valores a outras propriedades de domínio. O Gerenciador de desfazer definirá seus valores.  
  
- No entanto, ele deve atualizar todos os recursos externos, como objetos fora do repositório de banco de dados ou conteúdo do arquivo. Isso irá assegurar que elas são mantidas em synchronism com os valores no repositório.  
  
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
  
 Para obter mais informações sobre transações, consulte [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).  
  
## <a name="see-also"></a>Consulte também  
 [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)   
 [Propriedades das propriedades de domínio](../modeling/properties-of-domain-properties.md)   
 [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)



