---
title: Escolha a caixa de diálogo de operação (herdado) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Workflow.Activities.Design.OperationPickerDialog.UI
ms.assetid: bc3ec902-7797-494e-af48-e70c97eb6779
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 75b553bd79936db7b6d8aa2f8fe361650d4ef03e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49189613"
---
# <a name="choose-operation-dialog-box-legacy"></a>Escolha a caixa de diálogo da operação (o legados)
Este tópico descreve como usar o **escolher operação** caixa de diálogo em novas [!INCLUDE[wfd1](../includes/wfd1-md.md)]. Use [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado quando você precisa definir como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 O **escolher operação** caixa de diálogo é usada para selecionar uma operação para associar um <xref:System.Workflow.Activities.ReceiveActivity> atividade ou um <xref:System.Workflow.Activities.SendActivity> atividade. Para obter mais informações sobre como usar essa caixa de diálogo com essas atividades, consulte [como: implementar uma operação de contrato do Windows (legados)](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md) e [como: chamar uma operação de contrato do WCF (herdado)](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md).  
  
 A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **escolher operação** caixa de diálogo.  
  
|Elemento da Interface do Usuário|Descrição|  
|----------------|-----------------|  
|**Adicionar contrato**|Cria um novo contrato para você. Você pode definir novos operações no contrato. (Isso é usado com <xref:System.Workflow.Activities.ReceiveActivity> somente.)|  
|**Adicionar operação**|Adicionar novos operações para um novo contrato que você criou na **escolher operação** caixa de diálogo. **Observação:** você pode adicionar novos operações somente a contratos que você criou por meio de **escolher operação** caixa de diálogo. <br /><br /> (Isso é usado com <xref:System.Workflow.Activities.ReceiveActivity> somente.)|  
|**Importe...**|Importa um contrato definido anteriormente e permite que você selecione uma operação do contrato.|  
|**Nome da operação**|Nome da operação selecionada. Essa caixa de texto está disponível para edição somente se você tiver criado uma operação por meio de **escolher operação** caixa de diálogo.|  
|**Parâmetros**|Catalogue para conter as definições de parâmetro para a operação selecionada. **Observação:** definições de parâmetro podem ser alteradas somente se você tiver criado uma operação por meio de **escolher operação** caixa de diálogo.|  
|**Propriedades**|Catalogue para conter configurações de <xref:System.Net.Security.ProtectionLevel> para as mensagens enviadas entre o cliente e o serviço. **Observação:** esta guia estará habilitada apenas se você tiver criado uma operação por meio de **escolher operação** caixa de diálogo.|  
|**Permissões**|Catalogue para conter propriedades de <xref:System.Workflow.Activities.OperationInfoBase.PrincipalPermissionName%2A> e de <xref:System.Workflow.Activities.OperationInfoBase.PrincipalPermissionRole%2A> de usuários são permitidos que chamar a operação. Por exemplo, se apenas os usuários do grupo Administradores foram permissão para chamar a operação, em seguida, você escreveria "Administradores" **função** caixa de texto.<br /><br /> Essa guia está habilitado para ambas as operações criadas por meio de **ChooseOperation** caixa de diálogo e operações que foram importados por meio do **importação** botão.|  
  
> [!NOTE]
>  O **escolher operação** caixa de diálogo mostra somente contratos ou operações que são usadas por outras <xref:System.Workflow.Activities.SendActivity> atividades no fluxo de trabalho. Da mesma forma, o **escolher operação** caixa de diálogo <xref:System.Workflow.Activities.ReceiveActivity> mostra as atividades somente contratos ou operações que são usadas por outras **ReceiveActivity** atividades no fluxo de trabalho.  
  
## <a name="see-also"></a>Consulte também  
 [Como: implementar uma operação de contrato do Windows (legados)](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md)   
 [Como: chamar uma operação de contrato do WCF (legados)](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md)   
 [Designer herdado para a ajuda da interface do usuário do Windows Workflow Foundation](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)