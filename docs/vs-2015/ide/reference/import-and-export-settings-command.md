---
title: Comando Import and Export Settings | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Tools.ImportandExportSettings
helpviewer_keywords:
- Tools.ImportandExportSettings
- Import and Export Settings command
ms.assetid: 94a06468-a44d-403d-a931-77bbc9d06e56
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 2556b814059a80f2b93d0220de27cdbd8c051ea9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49305559"
---
# <a name="import-and-export-settings-command"></a>Comando Importar e Exportar Configurações
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Importa, exporta ou redefine configurações [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Tools.ImportandExportSettings [/export:filename | /import:filename | /reset]  
```  
  
## <a name="switches"></a>Opções  
 /export:`filename`  
 Opcional. Exporta as configurações atuais para o arquivo especificado.  
  
 /import:`filename`  
 Opcional. Importa as configurações no arquivo especificado.  
  
 /reset  
 Opcional. Redefine as configurações atuais.  
  
## <a name="remarks"></a>Comentários  
 Executar esse comando sem nenhuma opção abre o assistente **Importar e Exportar Configurações**. Para obter mais informações, consulte [Como: Compartilhar configurações entre computadores ou versões de Visual Studio](http://msdn.microsoft.com/en-us/1131fb10-35c1-42da-9cd8-91aa3235b882).  
  
## <a name="example"></a>Exemplo  
 O comando a seguir exporta as configurações atuais para o arquivo `MyFile.vssettings`.  
  
```  
Tools.ImportandExportSettings /export:"c:\Files\MyFile.vssettings"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)   
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)



