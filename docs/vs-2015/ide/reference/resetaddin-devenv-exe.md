---
title: -ResetAddin (devenv.exe) | Microsoft Docs
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
- disable addin
- addin state
- reset addin
ms.assetid: 9e339c8d-d768-4d86-8f45-2f479fc8255b
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f1b53a30845ca4b20372fb5a6e3552f31f3c1b60
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49950518"
---
# <a name="resetaddin-devenvexe"></a>/ResetAddin (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Remove comandos e comando da interface do usuário associado ao Suplemento especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Devenv /ResetAddin AddIn  
```  
  
## <a name="arguments"></a>Arguments  
 `AddIn`  
 Opcional. O nome de comando do Suplemento.  
  
## <a name="remarks"></a>Comentários  
 Por padrão, o nome do comando do suplemento é igual a *\<AddInSolutionName>*.Connect<em>.\<AddInSolutionName></em> e aparece no Connect.cs como o parâmetro `commandName` do método `Exec`. Você também pode verificar o nome do comando começando a digitar o nome do suplemento na janela Comandos no Visual Studio e usando o IntelliSense para preencher o restante.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir inicia o Visual Studio e impede o suplemento `MyAddin` de ser executado na inicialização.  
  
```  
Devenv.exe /ResetAddin MyAddin.Connect.MyAddin  
```  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)   
 [Opções de linha de comando devenv](../../ide/reference/devenv-command-line-switches.md)



