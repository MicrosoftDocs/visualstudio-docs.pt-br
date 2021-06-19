---
title: Preparar para depurar Windows Forms aplicativos | Microsoft Docs
description: Tome as etapas de preparação para depurar Windows Forms aplicativos, que são criados pelo modelo Windows Forms projeto no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging Windows applications
- Windows applications, debugging
- debugging [Visual Studio], Windows applications
- debugging [C#], Windows applications
- debugging [Visual Basic], Windows applications
ms.assetid: 7092ee7f-8378-4def-aef8-1695bd97cf14
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c2181fe0b0189b0c0472f4d7cadd6a7c8e172a9b
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387738"
---
# <a name="debugging-preparation-windows-forms-applications"></a>Preparação da depuração: aplicativos dos Windows Forms

O Windows Forms do aplicativo cria um aplicativo Windows Forms aplicativo. Depurar esse tipo de aplicativo no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] é simples. Para obter informações sobre como criar um projeto desse tipo, consulte [Criar um aplicativo do Windows Form.](../ide/create-csharp-winform-visual-studio.md)

 Quando você cria um projeto do Windows Forms com o modelo de projeto, o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] cria automaticamente as configurações necessárias para as configurações de depuração e versão. Se necessário, você pode alterar essas configurações. Essas configurações podem ser alteradas na caixa **\<project name> de diálogo Páginas** de Propriedades ( Meu **Projeto** no Visual Basic).

 Para obter mais informações, consulte [Configurações de propriedade recomendadas.](../debugger/managed-debugging-recommended-property-settings.md)

 A tabela a seguir exibe uma configuração de propriedade recomendada adicional.

### <a name="configuration-properties-in-debug-tab"></a>Propriedades de configuração na guia Depurar

|**Nome da Propriedade**|**Configuração**|
|-----------------------|-----------------|
|**Iniciar Ação**|–   Definido como **Iniciar projeto,** na maioria das vezes. Definido como **Iniciar programa externo** se você quiser iniciar outro executável ao iniciar a depuração (geralmente para depuração de DLLs).|

 Você pode depurar aplicativos do Windows Forms de dentro do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ou anexando a um aplicativo já em execução. Para obter mais informações sobre a anexação, consulte [Anexar a processos em execução.](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)

### <a name="to-debug-a-c-f-or-visual-basic-windows-forms-application"></a>Para depurar um aplicativo C#, F# ou Windows Forms do Visual Basic

1. Abra o projeto no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].

2. Crie pontos de interrupção conforme o necessário.

    Como os aplicativos do Windows Forms são controlados por eventos, seus pontos de interrupção entrarão no código do manipulador de eventos ou nos métodos chamados pelo código do manipulador de eventos. Eventos comuns nos quais colocar pontos de interrupção incluem:

   1. Os eventos associados a um controle, como Clique, Insira etc.

   2. Os eventos associados à inicialização e o desligamento do aplicativo, como Carregar, Ativado etc.

   3. Foco e eventos de validação.

      Para obter mais informações, consulte [Criando manipuladores de eventos nos Windows Forms](/dotnet/framework/winforms/creating-event-handlers-in-windows-forms).

3. No menu **Depurar** , clique em **Iniciar**.

4. Depurar usando as técnicas discutidas [em Primeira olhada no depurador](../debugger/debugger-feature-tour.md).

## <a name="see-also"></a>Confira também
- [Depurando código gerenciado](../debugger/debugging-managed-code.md)
- [Tipos de projeto do Visual Basic, C# e F#](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [Como definir configurações de depuração e versão](../debugger/how-to-set-debug-and-release-configurations.md)
- [Configurações do projeto para configurações de depuração em C#](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Configurações do projeto para uma configuração Visual Basic de depuração](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [Anexar aos processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [Windows Forms](/dotnet/framework/winforms/index)