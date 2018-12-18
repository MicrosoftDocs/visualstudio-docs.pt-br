---
title: Usado em cadeias de substituição. Pkgdef e. Arquivos de Pkgundef | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio shell, isolated mode%2C .pkgdef and .pkgundef files
ms.assetid: b1755d63-d794-4fd7-864b-70a9684881c2
caps.latest.revision: 5
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1496931b02c5673c1f08253ebed7da0cae0b904c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817536"
---
# <a name="substitution-strings-used-in-pkgdef-and-pkgundef-files"></a>Usado em cadeias de substituição. Pkgdef e. Arquivos Pkgundef
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar as cadeias de caracteres de substituição listadas abaixo na. pkgdef e isolado de arquivos. pkgundef definir para o Visual Studio o aplicativo de shell.  
  
## <a name="substitution-strings"></a>Cadeias de caracteres de substituição  
  
|Cadeia de Caracteres|Descrição|  
|------------|-----------------|  
|$=*RegistryEntry*$|O valor de *RegistryEntry* entrada. Se a cadeia de caracteres de entrada de registro terminar em uma barra invertida (\\), em seguida, o valor padrão da subchave do registro é usado. Por exemplo, a substituição de cadeia de caracteres $= HKEY_CURRENT_USER\Environment\TEMP$ é expandido para a pasta temporária do usuário atual.|  
|$ $AppName|O nome qualificado do aplicativo que é passado para os pontos de entrada AppEnv.dll. O nome qualificado consiste no nome do aplicativo, um sublinhado e o identificador de classe (CLSID) do objeto de automação application, que também é registrado como o valor da configuração no arquivo. pkgdef projeto ThisVersionDTECLSID.|  
|$AppDataLocalFolder|Na subpasta em % LOCALAPPDATA % para este aplicativo.|  
|$ $BaseInstallDir|O caminho completo do local em que o Visual Studio foi instalado.|  
|$ $CommonFiles|O valor da variável de ambiente % CommonProgramFiles %.|  
|$ $MyDocuments|O caminho completo da pasta Meus documentos do usuário atual.|  
|$ $PackageFolder|O caminho completo do diretório que contém os arquivos de assembly do pacote para o aplicativo.|  
|$ $ProgramFiles|O valor da variável de ambiente % ProgramFiles %.|  
|$ $RootFolder|O caminho completo do diretório raiz do aplicativo.|  
|$ $RootKey|A chave do registro raiz para o aplicativo. Por padrão, a raiz é no HKEY_CURRENT_USER\Software\\*CompanyName*\\*ProjectName*\\*VersionNumber* (quando o aplicativo está em execução, _Config é acrescentado a esta chave). Ele é definido pelo valor RegistryRoot na *SolutionName*arquivo. pkgdef.<br /><br /> A cadeia de caracteres de $ $RootKey pode ser usada para recuperar um valor do registro na subchave do aplicativo. Por exemplo, a cadeia de caracteres "$= $RootKey$ \AppIcon$" retornará o valor da entrada AppIcon sob a subchave de raiz do aplicativo.<br /><br /> O analisador processa o arquivo. pkgdef sequencialmente e pode acessar uma entrada de registro na subchave do aplicativo somente se a entrada tiver sido definida anteriormente|  
|$ $ShellFolder|O caminho completo do local em que o Visual Studio foi instalado.|  
|$ $System|A pasta Windows\system32.|  
|$ $WINDIR|A pasta Windows.|  
  
 Se o analisador não reconhece a cadeia de caracteres de substituição ou não é possível determinar o valor de uma entrada de registro ou uma variável de ambiente, em seguida, ele não executa substituição essa parte da cadeia de caracteres.

