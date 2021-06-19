---
title: Microsoft Visual Studio caixa de diálogo Depurador (Exceção Lançada) | Microsoft Docs
titleSuffix: ''
description: 'Saiba o que fazer quando ocorre uma exceção que seu programa precisa manipular. Você pode: 1) entrar no depurador; 2) continuar; ou 3) ignorar.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.exceptions.thrown
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Microsoft Visual Studio Debugger (Exception Thrown) dialog box
- exception handling, during debugging
- debugger, exceptions
- throwing exceptions, during debugging
ms.assetid: 1fe98d10-c8f9-4b39-a920-99169bfd542e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c7a4b92a3ec5c6876fae3054b692ff46f26e82cd
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387041"
---
# <a name="microsoft-visual-studio-debugger-exception-thrown-dialog-box"></a>Caixa de diálogo Depurador do Microsoft Visual Studio (exceção gerada)
Ocorreu uma exceção no seu programa. Esta caixa de diálogo relata o tipo de exceção lançada. Seu código precisa tratar essa exceção. Você pode escolher entre as seguintes opções para tratar a exceção:

 **Quebra** Permite que a execução entre no depurador. O manipulador de exceção não será invocado antes da interrupção. Se você continuar a partir da interrupção, o manipulador de exceção será invocado.

 **Continuar** Permite que a execução continue, dando ao manipulador de exceção a oportunidade de lidar com a exceção. Essa opção não está disponível para determinados tipos de exceções. **Continuar** permitirá que o aplicativo continue. Em um aplicativo nativo, ela fará com que a exceção seja relançada. Em um aplicativo gerenciado, ela fará com que o programa seja encerrado ou a exceção seja tratada por um aplicativo de hospedagem.

> [!NOTE]
> Você não pode continuar depois de uma exceção sem tratamento em código gerenciado. A escolha de **Continuar** depois de uma exceção sem tratamento no código gerenciado faz com que a depuração pare.

 **Ignorar** Permite que a execução continue sem invocar o manipulador de exceção. Como o manipulador de exceção não é invocado, isso poderá resultar em outras consequências, incluindo erros e exceções adicionais. Essa opção não está disponível para determinados tipos de exceções.

## <a name="see-also"></a>Confira também
- [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)
- [Práticas recomendadas para exceções](/dotnet/standard/exceptions/best-practices-for-exceptions)
- [Tratamento de exceções](/cpp/extensions/exception-handling-cpp-component-extensions)