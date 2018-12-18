---
title: -ResetSettings (devenv.exe) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Devenv, /ResetSettings switch
- ResetSettings switch
- /ResetSettings Devenv switch
ms.assetid: 1d41021c-6f58-4bd5-b122-d1c995812192
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 276205ae2aab3c38ceb3d4f1419e0bac13ae626c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49273488"
---
# <a name="resetsettings-devenvexe"></a>/ResetSettings (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Restaura [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] configurações padrão e inicia automaticamente o IDE do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Opcionalmente, redefine as configurações para o arquivo .vssettings especificado.  
  
 As configurações padrão são determinadas pelo perfil selecionado quando [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] foi inicializado pela primeira vez.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Devenv /ResetSettings SettingsFile  
```  
  
## <a name="arguments"></a>Arguments  
 `SettingsFile`  
 O caminho completo e o nome do arquivo .vssettings para aplicar a [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 Para restaurar o perfil de Configurações Gerais de Desenvolvimento, use `General`.  
  
## <a name="remarks"></a>Comentários  
 Se nenhum `SettingsFile` for especificado, será solicitado que você selecione uma coleção padrão de configurações na próxima vez iniciar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="example"></a>Exemplo  
 A seguinte linha de comando aplica as configurações armazenadas no arquivo `MySettings.vssettings`.  
  
```  
Devenv.exe /ResetSettings "C:\My Files\MySettings.vssettings"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)   
 [Opções de linha de comando devenv](../../ide/reference/devenv-command-line-switches.md)



