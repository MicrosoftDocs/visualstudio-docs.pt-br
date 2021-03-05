---
description: Esse erro ocorre quando o Serviço de administração do IIS não responde.
title: Uma verificação de segurança falhou porque o serviço de administração do IIS não respondeu | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.iis_not_responding
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 42c0a5a1a1fdb3a997f46a6933df9c8681fe0498
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147076"
---
# <a name="error-a-security-check-failed-because-the-iis-admin-service-did-not-respond"></a>Erro: falha na verificação de segurança porque o Serviço de Administração do IIS não respondeu
Esse erro ocorre quando o Serviço de administração do IIS não responde. Isso geralmente indica que há um problema com a instalação do IIS. Primeiro, verifique se o serviço está sendo executado usando a ferramenta **Serviços** de **Ferramentas Administrativas**.

### <a name="to-correct-this-error"></a>Para corrigir este erro

- Reinstale o IIS, usando o Painel de Controle **Adicionar ou Remover Programas**.

- -ou-

- Remova o IIS do computador, usando o painel de controle Adicionar ou Remover Programas. Se você tiver removido o IIS e ainda tiver problemas, verifique no Registro se essa chave já não existe:

    `HKEY_CLASSES_ROOT\CLSID\{A9E69610-B80D-11D0-B9B9-00A0C922E750}`

     -ou-

- Desabilite o Serviço de administração do IIS, usando o painel de controle Ferramentas Administrativas. Isso desabilitará o IIS no computador.

     Depois de executar qualquer uma dessas três etapas, reinicie o computador.

     Para obter informações adicionais, consulte a documentação do IIS.

## <a name="see-also"></a>Confira também
- [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
