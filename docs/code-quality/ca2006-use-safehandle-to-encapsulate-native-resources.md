---
title: 'CA2006: Usar SafeHandle para encapsular recursos nativos'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2006
- UseSafeHandleToEncapsulateNativeResources
helpviewer_keywords:
- UseSafeHandleToEncapsulateNativeResources
- CA2006
ms.assetid: a71950bd-bcc1-463d-b1f2-5233bc451456
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 6d29eb9475d48e634766df65836162d6a79fed77
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808404"
---
# <a name="ca2006-use-safehandle-to-encapsulate-native-resources"></a>CA2006: Usar SafeHandle para encapsular recursos nativos

|||
|-|-|
|NomeDoTipo|UseSafeHandleToEncapsulateNativeResources|
|CheckId|CA2006|
|Categoria|Microsoft.Reliability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa

O código gerenciado usa <xref:System.IntPtr> para acessar recursos nativos.

## <a name="rule-description"></a>Descrição da regra

Uso de `IntPtr` em código gerenciado pode indicar um problema potencial de segurança e confiabilidade. Todos os usos da `IntPtr` devem ser examinados para determinar se o uso de um <xref:System.Runtime.InteropServices.SafeHandle> , ou uma tecnologia semelhante, é necessário em seu lugar. Problemas ocorrerão se o `IntPtr` representa algum recurso nativo, como memória, um identificador de arquivo ou um soquete, que o código gerenciado é considerado como o próprio. Se o código gerenciado tem o recurso, ele também deve liberar os recursos nativos associados a ela, porque uma falha ao fazer isso causaria perda de recursos.

Nesses cenários, problemas de segurança ou confiabilidade também existirá se o acesso com multithread é permitido para o `IntPtr` e uma maneira de liberar o recurso que é representado pelo `IntPtr` é fornecido. Esses problemas que envolvem a reciclagem do `IntPtr` valor na liberação de recursos enquanto o uso simultâneo do recurso está sendo feito em outro thread. Isso pode causar condições de corrida em que um thread pode ler ou gravar dados que está associados com o recurso incorreto. Por exemplo, se seu tipo armazena um identificador de sistema operacional como um `IntPtr` e permite que os usuários que ambos **fechar** e qualquer outro método que usa esse identificador ao mesmo tempo e sem algum tipo de sincronização, o código tem um reciclagem de identificador problema.

Esse problema de reciclagem de identificador pode causar corrupção de dados e, frequentemente, uma vulnerabilidade de segurança. `SafeHandle` e sua classe irmão <xref:System.Runtime.InteropServices.CriticalHandle> fornecem um mecanismo para encapsular um identificador nativo para um recurso, de modo que esses problemas de threading podem ser evitados. Além disso, você pode usar `SafeHandle` e sua classe irmão `CriticalHandle` para outros problemas de threading, por exemplo, para controlar o tempo de vida de objetos gerenciados que contêm uma cópia do identificador nativo em chamadas a métodos nativos com cuidado. Nessa situação, geralmente, você pode remover chamadas para `GC.KeepAlive`. A sobrecarga de desempenho que você incorra quando você usa `SafeHandle` e, em um grau menor, `CriticalHandle`, com frequência pode ser reduzido por meio de um design cuidadoso.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Converter `IntPtr` uso para `SafeHandle` para gerenciar com segurança o acesso aos recursos nativos. Consulte o <xref:System.Runtime.InteropServices.SafeHandle> artigo de referência para obter exemplos.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima esse aviso.

## <a name="see-also"></a>Consulte também

- <xref:System.IDisposable>