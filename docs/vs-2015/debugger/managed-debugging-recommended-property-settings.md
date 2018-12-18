---
title: 'Depuração gerenciada: Configurações de propriedade recomendadas | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], managed
- debugging managed code, recommended property settings
ms.assetid: 3d14a8d4-2925-44d0-be41-ec546d411db9
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6c82a624e5a2847da5c0f85a9e2ef4180a338a34
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51724700"
---
# <a name="managed-debugging-recommended-property-settings"></a>Depuração gerenciada: configurações de propriedade recomendadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Certas propriedades devem ser definidas da mesma maneira para todos os cenários gerenciados de depuração.  
  
 As tabelas a seguir exibem as configurações de propriedade recomendadas.  
  
 As configurações não listadas aqui podem variar entre os diferentes tipos de projeto gerenciados. Por exemplo, **iniciar ação** será definido diferente em um projeto do Windows Forms que em um [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] projeto.  
  
### <a name="configuration-properties-on-the-build-c-or-compile-visual-basic-tab"></a>As propriedades de configuração na compilação (C#) ou na guia Compilar (Visual Basic)  
  
|**Nome da propriedade**|**Configuração**|  
|-----------------------|-----------------|  
|**Definir a constante DEBUG**|C# e F#: defina a caixa de seleção como verificado. Isso permite que o aplicativo use uma classe de Depuração.|  
|**Definir a constante TRACE**|C# e F#: defina a caixa de seleção como verificado. Isso permite que o aplicativo use uma classe de rastreamento.|  
|**Otimizar código**|F#, C# e Visual Basic: definidos como falso. O código otimizado é mais difícil de depurar porque as instruções geradas não correspondem diretamente ao código-fonte. Se você achar que seu programa tem um bug que aparece apenas em código otimizado, você pode ativar essa configuração, mas lembre-se de que o código mostrado na **desmontagem** janela é gerada de origem otimizada que pode não corresponder ao que você vê no código Editor. Para depurar o código otimizado, você deve desligar [Just My Code](just-my-code.md).<br /><br /> Para obter mais informações, consulte [configurações do projeto para configurações de depuração do c#](../debugger/project-settings-for-csharp-debug-configurations.md) ou [configurações do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md).|  
|**Caminho de saída**|Definido para bin\Debug\\.|  
|**Opções avançadas de compilação**|Somente Visual Basic. Clique em **avançado** para definir as propriedades avançadas descritas na tabela a seguir.|  
  
### <a name="advanced-compiler-settings-dialog-box"></a>Caixa de diálogo de Configurações Avançadas do Compilador  
  
|**Nome da propriedade**|**Configuração**|  
|-----------------------|-----------------|  
|**Habilitar otimizações**|Definida como false para as razões especificadas na **otimizar código** opção na tabela anterior.|  
|**Gerar informações de depuração**|Marque esta caixa de seleção para que o sinalizador /DEBUG seja definido ao compilar, o que vai gerar as informações necessárias para facilitar a depuração.|  
|**Definir a constante DEBUG**|Marque esta caixa de seleção para definir a constante de `DEBUG`, que permite que seu aplicativo use a classe <xref:System.Diagnostics.Debug>.|  
|**Definir a constante TRACE**|Marque esta caixa de seleção para definir a constante de `TRACE`, que permite que seu aplicativo use a classe <xref:System.Diagnostics.Trace>.|  
  
## <a name="see-also"></a>Consulte também  
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Tipos de projeto C#, F# e Visual Basic](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)



