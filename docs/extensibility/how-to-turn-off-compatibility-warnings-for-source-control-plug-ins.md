---
title: Desligar avisos para plug-ins de controle do código-fonte
description: Um usuário pode ver vários avisos de compatibilidade ao empregar o controle do código-fonte Visual Studio. Saiba como desabilitar esses avisos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- source control plug-ins, turning off compatibility warnings
- compatibility warnings, turning off
ms.assetid: ba318e12-921b-4b7a-a8c2-12c712be1dbf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ced04b09f8d4442cf0769ef503ee52772eccc0f6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905742"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>Como desativar avisos de compatibilidade para plug-ins de controle do código-fonte

Um usuário pode ver vários avisos de compatibilidade ao empregar o controle do código-fonte no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Os avisos apresentados dependem dos recursos do plug-in de controle do código-fonte e podem ser desabilitados conforme detalhado aqui.

### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>Para desabilitar o aviso: "Para garantir a integração ideal do controle do código-fonte com Visual Studio"

- De definir a seguinte entrada do Registro (adicionando o valor, se necessário):

   **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\DontDisplayCheckDotNETCompatible = dword:00000001**

   Esse aviso é exibido para todos os [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] plug-ins não.

### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>Para desabilitar o aviso: "O provedor de controle do código-fonte instalado não dá suporte a todos os recursos"

- De acordo com os dois valores do Registro a seguir (adicionando os valores, se necessário):

     **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\WarnedOldMSSCCIProvider = dword:00000000**

    **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\UseOldSCC = dword:00000001**

     Esse aviso será exibido se o plug-in de controle do código-fonte não dá suporte explicitamente à reentração para vários projetos (ou seja, se ele puder fazer check-in de apenas um arquivo e projeto por vez).

     É melhor dar suporte à reentração `SCC_CAP_REENTRANT` (funcionalidade); isso removerá esse aviso. No entanto, se esse suporte não for possível, essas entradas do Registro poderão ser definidas.

## <a name="see-also"></a>Confira também

- [Sinalizadores de funcionalidade](../extensibility/capability-flags.md)
