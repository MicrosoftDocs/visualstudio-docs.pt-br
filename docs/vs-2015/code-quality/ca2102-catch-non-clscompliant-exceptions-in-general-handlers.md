---
title: 'CA2102: capturar exceções não CLSCompliant em manipuladores gerais | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2102
- CatchNonClsCompliantExceptionsInGeneralHandlers
helpviewer_keywords:
- CA2102
ms.assetid: bf2df68f-d386-4379-ad9e-930a2c2e930d
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e2335b6d2bc3a5e99f0e6de1afefac4f42de0501
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521297"
---
# <a name="ca2102-catch-non-clscompliant-exceptions-in-general-handlers"></a>CA2102: Capturar exceções não CLSCompliant em manipuladores gerais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|CatchNonClsCompliantExceptionsInGeneralHandlers|
|CheckId|CA2102|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um membro em um assembly que não está marcado com o <xref:System.Runtime.CompilerServices.RuntimeCompatibilityAttribute> ou está marcado `RuntimeCompatibility(WrapNonExceptionThrows = false)` contém um bloco catch que manipula <xref:System.Exception?displayProperty=fullName> e não contém um bloco catch geral imediatamente após. Essa regra ignora [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] assemblies.

## <a name="rule-description"></a>Descrição da Regra
 Um bloco catch que trata de <xref:System.Exception> todas as exceções compatíveis com Common Language Specification (CLS). No entanto, ele não captura exceções não compatíveis com CLS. Exceções não compatíveis com CLS podem ser geradas de código nativo ou de código gerenciado que foi gerado pelo Microsoft Intermediate Language (MSIL) Assembler. Observe que o C# e os [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] compiladores não permitem que exceções não compatíveis com CLS sejam geradas e não [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] capturam exceções não compatíveis com CLS. Se a intenção do bloco catch é manipular todas as exceções, use a seguinte sintaxe de bloco catch geral.

- C#`catch {}`

- C++: `catch(...) {}` ou`catch(Object^) {}`

  Uma exceção não tratada em conformidade com CLS se torna um problema de segurança quando as permissões anteriormente permitidas são removidas no bloco catch. Como as exceções não compatíveis com CLS não são detectadas, um método mal-intencionado que gera uma exceção não compatível com CLS pode ser executado com permissões elevadas.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra quando a intenção é capturar todas as exceções, substitua ou adicione um bloco catch geral ou marque o assembly `RuntimeCompatibility(WrapNonExceptionThrows = true)` . Se as permissões forem removidas no bloco catch, duplique a funcionalidade no bloco catch geral. Se não for a intenção de lidar com todas as exceções, substitua o bloco catch que lida <xref:System.Exception> com blocos catch que lidam com tipos de exceção específicos.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o bloco try não contiver instruções que possam gerar uma exceção não compatível com CLS. Como qualquer código nativo ou gerenciado pode lançar uma exceção não compatível com CLS, isso requer conhecimento de todo o código que pode ser executado em todos os caminhos de código dentro do bloco try. Observe que as exceções não compatíveis com CLS não são lançadas pelo Common Language Runtime.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma classe MSIL que gera uma exceção não compatível com CLS.

```
.assembly ThrowNonClsCompliantException {}
.class public auto ansi beforefieldinit ThrowsExceptions
{
   .method public hidebysig static void
         ThrowNonClsException() cil managed
   {
      .maxstack  1
      IL_0000:  newobj     instance void [mscorlib]System.Object::.ctor()
      IL_0005:  throw
   }
}
```

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que contém um bloco catch geral que satisfaz a regra.

 [!code-csharp[FxCop.Security.CatchNonClsCompliantException#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.CatchNonClsCompliantException/cs/FxCop.Security.CatchNonClsCompliantException.cs#1)]

 Compile os exemplos anteriores da seguinte maneira.

```
ilasm /dll ThrowNonClsCompliantException.il
csc /r:ThrowNonClsCompliantException.dll CatchNonClsCompliantException.cs
```

## <a name="related-rules"></a>Regras relacionadas
 [CA1031: Não capturar tipos de exceção geral](../code-quality/ca1031-do-not-catch-general-exception-types.md)

## <a name="see-also"></a>Consulte Também
 [Exceções e tratamento de exceção](https://msdn.microsoft.com/library/0001887f-4fa2-47e2-8034-2819477e2344) [Ilasm.exe (Il assembler)](https://msdn.microsoft.com/library/4ca3a4f0-4400-47ce-8936-8e219961c76f) [substituindo](https://msdn.microsoft.com/4acdeff5-fc05-41bf-8505-7387cdbfca28) [a independência da linguagem de verificações de segurança e componentes independentes de linguagem](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
