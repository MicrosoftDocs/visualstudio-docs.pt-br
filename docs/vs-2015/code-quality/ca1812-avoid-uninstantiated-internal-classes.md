---
title: 'CA1812: Evite classes internas sem instâncias | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1812
- AvoidUninstantiatedInternalClasses
helpviewer_keywords:
- AvoidUninstantiatedInternalClasses
- CA1812
ms.assetid: 1bb92a42-322a-44cc-98a8-8858212c1e1f
caps.latest.revision: 28
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f44dcb010dd9c62d130913efd590a4c1b651de50
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60081990"
---
# <a name="ca1812-avoid-uninstantiated-internal-classes"></a>CA1812: Evitar classes internas sem instâncias
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidUninstantiatedInternalClasses|
|CheckId|CA1812|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Uma instância de um tipo no nível de assembly não é criada pelo código no assembly.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra tenta localizar uma chamada para um dos construtores de tipo e relata uma violação se nenhuma chamada for encontrada.

 Os seguintes tipos não são verificados por essa regra:

- Tipos de valor

- Tipos abstratos

- Enumerações

- Delegados

- Tipos de matriz emitidos pelo compilador

- Tipos que não pode ser instanciada e que definem `static` (`Shared` no Visual Basic) apenas métodos.

  Se você aplicar <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute?displayProperty=fullName> ao assembly que está sendo analisado, essa regra não ocorrerá nos construtores que são marcados como `internal` porque você não pode determinar se um campo está sendo usado por outro `friend` assembly.

  Mesmo que você não é possível contornar essa limitação em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] análise de código, o FxCop autônomo externo ocorrerá em construtores internos se cada `friend` assembly está presente na análise.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o tipo ou adicione o código que usa-o. Se o tipo contém apenas métodos estáticos, adicione o seguinte para o tipo para impedir que o compilador emite um construtor de instância pública padrão:

- Um construtor particular para tipos que se destinam [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] versões 1.0 e 1.1.

- O `static` (`Shared` no Visual Basic) modificador para tipos que se destinam [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)].

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra. É recomendável que você suprimir esse aviso nas seguintes situações:

- A classe é criada por meio de métodos de reflexão de associação tardia como <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>.

- A classe é criada automaticamente pelo tempo de execução ou [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Por exemplo, as classes que implementam <xref:System.Configuration.IConfigurationSectionHandler?displayProperty=fullName> ou <xref:System.Web.IHttpHandler?displayProperty=fullName>.

- A classe é passada como um parâmetro de tipo genérico que tem uma nova restrição. Por exemplo, o exemplo a seguir irá disparar essa regra.

  ```csharp
  internal class MyClass
  {
      public DoSomething()
      {
      }
  }
  public class MyGeneric<T> where T : new()
  {
      public T Create()
      {
          return new T();
      }
  }
  // [...]
  MyGeneric<MyClass> mc = new MyGeneric<MyClass>();
  mc.Create();
  ```

  Nessas situações, é recomendável que suprimir este aviso.

## <a name="related-rules"></a>Regras relacionadas
 [CA1811: Evitar código privado não chamado](../code-quality/ca1811-avoid-uncalled-private-code.md)

 [CA1801: Revisar parâmetros não utilizados](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804: Remover locais não usados](../code-quality/ca1804-remove-unused-locals.md)
