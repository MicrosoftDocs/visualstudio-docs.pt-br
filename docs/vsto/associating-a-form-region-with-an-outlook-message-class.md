---
title: Associar uma região de formulário uma classe de mensagem do Outlook
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.InvalidMessageClassName
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FormRegionMessageClassAttribute
- form regions [Office development in Visual Studio], message classes
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: b9614a0feab70dd97cfd64861737c8b42dd146b7
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248027"
---
# <a name="associate-a-form-region-with-an-outlook-message-class"></a>Associar uma região de formulário uma classe de mensagem do Outlook
  Você pode especificar quais itens do Microsoft Office Outlook exibem uma região de formulário por meio da associação a região do formulário com a classe message de cada item. Por exemplo, se você deseja acrescentar uma região de formulário na parte inferior de um item de email, você pode associar a região do formulário com o `IPM.Note` classe de mensagem.  
  
 Para associar uma região de formulário uma classe de mensagem, especifique o nome de classe de mensagem na **nova região de formulário do Outlook** assistente ou aplicar um atributo à classe de fábrica de região do formulário.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
## <a name="understand-outlook-message-classes"></a>Entender as classes de mensagem do Outlook  
 Classe de mensagem do Outlook identifica um tipo de item do Outlook. A tabela a seguir lista essas oito tipos padrão de itens e seus nomes de classe de mensagem.  
  
|Tipo de Item do Outlook|Nome de classe de mensagem|  
|-----------------------|------------------------|  
|AppointmentItem|`IPM.Appointment`|  
|ContactItem|`IPM.Contact`|  
|ContactItem|`IPM.DistList`|  
|JournalItem|`IPM.Activity`|  
|MailItem|`IPM.Note`|  
|PostItem|`IPM.Post` ou `IPM.Post.RSS`|  
|TaskItem|`IPM.Task`|  
  
 Você também pode especificar os nomes das classes de mensagem personalizada. Classes de mensagem personalizada identificam formulários personalizados que você define no Outlook.  
  
> [!NOTE]  
>  Para conhecer as regiões de formulário Substituir tudo e substituição, você pode especificar um novo nome de classe de mensagem personalizada. Você não precisa usar o nome de classe de mensagem de um formulário personalizado existente. O nome da classe de mensagem personalizada deve ser exclusivo. Uma maneira de garantir que o nome seja exclusivo é usar uma convenção de nomenclatura semelhante ao seguinte: \<*StandardMessageClassName*>.\< *Empresa*>.\< *MessageClassName*> (por exemplo: `IPM.Note.Contoso.MyMessageClass`).  
  
## <a name="associate-a-form-region-with-an-outlook-message-class"></a>Associar uma região de formulário uma classe de mensagem do Outlook  
 Há duas maneiras de associar uma região de formulário uma classe de mensagem:  
  
-   Use o **nova região de formulário do Outlook** assistente.  
  
-   Aplica atributos de classe.  
  
### <a name="use-the-new-outlook-form-region-wizard"></a>Use o Assistente de nova região de formulário do Outlook  
 Na página final do **nova região de formulário do Outlook** assistente, você pode selecionar as classes de mensagem padrão e digite os nomes das classes de mensagem personalizada que você deseja associar à região do formulário.  
  
 As classes de mensagem padrão não estão disponíveis se a região do formulário foi projetada para substituir todo o formulário ou a página padrão de um formulário. Você pode especificar nomes de classe de mensagem padrão somente para formulários que adicionar uma nova página a um formulário ou que são acrescentados à parte inferior de um formulário. Confira mais informações em [Como: Adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md).  
  
 Para incluir uma ou mais classes de mensagem personalizada, digite os nomes na **quais classes de mensagem personalizadas exibirão esta região do formulário?** caixa.  
  
 Os nomes que você digitar devem estar de acordo com as diretrizes a seguir:  
  
- Use o nome de classe de mensagem totalmente qualificado (por exemplo: "IPM. Note.Contoso").  
  
- Use ponto e vírgula para separar vários nomes de classe de mensagem.  
  
- Não inclua classes de mensagem de Outlook padrão, como "IPM. Observação"ou"IPM. Entre em contato com". Incluir somente as classes de mensagem personalizada, como "IPM. Note.Contoso".  
  
- Não especifique a classe base mensagem por si só (por exemplo: "IPM").  
  
- Não exceda 256 caracteres para cada nome de classe de mensagem.  
  
  O **nova região de formulário do Outlook** assistente valida o formato da entrada quando você clica em **concluir**.  
  
> [!NOTE]  
>  O **nova região de formulário do Outlook** assistente não verifique se os nomes de classe de mensagem que você fornece estão corretos ou válido.  
  
 Quando você concluir o assistente, o **nova região de formulário do Outlook** assistente se aplica a atributos à classe de região do formulário que contém os nomes de classe de mensagem especificada. Você também pode aplicar esses atributos manualmente.  
  
### <a name="apply-class-attributes"></a>Aplicar atributos de classe  
 Você pode associar uma região de formulário com uma classe de mensagem do Outlook depois de concluir a **nova região de formulário do Outlook** assistente. Para fazer isso, aplica atributos para a classe de fábrica da região de formulário.  
  
 O exemplo a seguir mostra duas <xref:Microsoft.Office.Tools.Outlook.FormRegionMessageClassAttribute> atributos que foram aplicados a uma classe de fábrica da região de formulário chamada `myFormRegion`. O primeiro atributo associa a região do formulário uma classe de mensagem padrão para um formulário de mensagem de email. O segundo atributo associa a região do formulário uma classe de mensagem personalizada denominada `IPM.Task.Contoso`.  
  
 [!code-vb[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Attributes/FormRegion1.vb#1)]
 [!code-csharp[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Attributes/FormRegion1.cs#1)]  
  
 Atributos devem ser compatíveis com as diretrizes a seguir:  
  
- Para classes de mensagem personalizada, use o nome de classe de mensagem totalmente qualificado (por exemplo: "IPM. Note.Contoso").  
  
- Não especifique a classe base mensagem por si só (por exemplo: "IPM").  
  
- Não exceda 256 caracteres para cada nome de classe de mensagem.  
  
- Não inclua os nomes das classes de mensagem padrão se a região do formulário substitui todo o formulário ou a página padrão de um formulário. Você pode especificar nomes de classe de mensagem padrão somente para formulários que adicionar uma nova página a um formulário ou que são acrescentados à parte inferior de um formulário. Confira mais informações em [Como: Adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md).  
  
  Quando você compila o projeto, o Visual Studio valida o formato dos nomes de classe de mensagem.  
  
> [!NOTE]  
>  Visual Studio não verifique se os nomes de classe de mensagem que você fornece estão corretos ou válido.  
  
## <a name="see-also"></a>Consulte também  
 [Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)   
 [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)   
 [Passo a passo: Criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)   
 [Diretrizes para criar regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)   
 [Visão geral da classe de nome e a mensagem de formulário](/office/vba/outlook/Concepts/Forms/form-name-and-message-class-overview)   
 [Como os formulários do Outlook e itens funcionam juntos](/office/vba/outlook/Concepts/Forms/how-outlook-forms-and-items-work-together)  
  
  