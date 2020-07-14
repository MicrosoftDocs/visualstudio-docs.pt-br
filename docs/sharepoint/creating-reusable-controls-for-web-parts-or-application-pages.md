---
title: Criando controles reutilizáveis para páginas Web Parts ou aplicativo | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- user controls [SharePoint development in Visual Studio], creating
- SharePoint development in Visual Studio, user controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b174e1e16802838f19cec6dce727ea3199df730f
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015138"
---
# <a name="create-reusable-controls-for-web-parts-or-application-pages"></a>Criar controles reutilizáveis para Web Parts ou páginas de aplicativo
  No Visual Studio, você pode criar controles personalizados e reutilizáveis que podem ser consumidos por páginas de aplicativo e Web Parts executados no SharePoint. Esses controles são chamados de controles de usuário. Um controle de usuário é um tipo de controle composto que funciona de forma muito parecida com uma página da Web ASP.NET – você pode adicionar controles de servidor Web e marcação existentes a um controle de usuário e definir propriedades e métodos para o controle. Em seguida, você pode incorporá-las em páginas da Web do ASP.NET, onde atuam como uma unidade.

## <a name="create-a-user-control"></a>Criar um controle de usuário
 Para criar um controle de usuário, adicione um **controle de usuário** a um **projeto do SharePoint vazio**. Para obter mais informações, consulte [como: criar um controle de usuário para uma página de aplicativo do SharePoint ou Web Part](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md).

 Quando você adiciona um item de **controle de usuário** , o Visual Studio cria uma pasta em seu projeto e, em seguida, adiciona vários arquivos à pasta. A tabela a seguir descreve cada arquivo.

|Arquivo|Descrição|
|----------|-----------------|
|Arquivo de controle de usuário|Define o controle de usuário. Projete o controle de usuário adicionando controles e marcação a esse arquivo.|
|Arquivo de código|Contém o código por trás do controle de usuário. Adicione código para manipular eventos a este arquivo.|
|Arquivo de código do designer|Contém o código gerado pelo designer e não deve ser editado diretamente.|

## <a name="design-the-user-control"></a>Criar o controle de usuário
 Projete o controle de usuário usando o designer do Visual Web Developer no Visual Studio. Esse designer aparece quando você abre o arquivo de controle de usuário em seu projeto e escolhe a guia **design** .

## <a name="consume-the-user-control"></a>Consumir o controle de usuário
 Os controles de usuário não aparecem no SharePoint até que você os inclua em uma página de aplicativo ou em uma Web Part.

 Para incluir um controle de usuário em uma página de aplicativo, abra a página da Web à qual você deseja adicionar o controle de usuário ASP.NET. Alterne para modo de exibição de Design, em seguida, selecione o arquivo de controle de usuário personalizado em Gerenciador de Soluções e arraste-o para a página. O controle de usuário ASP.NET é adicionado à página e o designer cria a diretiva @ Register, que é necessária para que a página reconheça o controle de usuário. Agora você pode trabalhar com as propriedades e os métodos públicos do controle.

 Para incluir um controle de usuário em uma Web Part, adicione o controle de usuário à coleção de Web Parts <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> no arquivo de código da Web Part. O exemplo a seguir adiciona um controle de usuário à <xref:System.Web.UI.WebControls.WebParts.Part.Controls%2A> coleção de uma Web Part.

 [!code-vb[SP_VisualWebPart#5](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1.vb#5)]
 [!code-csharp[SP_VisualWebPart#5](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1.cs#5)]

## <a name="debug-a-user-control"></a>Depurar um controle de usuário
 Para depurar um controle de usuário, verifique se o controle de usuário está incluído em uma página de aplicativo ou Web Part em seu projeto do SharePoint. Em seguida, você pode depurar o código no controle de usuário da mesma forma que você depuraria o código em qualquer projeto do Visual Studio.

 Quando você inicia o depurador do Visual Studio, o Visual Studio abre o site do SharePoint.

 No SharePoint, abra a página do aplicativo que inclui o controle de usuário. Se o controle de usuário estiver incluído em uma Web Part, adicione a Web Part a uma página de Web Part no SharePoint.

 Para obter mais informações sobre como depurar projetos do SharePoint, consulte [solução de problemas de soluções do SharePoint](../sharepoint/troubleshooting-sharepoint-solutions.md).

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[Como: criar um controle de usuário para uma página de aplicativo do SharePoint ou Web Part](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|Mostra como criar controles personalizados e reutilizáveis que podem ser consumidos por páginas de aplicativo e Web Parts executados no SharePoint.|
