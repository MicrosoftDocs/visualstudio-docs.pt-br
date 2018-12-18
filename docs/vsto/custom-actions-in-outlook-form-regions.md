---
title: Personalizar ações em regiões de formulário do Outlook
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], custom actions
- custom actions [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 4e2ad8e1c3b55d479cb031fe920e3027dbc1788c
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671060"
---
# <a name="custom-actions-in-outlook-form-regions"></a>Personalizar ações em regiões de formulário do Outlook
  Ações de exibem botões que permitem que os usuários respondam a um item do Microsoft Office Outlook. Por exemplo, para responder a um item de email, os usuários clicam a **resposta**, **responder a todos**, ou **Forward** botões de ação. Cada uma dessas ações cria um novo item de email e preenche os campos do item com o uso de informações do item original.  
  
 Você pode criar uma ação personalizada que é aberta a qualquer tipo de item do Outlook. Por exemplo, você pode adicionar uma ação personalizada que abre um novo item de compromisso ou tarefa. Definir as propriedades de uma ação personalizada ou usar código personalizado para preencher os campos do novo item. Ações personalizadas aparecem na **Custom Actions** lista suspensa de um item que está aberto em uma janela de Inspetor do Outlook.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="add-custom-actions-to-a-form-region"></a>Adicionar ações personalizadas para uma região de formulário  
 Para adicionar uma ação personalizada para uma região de formulário, use o **ações personalizadas** caixa de diálogo. Você pode abrir o **Custom Actions** da caixa de diálogo **Gerenciador de soluções** , expandindo o **manifesto** nó, selecionando o **CustomActions**propriedade e, em seguida, clicar no botão de reticências (![elipse designer móvel do ASP.NET](../sharepoint/media/mwellipsis.gif "elipse do Designer de dispositivo móvel do ASP.NET")).  
  
 Você pode usar o **Custom Actions** caixa de diálogo para especificar um *formulário de destino*. Um formulário de destino é o formulário que aparece quando o usuário executa a ação personalizada.  
  
 Você também pode usar o **Custom Actions** caixa de diálogo para especificar como deseja que as informações do item original seja exibido no formulário de destino.  
  
 A tabela a seguir descreve as propriedades que estão disponíveis na **Custom Actions** caixa de diálogo.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**AddressLike**|Especifica como o formulário de destino será resolvido.|  
|**Corpo**|Especifica como o corpo do item original é anexado ao formulário de destino.|  
|**Habilitado**|Indica se a ação personalizada está habilitada. Se essa propriedade é definida como **falsos**, a ação personalizada está desabilitada.|  
|**Método**|Especifica o tipo de resposta disponível quando a ação personalizada é executada. A ação personalizada pode enviar o formulário, abra o formulário ou solicitar que o usuário se deseja enviar ou abrir o formulário.|  
|**Nome**|Especifica o nome interno que você pode usar para fazer referência a essa ação personalizada no código.|  
|**ShowOnRibbon**|Indica se deve exibir a ação personalizada na faixa de opções do item original.|  
|**SubjectPrefix**|Especifica o texto que é inserido no início da linha de assunto do formulário de destino.|  
|**TargetForm**|Especifica o nome de classe de mensagem do formulário de destino. Por exemplo, digite **IPM. Tarefa** para abrir um formulário de tarefa.|  
|**Título**|Especifica o rótulo do botão de ação personalizada.|  
  
## <a name="customize-a-custom-action-at-runtime"></a>Personalizar uma ação personalizada em tempo de execução  
 Você também pode adicionar comportamento para a ação personalizada usando código. Por exemplo, você pode adicionar código que usa os nomes dos destinatários de email e adiciona os nomes como participantes em um novo item de compromisso. Para fazer isso, lidar com o [CustomAction](/office/vba/api/Outlook.MailItem.CustomAction) eventos da [objeto MailItem](/office/vba/api/Outlook.MailItem).  
  
## <a name="see-also"></a>Consulte também  
 [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)   
 [Passo a passo: Criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)   
 [Associar uma região de formulário uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md)  
  
  