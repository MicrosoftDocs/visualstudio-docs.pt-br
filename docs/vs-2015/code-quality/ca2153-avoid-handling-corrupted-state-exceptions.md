---
title: 'CA2153: Evitar o tratamento de exceções de estado corrompidas | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 418cc9cb-68ad-47e9-a6c8-a48b9c35db45
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 00e475fa90e0a9976105e4c9c645746427366f32
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49869945"
---
# <a name="ca2153-avoid-handling-corrupted-state-exceptions"></a>CA2153: evite manipular exceções de estado corrompido
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidHandlingCorruptedStateExceptions|
|CheckId|CA2153|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 [Corrompido exceções de estado (CSE)](https://msdn.microsoft.com/magazine/dd419661.aspx) indicam que a memória corrupção existe em seu processo. Capturar esses em vez de permitir que o processo falhe pode levar a vulnerabilidades de segurança se um invasor pode colocar uma exploração para a região de memória corrompida.

## <a name="rule-description"></a>Descrição da Regra
 CSE indica que o estado de um processo foi corrompido e não capturado pelo sistema. No cenário de estado corrompido, um manipulador geral só captura a exceção se você marcar o método com as devidas `HandleProcessCorruptedStateExceptions` atributo. Por padrão, o [Common Language Runtime (CLR)](https://msdn.microsoft.com/library/8bs2ecf4.aspx) não invoca manipuladores catch para CSEs.

 Permitindo que o processo falhe sem capturar esses tipos de exceções é a opção mais segura, como o mesmo código de registro pode permitir que os invasores podem explorar os bugs de corrupção de memória.

 Esse aviso dispara quando capturando CSEs com um manipulador geral que captura todas as exceções, como catch (Exception) ou catch (especificação de exceção).

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para resolver este aviso, você deve fazer o seguinte:

 1. Remover o `HandleProcessCorruptedStateExceptions` atributo. Isso será revertido para o comportamento de tempo de execução padrão no qual os CSEs não são passados para manipuladores catch.

 2. Remova o manipulador catch geral in preference of manipuladores que capturar tipos de exceção específica.  Isso pode incluir CSEs, supondo que o código do manipulador possa tratá-las com segurança (muito raro).

 3. Gera novamente a CSE no manipulador catch que garante que a exceção é passada para o chamador e resultarão no encerramento do processo em execução.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="pseudo-code-example"></a>Exemplo de pseudocódigo

### <a name="violation"></a>Violação
 O pseudocódigo a seguir ilustra o padrão detectado por essa regra.

```
[HandleProcessCorruptedStateExceptions]
//method to handle and log CSE exceptions
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle error
    }
}
```

### <a name="solution-1"></a>Solução 1
 Removendo o atributo HandleProcessCorruptedExceptions garante que as exceções não ocorrerão.

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (IOException e)
    {
        // Handle error
    }
    catch (UnauthorizedAccessException e)
    {
        // Handle error
    }
}
```

### <a name="solution-2"></a>Solução 2
 Remover o manipulador catch geral e capturar apenas os tipos de exceção específica.

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (IOException e)
    {
        // Handle error
    }
    catch (UnauthorizedAccessException e)
    {
        // Handle error
    }
}
```

### <a name="solution-3"></a>Solução 3
 Gera novamente a exceção.

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle error
        throw;
    }
}
```



