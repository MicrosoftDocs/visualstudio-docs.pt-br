---
title: Configurações de propriedade do depurador recomendadas para C#, VB | Microsoft Docs
description: Confira as configurações de propriedade de compilação e build que devem ser as mesmas para toda a depuração gerenciada. Outras configurações podem variar dependendo do tipo de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], managed
- debugging managed code, recommended property settings
ms.assetid: 3d14a8d4-2925-44d0-be41-ec546d411db9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: c2262194dbb6a8f4b0a47b4fcfc7f9f696c60167
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390392"
---
# <a name="managed-debugging-recommended-property-settings"></a>Depuração gerenciada: configurações de propriedade recomendadas
Certas propriedades devem ser definidas da mesma maneira para todos os cenários gerenciados de depuração.

 As tabelas a seguir exibem as configurações de propriedade recomendadas.

 As configurações não listadas aqui podem variar entre os diferentes tipos de projeto gerenciados. Por exemplo, **Iniciar Ação** será definido de maneira diferente em um projeto do Windows Forms do que em um projeto do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)].

### <a name="configuration-properties-on-the-build-c-or-compile-visual-basic-tab"></a>As propriedades de configuração na compilação (C#) ou na guia Compilar (Visual Basic)

|**Nome da Propriedade**|**Configuração**|
|-----------------------|-----------------|
|**Definir constante DEBUG**|C# e F#: defina a caixa de seleção como verificado. Isso permite que o aplicativo use uma classe de Depuração.|
|**Definir a constante TRACE**|C# e F#: defina a caixa de seleção como verificado. Isso permite que o aplicativo use uma classe de rastreamento.|
|**Otimizar código**|F#, C# e Visual Basic: definidos como falso. O código otimizado é mais difícil de depurar porque as instruções geradas não correspondem diretamente ao código-fonte. Se você descobrir que seu programa tem um bug que aparece apenas em código otimizado, habilite essa configuração, mas lembre-se de que o código exibido na janela **Desmontagem** será gerado da origem otimizada que pode não corresponder ao que aparece no Editor de Códigos. Para depurar um código otimizado, você deve desativar o Apenas Meu Código. (Confira [Restringir a depuração a Apenas Meu Código](../debugger/navigating-through-code-with-the-debugger.md#BKMK_Restrict_stepping_to_Just_My_Code)).<br /><br /> Para obter mais informações, consulte Configurações de projeto para configurações [de depuração](../debugger/project-settings-for-csharp-debug-configurations.md) em C# ou Configurações de projeto para uma [configuração Visual Basic de depuração.](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)|
|**Caminho de saída**|Definido para bin\Debug\\.|
|**Opções compiladas avançadas**|Somente Visual Basic. Clique em **Avançado** para definir as propriedades avançadas descritas na tabela a seguir.|

### <a name="advanced-compiler-settings-dialog-box"></a>Caixa de diálogo de Configurações Avançadas do Compilador

|**Nome da Propriedade**|**Configuração**|
|-----------------------|-----------------|
|**Habilitar otimizações**|Definido como false pelos motivos especificados na **opção Otimizar código** na tabela anterior.|
|**Gerar informações de depuração**|Marque esta caixa de seleção para que o sinalizador /DEBUG seja definido ao compilar, o que vai gerar as informações necessárias para facilitar a depuração.|
|**Definir constante DEBUG**|Marque esta caixa de seleção para definir a constante de `DEBUG`, que permite que seu aplicativo use a classe <xref:System.Diagnostics.Debug>.|
|**Definir a constante TRACE**|Marque esta caixa de seleção para definir a constante de `TRACE`, que permite que seu aplicativo use a classe <xref:System.Diagnostics.Trace>.|

## <a name="see-also"></a>Confira também
- [Depurando código gerenciado](../debugger/debugging-managed-code.md)
- [Tipos de projeto do Visual Basic, C# e F#](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)