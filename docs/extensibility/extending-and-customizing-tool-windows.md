---
title: Estendendo e personalizando a ferramenta Windows | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, essentials
- tool windows, standard
ms.assetid: 46b2892e-7b2b-4b3f-83a7-b884f1e114ee
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c11485e830d1b7bcef851a50225e15f351e64f3e
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39637478"
---
# <a name="extend-and-customize-tool-windows"></a>Estender e personalizar janelas de ferramentas
Visual Studio fornece vários tipos diferentes do windows, por exemplo, janelas de ferramentas, janelas de documentos e janelas de diálogo. Outras janelas, como o **propriedades** janela, o **saída** janela e o **lista de tarefas** janela, são tipos de janelas de ferramentas.  
  
## <a name="tool-windows"></a>Janelas de ferramentas  
 Janelas de ferramentas do Visual Studio são normalmente somente leitura windows que não são baseados em arquivo. Neste diferem das janelas de documento, quais arquivos são exibidos no modo de leitura / gravação. O **caixa de ferramentas**, **Gerenciador de soluções**, **propriedades** janela, e **navegador da Web** são exemplos de janelas de ferramentas.  
  
 Para saber como criar uma janela de ferramenta simples, consulte [adicionar uma janela de ferramentas](../extensibility/adding-a-tool-window.md).  
  
 Para registrar uma janela de ferramentas com o Visual Studio, consulte [registrar uma janela de ferramentas](../extensibility/registering-a-tool-window.md).  
  
 Janelas de ferramentas são a única instância por padrão, que significa que apenas uma instância da janela de ferramentas pode ser aberto por vez. Depois que uma janela de ferramentas de instância única é aberta, ele permanece aberto até que o IDE é fechada. Quando você fechar uma janela de ferramentas de instância única, apenas sua visibilidade é alterado. Você também pode criar várias instâncias janelas de ferramentas, de modo que várias instâncias da janela podem ser abertas simultaneamente. Ver [criar uma janela de ferramentas de várias instâncias](../extensibility/creating-a-multi-instance-tool-window.md) para obter mais informações.  
  
 Janelas de ferramenta podem ser *dinâmico*, que significa que eles estejam visíveis sempre que seu contexto de interface do usuário relacionado se aplica. O uso de visibilidade de automático pode reduzir a confusão de janelas no IDE. Para obter mais informações, consulte [abra uma janela de ferramenta dinâmica](../extensibility/opening-a-dynamic-tool-window.md).  
  
 Janelas de ferramenta podem ser encaixado, flutuante ou com guias no quadro de documento. O quadro de janela de ferramenta é fornecido pelo IDE e é usado para controlar o tamanho, local, estado de encaixe e outras propriedades persistentes. O painel da janela de ferramenta exibe o conteúdo. O tamanho e local padrão se aplicam somente quando a janela de ferramentas é aberta pela primeira vez; Depois que o estado da janela de ferramenta é mantido.  
  
 Painéis de janela de ferramenta podem hospedar controles de usuário do WPF e barras de ferramentas de suporte. Você pode substituir o <xref:Microsoft.VisualStudio.Shell.WindowPane.Window%2A> propriedade para retornar o identificador do controle hospedado.  
  
 Você pode adicionar muitos recursos diferentes para as janelas de ferramentas. Por exemplo, você pode adicionar uma barra de ferramentas: [adicionar uma barra de ferramentas para uma janela de ferramentas](../extensibility/adding-a-toolbar-to-a-tool-window.md) ou um menu de atalho: [adicionar um menu de atalho em uma janela de ferramenta](../extensibility/adding-a-shortcut-menu-in-a-tool-window.md). Você pode adicionar um controle de pesquisa que permite que você pesquise itens dentro de sua janela de ferramentas: [Adicionar pesquisa a uma janela de ferramenta](../extensibility/adding-search-to-a-tool-window.md).  
  
 Você pode assinar eventos de janela de ferramenta: [assinar um evento](../extensibility/subscribing-to-an-event.md).  
  
## <a name="extend-existing-tool-windows"></a>Estender as janelas de ferramentas existente  
 Você pode adicionar informações sobre sua janela de ferramentas para um novo **opções** página e uma nova configuração na **propriedades** página, escreva para o **lista de tarefas** e **saída**  windows. Para obter mais informações, consulte [estender as janelas de propriedades, lista de tarefas, saída e as opções](../extensibility/extending-the-properties-task-list-output-and-options-windows.md) e [estender as janelas de propriedades, lista de tarefas, saída e opções](../extensibility/extending-the-properties-task-list-output-and-options-windows.md).  
  
## <a name="modal-dialog-boxes"></a>Caixas de diálogo modais  
 Em uma extensão do Visual Studio, você deve criar caixas de diálogo modal, derivando-os da <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow?displayProperty=fullName>, que permite que você controle e o restante da interface do usuário. Para obter mais informações, consulte [criar e gerenciar caixas de diálogo modais](../extensibility/creating-and-managing-modal-dialog-boxes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md)