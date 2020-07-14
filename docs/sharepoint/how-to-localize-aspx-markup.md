---
title: 'Como: localizar marcação ASPX | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing XML [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 63bd8ee614a78752069002820689a2cc6c0be783
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016279"
---
# <a name="how-to-localize-aspx-markup"></a>Como: localizar marcação ASPX
  [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]as páginas (. aspx) normalmente usam valores de cadeia de caracteres embutidos em código. Para localizar essas cadeias de caracteres, substitua-as por expressões que fazem referência a recursos localizados.

## <a name="localize-aspx-markup"></a>Localizar marcação ASPX

#### <a name="to-localize-aspx-markup"></a>Para localizar marcação ASPX

1. Adicione arquivos de recurso separados: um para o idioma padrão e outro para cada idioma localizado.

     Se você estiver localizando apenas marcação e não código, adicione um item de projeto de arquivo de recursos globais. Se você estiver localizando código e marcação, adicione um item de projeto de arquivo de recursos.

    1. Para adicionar um arquivo de recursos globais, em **Gerenciador de soluções**, abra o menu de atalho para um item de projeto do SharePoint e escolha **Adicionar**  >  **novo item**. No nó SharePoint **2010** , escolha o modelo de **arquivo de recursos globais** .

    2. Para adicionar um arquivo de recursos, em **Gerenciador de soluções**, abra o menu de atalho para um item de projeto do SharePoint e escolha **Adicionar**  >  **novo item**. No nó **Visual Basic** ou no **Visual C#** , escolha o modelo de **arquivo de recursos** .

    > [!NOTE]
    > Certifique-se de adicionar os arquivos de recurso a um item de projeto do SharePoint para habilitar a propriedade do tipo de implantação. Essa propriedade é necessária posteriormente neste procedimento. Se sua solução não tiver um item de projeto do SharePoint, você poderá adicionar um projeto do SharePoint vazio e remover seu arquivo de *Elements.xml* padrão.

2. Dê ao arquivo de recurso de idioma padrão um nome de sua escolha anexado com uma extensão *. resx* , como MyAppResources. resx. Use o mesmo nome de base para cada arquivo de recurso localizado, mas adicione a cultura [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] . Por exemplo, nomeie um recurso localizado *em alemão MyAppResources.de-de. resx*.

3. Altere o valor da propriedade **tipo de implantação** de cada arquivo de recurso para **AppGlobalResource** para fazer com que eles sejam implantados na pasta App_GlobalResources do servidor.

4. Se você estiver usando os recursos para localizar o código, além da marcação ASPX, deixe o valor da propriedade **criar ação** de cada arquivo como **recurso incorporado**. Se você estiver usando os arquivos de recurso somente para localizar a marcação, você pode opcionalmente alterar o valor da propriedade dos arquivos para **conteúdo**. Para obter mais informações, consulte [Localizar soluções do SharePoint](../sharepoint/localizing-sharepoint-solutions.md).

5. Abra cada arquivo de recurso e adicione cadeias de caracteres localizadas, usando as mesmas IDs de cadeia em cada arquivo.

6. Na [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] marcação para a página ou controle aspx, substitua as cadeias de caracteres embutidas em código por valores que usam o seguinte formato:

    ```aspx-csharp
    <%$Resources:Resource File Name, String ID%>
    ```

     Por exemplo, para localizar o texto de um controle rótulo em uma página de aplicativo, você alteraria:

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

7. Escolha a tecla **F5** para compilar e executar o aplicativo.

8. No SharePoint, altere o idioma de exibição do padrão.

     As cadeias de caracteres localizadas aparecem no aplicativo. Para exibir recursos localizados, o servidor do SharePoint deve ter um pacote de idiomas instalado que corresponda à cultura do arquivo de recurso.

## <a name="see-also"></a>Consulte também
- [Localizar soluções do SharePoint](../sharepoint/localizing-sharepoint-solutions.md)
- [Como localizar um recurso](../sharepoint/how-to-localize-a-feature.md)
- [Como adicionar um arquivo de recurso](../sharepoint/how-to-add-a-resource-file.md)
- [Como: Localizar código](../sharepoint/how-to-localize-code.md)
