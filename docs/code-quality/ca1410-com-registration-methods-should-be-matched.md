---
title: 'CA1410: os métodos de registro COM devem ser correspondentes'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1410
- ComRegistrationMethodsShouldBeMatched
helpviewer_keywords:
- CA1410
- ComRegistrationMethodsShouldBeMatched
ms.assetid: f3b2e62d-fd66-4093-9f0c-dba01ad995fd
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 5d04668ef21ea469e1dbb42cea6c8a8b5b7f18f5
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47858394"
---
# <a name="ca1410-com-registration-methods-should-be-matched"></a>CA1410: os métodos de registro COM devem ser correspondentes

|||
|-|-|
|NomeDoTipo|ComRegistrationMethodsShouldBeMatched|
|CheckId|CA1410|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo declara um método que é marcado com o <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> de atributo, mas não declara um método que é marcado com o <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> atributo, ou vice-versa.

## <a name="rule-description"></a>Descrição da regra
 Para clientes do modelo de objeto de componente (COM) criar um tipo .NET Framework, o tipo deve ser registrado pela primeira vez. Se ele estiver disponível, um método que é marcado com o <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> atributo é chamado durante o processo de registro para executar o código especificado pelo usuário. Um método correspondente que é marcado com o <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> atributo é chamado durante o processo de cancelamento de registro para reverter as operações do método de registro.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, adicione o método de cancelamento de registro ou registro correspondente.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra. O código comentado mostra a correção para a violação.

 [!code-csharp[FxCop.Interoperability.ComRegistration#1](../code-quality/codesnippet/CSharp/ca1410-com-registration-methods-should-be-matched_1.cs)]
 [!code-vb[FxCop.Interoperability.ComRegistration#1](../code-quality/codesnippet/VisualBasic/ca1410-com-registration-methods-should-be-matched_1.vb)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1411: os métodos de registro COM não devem estar visíveis](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)

## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>
- [Registrando assemblies usando COM](/dotnet/framework/interop/registering-assemblies-with-com)
- [Regasm.exe (Ferramenta de Registro de Assembly)](/dotnet/framework/tools/regasm-exe-assembly-registration-tool)