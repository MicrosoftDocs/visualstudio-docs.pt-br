---
title: 'Erro: Falha em uma verificação de segurança porque o serviço de administração do IIS não respondeu | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: troubleshooting
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4f307e84f5267036e480ab1ec8118c32ee632bff
ms.sourcegitcommit: 0bf2aff6abe485e3fe940f5344a62a885ad7f44e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37058055"
---
# <a name="error-a-security-check-failed-because-the-iis-admin-service-did-not-respond"></a>Erro: falha na verificação de segurança porque o Serviço de Administração do IIS não respondeu
Esse erro ocorre quando o Serviço de administração do IIS não responde. Isso geralmente indica que há um problema com a instalação do IIS. Primeiro, verifique se o serviço está em execução usando o **Services** ferramenta de **ferramentas administrativas**.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Reinstale o IIS, usando o **adicionar ou remover programas** painel de controle.  
  
-   -ou-  
  
-   Remova o IIS do computador, usando o painel de controle Adicionar ou Remover Programas. Se você tiver removido o IIS e ainda tiver problemas, verifique no Registro se essa chave já não existe:  
  
    `HKEY_CLASSES_ROOT\CLSID\{A9E69610-B80D-11D0-B9B9-00A0C922E750}`  
  
     -ou-  
  
-   Desabilite o Serviço de administração do IIS, usando o painel de controle Ferramentas Administrativas. Isso desabilitará o IIS no computador.  
  
     Depois de executar qualquer uma dessas três etapas, reinicie o computador.  
  
     Para obter informações adicionais, consulte a documentação do IIS.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)