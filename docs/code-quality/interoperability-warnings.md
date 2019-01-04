---
title: Avisos de interoperabilidade
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- vs.codeanalysis.Interoperabilityrules
helpviewer_keywords:
- managed code analysis warnings, interoperability warnings
- interoperability warnings
- warnings, interoperability
ms.assetid: 95de6eb3-40c4-4063-9f59-25cb70e3b2b3
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b96131b2847b59632212c26bf5fa77fbe6b88960
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53956590"
---
# <a name="interoperability-warnings"></a>Avisos de interoperabilidade

Avisos de interoperabilidade dão suporte à interação com clientes COM.

## <a name="in-this-section"></a>Nesta seção

| Regra | Descrição |
| - | - |
| [CA1400: OS Pontos de entrada P/Invoke devem existir](../code-quality/ca1400-p-invoke-entry-points-should-exist.md) | Um método público ou protegido é marcado usando-se o atributo System.Runtime.InteropServices.DllImportAttribute. Não foi possível localizar a biblioteca não gerenciada ou não foi possível comparar o método a uma função na biblioteca. |
| [CA1401: P/Invokes não devem ser visíveis](../code-quality/ca1401-p-invokes-should-not-be-visible.md) | Um método público ou protegido em um tipo público tem o atributo DllImportAttribute (também implementado pela palavra-chave Declare em Visual Basic). Esses métodos não devem ser expostos. |
| [CA1402: Evitar sobrecargas em interfaces visíveis COM](../code-quality/ca1402-avoid-overloads-in-com-visible-interfaces.md) | Quando os métodos sobrecarregados são expostos a clientes COM, apenas a primeira sobrecarga do método mantém seu nome. As sobrecargas subsequentes são renomeadas com exclusividade acrescentando-se ao nome um caractere de sublinhado (_) e um inteiro correspondente à ordem de declaração da sobrecarga. |
| [CA1403: Tipos de layout automático não devem ser visíveis em COM](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md) | Um tipo de valor visível por COM é marcado usando-se o atributo System.Runtime.InteropServices.StructLayoutAttribute definido como LayoutKind.Auto. O layout desses tipos pode ser alterados entre versões do .NET Framework, o que interromperá clientes COM que esperam um layout específico. |
| [CA1404: Chamar GetLastError logo depois de P/Invoke](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md) | É feita uma chamada para o método Marshal.GetLastWin32Error ou o equivalente [!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)] função GetLastError e a chamada imediatamente anterior não é para uma plataforma de invocação de método. |
| [CA1405: Tipos de base de tipo visível COM devem ser visíveis em COM](../code-quality/ca1405-com-visible-type-base-types-should-be-com-visible.md) | Um tipo visível por COM deriva de um tipo que não é visível por COM. |
| [CA1406: Evitar argumentos Int64 para clientes Visual Basic 6](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md) | Os clientes COM do Visual Basic 6 não podem acessar inteiros de 64 bits. |
| [CA1407: Evitar membros estáticos em tipos visíveis COM](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md) | COM não dá suporte para métodos estáticos. |
| [CA1408: Não usar AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md) | Tipos que usam uma interface dupla permitem que clientes sejam associados a um layout de interface específico. Todas as alterações feitas em uma versão futura do layout do tipo ou de qualquer tipo de base interromperão clientes COM associados à interface. Por padrão, se o atributo ClassInterfaceAttribute não for especificado, será usada uma interface somente de expedição. |
| [CA1409: Tipos visíveis com devem ser criáveis](../code-quality/ca1409-com-visible-types-should-be-creatable.md) | Um tipo de referência marcado especificamente como visível para COM contém um construtor parametrizado público, mas não contém um construtor padrão público (sem parâmetros). Um tipo sem um construtor padrão público não pode ser criado por clientes COM. |
| [CA1410: OS métodos de registro devem ser correspondidos.](../code-quality/ca1410-com-registration-methods-should-be-matched.md) | Um tipo declara um método que é marcado usando o <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> de atributo, mas não declara um método que é marcado usando o <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> atributo, ou vice-versa. |
| [CA1411: OS métodos de registro não devem ser visíveis](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md) | Um método que é marcado usando ComRegisterFunctionAttribute ou o atributo System é visível externamente. |
| [CA1412: Marcar Interfaces ComSource como IDispatch](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md) | Um tipo é marcado usando-se o atributo System.Runtime.InteropServices.ComSourceInterfacesAttribute, e pelo menos uma das interfaces especificadas não está marcada usando-se o atributo System.Runtime.InteropServices.InterfaceTypeAttribute definido como ComInterfaceType.InterfaceIsIDispatch. |
| [CA1413: Evitar campos não públicos em tipos de valor visíveis COM](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md) | Os campos de instância não pública dos tipos de valor visíveis por COM permanecem visíveis para clientes COM. Revise o conteúdo dos campos em busca de informações que não devem ser expostas, ou isso terá efeitos não intencionais sobre o design ou a segurança. |
| [CA1414: Marcar argumentos P/Invoke boolianos com MarshalAs](../code-quality/ca1414-mark-boolean-p-invoke-arguments-with-marshalas.md) | O tipo de dados Booliano tem várias representações em código não gerenciado. |
| [CA1415: Declarar P/Invokes corretamente](../code-quality/ca1415-declare-p-invokes-correctly.md) | Esta regra procura declarações de método de invocação de plataforma que direcionam [!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)] parâmetro de estrutura de funções que têm um ponteiro para um OVERLAPPED e o parâmetro gerenciado correspondente não é um ponteiro para um <xref:System.Threading.NativeOverlapped?displayProperty=fullName> estrutura. |