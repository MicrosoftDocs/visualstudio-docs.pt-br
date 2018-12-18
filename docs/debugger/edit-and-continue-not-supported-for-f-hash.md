---
title: 'Editar e continuar não suportado para F # | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [F#]
- Debugging [F#], Edit and Continue
ms.assetid: 40ec77bb-07e3-4b58-9254-ae015009441c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4b945f92caa531e4de020f6cd07555b055aef287
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31473404"
---
# <a name="edit-and-continue-not-supported-for-f"></a>Editar e Continuar não suportado para F# #
A função Editar e Continuar não tem suporte quando você depura o código F#. As edições ao código F# são possíveis durante uma sessão de depuração mas devem ser evitadas. As alterações de código não são aplicadas durante a sessão de depuração. Como consequência, todas as edições feitas no código F# enquanto você depura resultarão no código-fonte que não corresponde ao código que está sendo depurado.
