---
title: 'Como: localizar marcação ASPX | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- localizing XML [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 68e74f743c1c00bb940a89039e4fd5cfcf8e63e4
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118385"
---
# <a name="how-to-localize-aspx-markup"></a>Como: localizar marcação ASPX
  [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] páginas (. aspx) normalmente usam valores de cadeia de caracteres embutida. Para localizar essas cadeias de caracteres, substitua-os com expressões que fazem referência a recursos localizados.  
  
## <a name="localize-aspx-markup"></a>Localizar marcação ASPX  
  
#### <a name="to-localize-aspx-markup"></a>Ao localizar marcação ASPX  
  
1.  Adicionar arquivos de recurso separados: um para o idioma padrão e um para cada idioma de localizado.  
  
     Se você estiver localizando apenas a marcação e não no código, adicione um item de projeto do arquivo de recursos globais. Se você estiver localizando o código e marcação, adicione um item de projeto do arquivo de recursos.  
  
    1.  Para adicionar um arquivo de recursos globais **Gerenciador de soluções**, abra o menu de atalho para um item de projeto do SharePoint e, em seguida, escolha **Add** > **Novo Item**. Sob o SharePoint **2010** nó, escolher o **arquivo de recursos globais** modelo.  
  
    2.  Para adicionar um arquivo de recursos, na **Gerenciador de soluções**, abra o menu de atalho para um item de projeto do SharePoint e, em seguida, escolha **Add** > **Novo Item**. Em qualquer um de **Visual Basic** ou **Visual c#** nó, escolha o **arquivo de recursos** modelo.  
  
    > [!NOTE]  
    >  Certifique-se de adicionar os arquivos de recurso a um item de projeto do SharePoint para habilitar a propriedade de tipo de implantação. Essa propriedade é necessária neste procedimento. Se sua solução não tiver um item de projeto do SharePoint, você pode adicionar um projeto vazio do SharePoint e remover seu padrão *Elements. XML* arquivo.  
  
2.  Nomeie o arquivo de recurso de idioma padrão de sua escolha com uma *. resx* extensão, como Myappresources. Use o mesmo nome de base para cada arquivo de recurso localizado, mas adicione a cultura [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]. Por exemplo, o nome de um alemão recurso localizado *MyAppResources.de-de. resx*.  
  
3.  Altere o valor da **tipo de implantação** propriedade de cada arquivo de recurso para **AppGlobalResource** para fazer com que eles implantem para a pasta do servidor App_GlobalResources.  
  
4.  Se você estiver usando os recursos para localizar o código, além de marcação ASPX, deixe o valor da **ação de compilação** propriedade de cada arquivo como **Embedded Resource**. Se você estiver usando os arquivos de recurso somente para localizar a marcação, você pode, opcionalmente, alterar o valor da propriedade dos arquivos a serem **conteúdo**. Para obter mais informações, consulte [soluções do SharePoint localizar](../sharepoint/localizing-sharepoint-solutions.md).  
  
5.  Abra cada arquivo de recurso e adicione cadeias de caracteres localizadas, usando a mesma cadeia de caracteres IDs em cada arquivo.  
  
6.  No [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] marcação para a página ASPX página ou controle, substitua as cadeias de caracteres embutidas com valores que usam o seguinte formato:  
  
    ```aspx-csharp  
    <%$Resources:Resource File Name, String ID%>  
    ```  
  
     Por exemplo, para localizar o texto de um controle de rótulo em uma página de aplicativo, altere:  
  
    ```aspx-csharp  
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">  
    <asp:Label ID="lbl" runat="server" Text="Label text"></asp:Label>  
    </asp:Content>  
    ```  
  
     para  
  
    ```aspx-csharp  
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">  
    <asp:Label ID="lbl" runat="server" Text="<%$Resources:MyAppResources,String1%>"></asp:Label>  
    </asp:Content>  
    ```  
  
7.  Escolha o **F5** tecla para compilar e executar o aplicativo.  
  
8.  No SharePoint, altere o idioma de exibição do padrão.  
  
     As cadeias de caracteres localizadas aparecem no aplicativo. Para exibir recursos localizados, o servidor do SharePoint deve ter um pacote de idiomas instalado que corresponda à cultura do arquivo de recurso.  
  
## <a name="see-also"></a>Consulte também
 [Localizar soluções do SharePoint](../sharepoint/localizing-sharepoint-solutions.md)   
 [Como: localizar um recurso](../sharepoint/how-to-localize-a-feature.md)   
 [Como: adicionar um arquivo de recurso](../sharepoint/how-to-add-a-resource-file.md)   
 [Como: localizar o código](../sharepoint/how-to-localize-code.md)  
  
