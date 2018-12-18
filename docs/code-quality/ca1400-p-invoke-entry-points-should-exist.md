---
title: 'CA1400: os pontos de entrada de P-Invoke devem existir'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1400
- PInvokeEntryPointsShouldExist
helpviewer_keywords:
- PInvokeEntryPointsShouldExist
- CA1400
ms.assetid: 1d64e470-7b2f-4cca-8fb0-ac92829e6332
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 950983bd8c953a9a29c7d2f0ca216975d6c0f142
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839252"
---
# <a name="ca1400-pinvoke-entry-points-should-exist"></a>CA1400: os pontos de entrada P/Invoke devem existir

|||
|-|-|
|NomeDoTipo|PInvokeEntryPointsShouldExist|
|CheckId|CA1400|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um método público ou protegido é marcado com o <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>. Não foi possível localizar a biblioteca não gerenciada ou não foi possível comparar o método a uma função na biblioteca. Se a regra não é possível localizar o nome do método exatamente como ele é especificado, ele procura por ANSI ou versões de caractere largo do método acrescentando o nome do método com 'A' ou 'W'. Se nenhuma correspondência for encontrada, a regra tenta localizar uma função usando o formato de nome de stdcall (_MyMethod@12, onde 12 representa o comprimento dos argumentos). Se nenhuma correspondência for encontrada e o nome do método começa com '#', a regra de pesquisa para a função como uma referência ordinal, em vez de uma referência de nome.

## <a name="rule-description"></a>Descrição da regra
 Nenhuma verificação de tempo de compilação está disponível para certificar-se de que os métodos são marcados com <xref:System.Runtime.InteropServices.DllImportAttribute> estão localizados na DLL não gerenciada referenciada. Se nenhuma função que tem o nome especificado está na biblioteca, ou os argumentos para o método não coincidem com os argumentos da função, o common language runtime lançará uma exceção.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, corrija o método que tem o <xref:System.Runtime.InteropServices.DllImportAttribute> atributo. Certifique-se de que a biblioteca não gerenciada existe e está no mesmo diretório que o assembly que contém o método. Se a biblioteca estiver presente e referenciado corretamente, verifique se o nome do método, o tipo de retorno e a assinatura de argumento correspondem a função de biblioteca.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra quando a biblioteca não gerenciada está no mesmo diretório que o assembly gerenciado que faz referência a ele. Talvez seja seguro suprimir um aviso nessa regra no caso em que a biblioteca não gerenciada não pôde ser localizada.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra. Nenhuma função chamada `DoSomethingUnmanaged` ocorre em kernel32.dll.

 [!code-csharp[FxCop.Interoperability.DLLExists#1](../code-quality/codesnippet/CSharp/ca1400-p-invoke-entry-points-should-exist_1.cs)]

## <a name="see-also"></a>Consulte também
 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>