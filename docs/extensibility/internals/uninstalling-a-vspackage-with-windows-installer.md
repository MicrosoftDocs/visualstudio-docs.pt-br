---
title: Desinstalar um VSPackage com o Windows Installer | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- packages, uninstalling
- VSPackages, uninstalling
- uninstalling VSPackages
ms.assetid: c4575ac7-82da-4af8-a375-ea756a101fbf
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c619cdeffccb6e5da37eaaf15e5542fe78c44f79
ms.sourcegitcommit: 9765b3fcf89375ca499afd9fc42cf4645b66a8a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46495304"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>Desinstalando um VSPackage com o Windows Installer
Na maior parte, o Windows Installer pode desinstalar o VSPackage apenas por "Desfazer" o que fazia para instalar o VSPackage. As ações personalizadas discutidos [comandos que deve ser executado após a instalação](../../extensibility/internals/commands-that-must-be-run-after-installation.md) deve ser executado após a desinstalação também. Como as chamadas para devenv.exe ocorrerem logo antes da ação padrão de InstallFinalize para instalação e desinstalação, as entradas da tabela CustomAction e InstallExecuteSequence atender a ambos os casos.  
  
> [!NOTE]
>  Executar `devenv /setup` depois de desinstalar um pacote MSI.  
  
 Como regra geral, se você adicionar ações personalizadas a um pacote do Windows Installer, você deve tratar essas ações durante a reversão e desinstalação. Se você adicionar ações personalizadas para se registrar o VSPackage, por exemplo, você deve adicionar ações personalizadas para cancelar o registro, muito.  
  
> [!NOTE]
>  É possível que um usuário instalar o VSPackage e, em seguida, desinstalar as versões do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] com o qual ele está integrado. Você pode ajudar a garantir que a desinstalação do VSPackage funciona nesse cenário, eliminando as ações personalizadas que executam código com dependências no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
## <a name="handling-launch-conditions-at-uninstall-time"></a>Manipulação de condições de inicialização no momento da desinstalação  
 A ação padrão de LaunchConditions lê as linhas da tabela para mostrar o erro LaunchCondition mensagens se as condições não forem atendidas. Conforme as condições de inicialização geralmente são usadas para garantir que os requisitos de sistema são atendidos, você geralmente pode ignorar condições de inicialização durante a desinstalação, adicionando a condição, `NOT Installed`, à linha da tabela LaunchCondition LaunchConditions.  
  
 Uma alternativa é adicionar `OR Installed` para iniciar as condições que não são importantes durante a desinstalação. Isso garante que a condição sempre será true durante a desinstalação e, portanto, não exibirá a mensagem de erro de condição de inicialização.  
  
> [!NOTE]
>  `Installed` é a propriedade que instalador do Windows define quando ele detecta que o VSPackage já foi instalado no sistema.  
  
## <a name="see-also"></a>Consulte também  
 [Windows Installer](https://msdn.microsoft.com/library/187d8965-c79d-4ecb-8689-10930fa8b3b5)   
 [Detectar os requisitos do sistema](../../extensibility/internals/detecting-system-requirements.md)