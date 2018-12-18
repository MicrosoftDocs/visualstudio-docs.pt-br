---
title: Registrar verbos para extensões de nome de arquivo | Microsoft Docs
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
- verbs, registering
ms.assetid: 81a58e40-7cd0-4ef4-a475-c4e1e84d6e06
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3a1300f7f66e9c3e9e9cebe3a7b0c7c84e7df4c2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782421"
---
# <a name="registering-verbs-for-file-name-extensions"></a>Registrando verbos para extensões de nome de arquivo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em geral, a associação de uma extensão de nome de arquivo com um aplicativo tem uma ação preferencial que ocorre quando um usuário clica duas vezes em um arquivo. Isso preferencial a ação é vinculada a um verbo, por exemplo aberto, que corresponde à ação.  
  
 Você pode registrar verbos que estão associados com um identificador programático (ProgID) para uma extensão usando a chave de Shell localizada em HKEY_CLASSES_ROOT\\*progid*\shell. Para obter mais informações, consulte [tipos de arquivo](http://msdn.microsoft.com/library/windows/desktop/cc144148\(v=vs.85\).aspx).  
  
## <a name="registering-standard-verbs"></a>Registrar verbos padrão  
 O sistema operacional reconhece os seguintes verbos padrão:  
  
- Abrir  
  
- Editar  
  
- Play  
  
- Imprimir  
  
- Visualizar  
  
  Sempre que possível, registre um verbo padrão. A opção mais comum é o verbo Open. Use o verbo de edição somente se houver uma diferença clara entre a abertura do arquivo e editando o arquivo. Por exemplo, abrir um arquivo. htm exibe no navegador, enquanto a edição de um arquivo. htm inicia um editor de HTML. Verbos padrão estão localizados com a localidade do sistema operacional.  
  
> [!NOTE]
>  Ao registrar verbos padrão, não defina o valor padrão para a chave de abertura. O valor padrão contém a cadeia de caracteres de exibição no menu. O sistema operacional fornece essa cadeia de caracteres para verbos padrão.  
  
 Arquivos de projeto devem ser registrados para iniciar uma nova instância da [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] quando um usuário abre o arquivo. O exemplo a seguir ilustra um registro de verbo padrão para um [!INCLUDE[csprcs](../includes/csprcs-md.md)] projeto.  
  
```  
[HKEY_CLASSES_ROOT\.csproj]  
@="VisualStudio.csproj.8.0"  
  
[HKEY_CLASSES_ROOT\.csproj\OpenWithList]  
[HKEY_CLASSES_ROOT\.csproj\OpenWithList\VSLauncher.exe]  
@=""  
  
[HKEY_CLASSES_ROOT\.csproj\OpenWithProgids]  
"VisualStudio.csproj.8.0"=""  
  
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe]  
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell]  
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open]  
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open\Command]  
@="C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe \"%1\""  
  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0]  
@="C# Project file"  
  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\DefaultIcon]  
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,0"  
  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell]  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open]  
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open\Command]  
@="\"C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe\" \"%1\""  
```  
  
 Para abrir um arquivo em uma instância existente do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], registre-se uma chave DDEEXEC. O exemplo a seguir ilustra um registro de verbo padrão para um [!INCLUDE[csprcs](../includes/csprcs-md.md)] arquivo. cs.  
  
```  
[HKEY_CLASSES_ROOT\.cs]  
@="VisualStudio.cs.8.0"  
  
[HKEY_CLASSES_ROOT\.cs\OpenWithList]  
[HKEY_CLASSES_ROOT\.cs\OpenWithList\devenv.exe]  
@=""  
  
[HKEY_CLASSES_ROOT\.cs\OpenWithProgids]  
"VisualStudio.cs.8.0"=""  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0]  
@="C# Source file"  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\DefaultIcon]  
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,1"  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell]  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open]  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\Command]  
@="\"C:\\VisualStudioPath\\Common7\\IDE\\devenv.exe\" /dde \"%1\""  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec]  
@="Open(\"%1\")"  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Application]  
@="VisualStudio.8.0"  
  
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Topic]  
@="system"  
```  
  
## <a name="setting-the-default-verb"></a>Definindo o verbo padrão  
 O verbo padrão é a ação que é executada quando um usuário clica duas vezes em um arquivo no Windows Explorer. O verbo padrão é o verbo especificado como o valor padrão para o HKEY_CLASSES_ROOT\\*progid*\Shell chave. Se nenhum valor for especificado, o verbo padrão é o primeiro verbo especificado no HKEY_CLASSES_ROOT\\*progid*\Shell lista de chaves.  
  
> [!NOTE]
>  Se você planejar alterar o verbo padrão para uma extensão em uma implantação lado a lado, considere o impacto sobre a instalação e remoção. Durante a instalação, o valor padrão original será substituído.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar associações de arquivo lado a lado](../extensibility/managing-side-by-side-file-associations.md)

