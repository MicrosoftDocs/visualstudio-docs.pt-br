---
title: 'CA1024: usar propriedades quando apropriado | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UsePropertiesWhereAppropriate
- CA1024
helpviewer_keywords:
- CA1024
- UsePropertiesWhereAppropriate
ms.assetid: 3a04f765-af7c-4872-87ad-9cc29e8e657f
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a240a6eea86075bbf7f721f8620b6d135d594c20
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546660"
---
# <a name="ca1024-use-properties-where-appropriate"></a>CA1024: Usar propriedades quando apropriado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|UsePropertiesWhereAppropriate|
|CheckId|CA1024|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método público ou protegido tem um nome que começa com `Get` , não usa parâmetros e retorna um valor que não é uma matriz.

## <a name="rule-description"></a>Descrição da Regra
 Na maioria dos casos, as propriedades representam dados e métodos executam ações. As propriedades são acessadas como campos, o que as torna mais fáceis de usar. Um método é um bom candidato a se tornar uma propriedade se uma dessas condições estiver presente:

- Não usa argumentos e retorna as informações de estado de um objeto.

- Aceita um único argumento para definir alguma parte do estado de um objeto.

  As propriedades devem se comportar como se fossem campos; Se o método não puder, ele não deverá ser alterado para uma propriedade. Os métodos são melhores do que as propriedades nas seguintes situações:

- O método executa uma operação demorada. O método é muito mais lento do que o tempo necessário para definir ou obter o valor de um campo.

- O método executa uma conversão. O acesso a um campo não retorna uma versão convertida dos dados que ele armazena.

- O método Get tem um efeito colateral observável. A recuperação do valor de um campo não produz nenhum efeito colateral.

- A ordem de execução é importante. Definir o valor de um campo não depende da ocorrência de outras operações.

- Chamar o método duas vezes em sucessão cria resultados diferentes.

- O método é estático, mas retorna um objeto que pode ser alterado pelo chamador. A recuperação do valor de um campo não permite que o chamador altere os dados armazenados pelo campo.

- O método retorna uma matriz.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o método para uma propriedade.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso dessa regra se o método atender a pelo menos um dos critérios listados anteriormente.

## <a name="controlling-property-expansion-in-the-debugger"></a>Controlando a expansão da propriedade no depurador
 Um motivo pelo qual os programadores evitam o uso de uma propriedade é porque não querem que o depurador a expanda automaticamente. Por exemplo, a propriedade pode envolver a alocação de um objeto grande ou a chamada de P/Invoke, mas pode não ter realmente nenhum efeito colateral observável.

 Você pode impedir que o depurador expanda automaticamente as propriedades aplicando <xref:System.Diagnostics.DebuggerBrowsableAttribute?displayProperty=fullName> . O exemplo a seguir mostra esse atributo sendo aplicado a uma propriedade de instância.

```vb
Imports System
Imports System.Diagnostics

Namespace Microsoft.Samples

    Public Class TestClass

        ' [...]

        <DebuggerBrowsable(DebuggerBrowsableState.Never)> _
        Public ReadOnly Property LargeObject() As LargeObject
            Get
                ' Allocate large object
                ' [...]
            End Get
        End Property

    End Class

End Namespace
```

```csharp

      using System;
using System.Diagnostics;

namespace Microsoft.Samples
{
    publicclass TestClass
    {
        // [...]

        [DebuggerBrowsable(DebuggerBrowsableState.Never)]
        public LargeObject LargeObject
        {
            get
            {
                // Allocate large object
                // [...]

        }
    }
}
```

## <a name="example"></a>Exemplo
 O exemplo a seguir contém vários métodos que devem ser convertidos em Propriedades e vários que não deveriam porque eles não se comportam como campos.

 [!code-csharp[FxCop.Design.MethodsProperties#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.MethodsProperties/cs/FxCop.Design.MethodsProperties.cs#1)]
