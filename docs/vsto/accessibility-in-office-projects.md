---
title: Acessibilidade em projetos do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, accessibility
- shortcut keys [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], shortcut keys
- accessibility [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9c39a68d13e2fd3d4932e169e713ed8534e0d266
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305124"
---
# <a name="accessibility-in-office-projects"></a>Acessibilidade em projetos do Office
  Microsoft Visual Studio e do Microsoft Office incluem muitos recursos de acessibilidade que permitem que você crie soluções personalizadas que atendem aos requisitos de acessibilidade padrão. A Microsoft publica as diretrizes de acessibilidade na Web. Para obter detalhes, consulte o [site de acessibilidade](http://go.microsoft.com/fwlink/?LinkID=37113).  

 Na maioria dos casos, os projetos do Office no Visual Studio atende aos padrões ou expõe as propriedades de acessibilidade que podem ser definidas para disponibilizar suas soluções. No entanto, há alguns recursos que têm a acessibilidade limitada.  

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  

## <a name="accessibility-at-design-time"></a>Acessibilidade no tempo de design  

### <a name="use-shortcut-keys-in-document-level-projects"></a>Use as teclas de atalho em projetos de nível de documento  
 Quando um documento do Microsoft Office Word ou uma pasta de trabalho do Microsoft Office Excel é aberta no Visual Studio, o aplicativo apenas uma por vez recebe os comandos de tecla de atalho. Por padrão, o Visual Studio recebe todos os comandos de tecla de atalho, mas você pode fazer o Word ou Excel recebê-las quando o documento tem o foco, selecionando **esquema de teclado dinâmico** sobre o **configurações de teclado** página dos **opções** caixa de diálogo. Para obter mais informações, consulte [teclado do Word do Microsoft Office, configurações de teclado do Microsoft Office, caixa de diálogo Opções](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md) e [teclado do Excel do Microsoft Office, configurações de teclado do Microsoft Office, a caixa de diálogo de opções](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md).  

### <a name="display-shortcut-keys-for-the-ribbon-in-document-level-projects"></a>Exibir as teclas de atalho para a faixa de opções no nível de documento  
 Quando um documento do Word ou uma pasta de trabalho do Excel é aberta no Visual Studio, você não pode pressionar o **Alt** tecla para exibir as teclas de atalho para as guias e controles da faixa de opções. Para exibir as teclas de atalho quando o documento ou pasta de trabalho é aberta no designer, execute as seguintes etapas.  

#### <a name="to-view-shortcut-keys-for-ribbon-tabs-and-controls-in-the-designer"></a>Para exibir as teclas de atalho para controles e guias da faixa de opções no designer  

1.  No Visual Studio, sobre o **ferramentas** menu, clique em **opções**.  

2.  Expanda o **ferramentas do Office** nó e selecione **teclado do Microsoft Office Excel** ou **teclado do Microsoft Office Word**, conforme apropriado.  

3.  Selecione **esquema de teclado dinâmico**.  

     Será exibida uma mensagem informando que você deve reiniciar o Visual Studio para que a alteração tenha efeito.  

4.  Clique em **OK**.  

5.  Reinicie o Visual Studio e, em seguida, reabra o projeto.  

6.  Abra o designer do documento ou pasta de trabalho para o seu projeto.  

7.  Pressione **F6** para exibir as teclas de atalho para a faixa de opções.  

## <a name="accessibility-at-runtime"></a>Acessibilidade no tempo de execução  

### <a name="windows-forms-controls-on-office-documents"></a>Controles de Windows Forms em documentos do Office  
 Controles dos Windows Forms expõem as propriedades de acessibilidade para fornecer informações sobre o controle para auxílios de acessibilidade, como leitores de tela. Quando os controles estão em um documento do Office em uma personalização no nível de documento, você pode tirar proveito dessas propriedades de acessibilidade. Para obter mais informações, consulte [fornecer informações de acessibilidade para controles em um formulário do Windows](/dotnet/framework/winforms/controls/providing-accessibility-information-for-controls-on-a-windows-form).  

 No entanto, existem algumas limitações de acessibilidade em tempo de execução quando controles dos Windows Forms são hospedados em uma pasta de trabalho do Excel ou um documento do Word:  

- Você não pode tabular de um controle para outro.  

- Controles em um documento são desabilitados quando você alterar a configuração de zoom do documento para algo diferente de 100%.  

  Para obter informações sobre as limitações de controles do Windows Forms em documentos, consulte [limitações dos Windows Forms a controles em documentos do Office](../vsto/limitations-of-windows-forms-controls-on-office-documents.md).  

### <a name="actions-panes-and-custom-task-panes"></a>Painéis de ações e painéis de tarefas personalizados  
 Quando um painel de ações ou o painel de tarefas personalizado tem o foco, acessar controles da mesma forma que você acessaria os controles em um aplicativo do Windows Forms. Para mover o cursor entre o painel de ações e o documento, você pode pressionar **F6**.  

 Para obter mais informações sobre painéis de ações e painéis de tarefas personalizados, consulte [visão geral do painel de ações](../vsto/actions-pane-overview.md) e [painéis de tarefas personalizados](../vsto/custom-task-panes.md).  

### <a name="display-modes"></a>Modos de exibição  
 Visual Studio tem as seguintes limitações relacionadas a modos de exibição:  

- Controles em um documento do Word ou planilha do Excel são desabilitados quando você alterar a configuração de zoom do documento para algo diferente de 100%.  

- O **novo projeto** caixa de diálogo Exibir controles corretamente se um usuário altera as opções de acessibilidade do computador para **usar alto contraste**.  

  Você pode usar a Lente de aumento para superar essas limitações. A Lupa é um utilitário de exibição no Windows que cria uma janela separada que exibe uma parte ampliada da tela.  

## <a name="see-also"></a>Consulte também  
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Acessibilidade para pessoas portadoras de deficiências](/visualstudio/ide/reference/accessibility-for-people-with-disabilities)   
 [Recursos de acessibilidade do Visual Studio](/visualstudio/ide/reference/accessibility-features-of-visual-studio)  
