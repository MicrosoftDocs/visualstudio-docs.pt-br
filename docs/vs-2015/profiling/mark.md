---
title: Marca | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1d72cef3-bb09-4bbb-8864-6ea0ab623ff9
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ff40ac5db35927fad0fe28fe3c86c5411b5f5255
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51769079"
---
# <a name="mark"></a>Marca
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A opção **Marca** do VSPerfCmd.exe insere as informações especificadas no arquivo de dados de criação de perfil. Marca pode ser listada em um relatório VSPerfReport separado ou na exibição de Relatório de marca da interface do usuário do criador de perfil. **Marca** pode ser usada para especificar os pontos inicial e final em relatórios e exibir filtros.  
  
 A opção **Marca** deve ser a única opção especificada na linha de comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe /Mark:MarkID,[MarkName]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `MarkID`  
 Um inteiro definido pelo usuário que está listado como a ID de marca em relatórios e exibições do criador de perfil. `MarkID` não precisa ser exclusivo.  
  
 `MarkName`  
 (Opcional) Uma cadeia de caracteres definida pelo usuário que está listada como o Nome da marca em relatórios e exibições do criador de perfil. Se `MarkName` não for especificado, o campo Nome da marca da listagem de marca estará vazio. Coloque as cadeias de caracteres que contêm espaços ou barras ("/") entre aspas.  
  
## <a name="example"></a>Exemplo  
 Este exemplo insere uma marca com uma ID de 123 e o nome da marca de "TestMark".  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe  
VSPerfCmd.exe /Mark:123,TestMark  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)



