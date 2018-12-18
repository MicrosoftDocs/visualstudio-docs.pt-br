---
title: Preparar para depurar aplicativos do Windows Forms | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d441da0fd7a9342ef7b64f47374dc2ca61706db7
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53066412"
---
# <a name="debugging-preparation-windows-forms-applications"></a>Preparação de depuração: Aplicativos dos Windows Forms
O modelo de projeto do Windows Forms (.NET) cria um aplicativo do Windows Forms. Depurar esse tipo de aplicativo no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] é simples. Para obter mais informações, consulte [criando um projeto de aplicativo do Windows](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/42wc9kk5(v=vs.100)).  
  
 Quando você cria um projeto do Windows Forms com o modelo de projeto, o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] cria automaticamente as configurações necessárias para as configurações de depuração e versão. Se necessário, você pode alterar essas configurações. Essas configurações podem ser alteradas na caixa de diálogo **\<nome do projeto> Páginas de Propriedades** (**Meu Projeto** em Visual Basic).  
  
 Para obter mais informações, consulte [configurações de propriedade recomendadas](../debugger/managed-debugging-recommended-property-settings.md).  
  
 A tabela a seguir exibe uma configuração de propriedade recomendada adicional.  
  
### <a name="configuration-properties-in-debug-tab"></a>Propriedades de configuração na guia Depurar  
  
|**Nome da propriedade**|**Configuração**|  
|-----------------------|-----------------|  
|**Iniciar ação**|–   Definido como **Iniciar projeto,** na maioria das vezes. Definido como **Iniciar programa externo** se você quiser iniciar outro executável ao iniciar a depuração (geralmente para depuração de DLLs).|  
  
 Você pode depurar aplicativos do Windows Forms de dentro do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ou anexando a um aplicativo já em execução. Para obter mais informações sobre como anexar, consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
### <a name="to-debug-a-c-f-or-visual-basic-windows-forms-application"></a>Para depurar um aplicativo C#, F# ou Windows Forms do Visual Basic  
  
1. Abra o projeto no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
2. Crie pontos de interrupção conforme o necessário.  
  
    Como os aplicativos do Windows Forms são controlados por eventos, seus pontos de interrupção entrarão no código do manipulador de eventos ou nos métodos chamados pelo código do manipulador de eventos. Eventos comuns nos quais colocar pontos de interrupção incluem:  
  
   1. Os eventos associados a um controle, como Clique, Insira etc.  
  
   2. Os eventos associados à inicialização e o desligamento do aplicativo, como Carregar, Ativado etc.  
  
   3. Foco e eventos de validação.  
  
      Para obter mais informações, consulte [Criando manipuladores de eventos nos Windows Forms](/dotnet/framework/winforms/creating-event-handlers-in-windows-forms).  
  
3. No menu **Depurar**, clique em **Iniciar**.  
  
4. Depuração usando as técnicas discutidas [Noções básicas do depurador](../debugger/getting-started-with-the-debugger.md).  
  
## <a name="see-also"></a>Consulte também  
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Tipos de projeto do C#, F# e Visual Basic](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [Como: Definir as configurações de depuração e de versão](../debugger/how-to-set-debug-and-release-configurations.md)   
 [Configurações do projeto para configurações de depuração de C#](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Configurações do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [Anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [Windows Forms](/dotnet/framework/winforms/index)