---
title: 'Como: criar uma Web Part do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2a8c02cce2f55374b4d62ba5663e8b3fe85b55b5
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016446"
---
# <a name="how-to-create-a-sharepoint-web-part"></a>Como: criar uma Web Part do SharePoint
  Você pode criar e personalizar uma Web Part adicionando um item de **Web Part** a qualquer projeto do SharePoint e, em seguida, editando o arquivo de código para a Web Part ou usando um designer. Para obter mais informações, consulte [como: criar uma Web Part do SharePoint usando um designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md).

### <a name="to-create-a-sharepoint-web-part"></a>Para criar uma Web Part do SharePoint

1. Crie ou abra um projeto do SharePoint.

     Para obter mais informações, consulte [projeto do SharePoint e modelos de item de projeto](../sharepoint/sharepoint-project-and-project-item-templates.md).

2. Escolha o nó do projeto do SharePoint em **Gerenciador de soluções** e, em seguida, escolha **projeto**  >  **Adicionar novo item**.

3. Na caixa de diálogo **Adicionar novo item** , expanda o nó **SharePoint** e escolha o nó **2010** .

4. Na lista de modelos do SharePoint, escolha **Web Part**.

5. Na caixa **nome** , especifique um nome para a Web Part e, em seguida, escolha o botão **Adicionar** .

     A Web Part aparece em **Gerenciador de soluções**. Para obter mais informações sobre os arquivos incluídos em uma Web Part, consulte [criar Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md).

6. No **Gerenciador de soluções**, abra o arquivo de código para a Web Part que você acabou de criar.

     Por exemplo, se o nome de sua Web Part for *WebPart1*, abra *WebPart1. vb* (em Visual Basic) ou *WebPart1.cs* (em C#).

7. No arquivo de código, adicione controles ao <xref:System.Web.UI.Control.CreateChildControls%2A> método.

     Para obter um exemplo, consulte [Walkthrough: criar uma Web Part para o SharePoint](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md).

## <a name="see-also"></a>Consulte também
- [Criar Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)
- [Como: criar uma Web Part do SharePoint usando um designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)
- [Walkthrough: criar uma Web Part para o SharePoint](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [Walkthrough: criar uma Web Part para o SharePoint usando um designer](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
