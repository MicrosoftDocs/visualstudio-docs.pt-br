---
title: Localizando soluções do SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VS.SharePointTools.Project.GlobalAndFeatureResource
- VS.SharePoint.Project.AddResourceDialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalizing [SharePoint development in Visual Studio]
- localizing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0a7b04ab1f77eba15f2bc617f89514a8d0952674
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017145"
---
# <a name="localize-sharepoint-solutions"></a>Localizar soluções do SharePoint

  O processo de preparação de seus aplicativos para que eles possam ser usados em todo o mundo é conhecido como localização. A localização está traduzindo recursos para uma cultura específica. Para obter mais informações, consulte [Globalizando e Localizando aplicativos](../ide/globalizing-and-localizing-applications.md). Este tópico fornece uma visão geral de como localizar uma solução do SharePoint.

 Para localizar uma solução, você remove cadeias de caracteres embutidas no código e as abstrai em arquivos de recursos. Um arquivo de recurso é um [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] arquivo baseado em uma extensão *. resx* . O arquivo de recursos contém as versões traduzidas das cadeias de caracteres usadas em sua solução. Para obter mais informações, consulte [recursos em aplicativos](/previous-versions/dotnet/netframework-4.0/f45fce5x(v=vs.100)).

> [!NOTE]
> Adicione somente recursos de cadeia de caracteres aos arquivos de recurso de solução do SharePoint. Embora o editor de recursos permita adicionar recursos que não sejam de cadeia de caracteres, os recursos que não são de cadeia de caracteres não são implantados no SharePoint.

## <a name="resource-files"></a>Arquivos de recurso
 Há três tipos de arquivos de recurso: padrão, neutro de idioma e específico de idioma.

|Tipo de arquivo de recurso|Descrição|
|------------------------|-----------------|
|Padrão|Também conhecido como um recurso de fallback, os arquivos de recurso padrão contêm cadeias de caracteres localizadas para a cultura padrão, como o inglês. Eles serão usados se nenhum arquivo de recurso localizado para o idioma especificado puder ser encontrado. Os recursos padrão não têm arquivos separados, eles são armazenados no assembly principal do aplicativo.|
|Neutro de idioma|Um arquivo de recurso que contém cadeias de caracteres localizadas para um idioma, mas não uma cultura específica. Por exemplo, "fr" para francês.|
|Específico do idioma|Um arquivo de recurso que contém cadeias de caracteres localizadas para um idioma e uma cultura. Por exemplo, "fr-CA" para francês canadense.|

 Para obter mais informações, consulte [organização hierárquica de recursos para localização](../ide/globalizing-and-localizing-applications.md).

 Para especificar arquivos de recurso padrão em projetos do SharePoint que você desenvolve no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , escolha **Idioma invariável (país invariável)** na lista de culturas da caixa de diálogo **Adicionar recurso** ao adicionar um arquivo de recurso.

## <a name="localize-visual-studio-sharepoint-solutions"></a>Localizar soluções do Visual Studio SharePoint
 Ao localizar uma solução, você deve considerar todas as informações textuais que sua solução exibe para os usuários. Mensagens informativas, mensagens de erro e [!INCLUDE[TLA2#tla_ui](../sharepoint/includes/tla2sharptla-ui-md.md)] cadeias de caracteres devem ser traduzidas e as conversões colocadas nos arquivos de recurso.

 Cada cadeia de caracteres em um arquivo de recurso tem um identificador exclusivo. Use o mesmo identificador para a cadeia de caracteres traduzida em cada arquivo de recurso. Por exemplo, se "seqüência1" for o identificador da primeira cadeia de caracteres no arquivo de recurso padrão, use o mesmo identificador para a primeira cadeia de caracteres nos arquivos de recursos específicos do idioma.

 Há três áreas que você normalmente localiza em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] aplicativos do SharePoint: recursos, marcação de página aspx e código. Para fins de ilustração, as seções a seguir pressupõem que você tenha uma solução do SharePoint que você deseja localizar em alemão e japonês. O idioma padrão é inglês.

### <a name="localize-features"></a>Recursos do localize
 Para localizar um recurso, você precisa substituir o título e a descrição embutidos em código do recurso por uma expressão que referencie o título e a cadeia de caracteres traduzidos no arquivo de recursos localizado. Você faz essa alteração no **Designer de recursos** no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Para obter mais informações, consulte [como: localizar um recurso](../sharepoint/how-to-localize-a-feature.md).

 Para localizar o recurso em inglês em alemão e japonês, adicione três itens de projeto de arquivo de recurso ao seu projeto: um para inglês, um para alemão e outro para japonês. Arquivos de recursos de recurso não podem ser usados para localizar código ou marcação ASPX; arquivos de recurso separados são necessários para eles.

 Depois de criar os arquivos de recurso de recurso, adicione cadeias de caracteres traduzidos a eles. Acesse as cadeias de caracteres localizadas com uma expressão no seguinte formato:

```aspx-csharp
$Resources:String ID
```

 Recursos de recurso no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] são sempre chamados de recursos. Se você selecionar um idioma diferente do idioma invariável, uma cultura [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] será adicionada ao nome do arquivo de recurso. Por exemplo, se você adicionar um arquivo de recurso de recurso de Idioma invariável (padrão), ele será chamado de *Resources. resx*. Se você adicionar um recurso de recurso específico a um idioma selecionando uma cultura de japonês (Japão), o arquivo será chamado de *Resources. ja-JP. resx*. Os nomes de arquivo de recursos de recurso são automaticamente atribuídos e não podem ser alterados.

 O escopo dos recursos de recurso é local para o recurso ao qual eles são adicionados. Para criar recursos que podem ser usados por qualquer recurso ou arquivo de elemento na solução, adicione um item de projeto de **arquivo de recursos globais** em vez de um arquivo de recurso de recurso. O item de projeto de **arquivo de recursos globais** está localizado na pasta **2010** em **SharePoint** na caixa de diálogo **Adicionar novo item** . Os arquivos de recursos globais são implantados na pasta \resources da pasta raiz do SharePoint.

### <a name="localize-aspx-page-markup"></a>Localizar marcação de página ASPX
 Para localizar [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] páginas, você adiciona três itens de projeto de arquivo de recursos ao seu projeto: um para inglês, um para alemão e outro para japonês. Se você não precisar localizar o código além da marcação, poderá adicionar arquivos de recursos globais.

 Forneça um nome para o arquivo de recurso de idioma padrão. Forneça os arquivos de recurso localizados com o mesmo nome anexado à cultura específica do idioma [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] . Por exemplo, *MyAppResources.de-de. resx* para alemão e *MyAppResources. ja-JP. resx* para japonês.

 Defina a propriedade **tipo de implantação** de cada arquivo de recurso como **AppGlobalResource**. Isso faz com que os arquivos de recurso sejam implantados na pasta App_GlobalResources, onde estão disponíveis para todas as páginas ASPX e controles na solução. A pasta App_GlobalResources está localizada em C:\inetpub\wwwroot\wss\VirtualDirectories \\<número da porta \> \ App_GlobalResources.

> [!NOTE]
> Se você usar arquivos de recurso não globais, mova-os para a pasta de item de projeto para habilitar a propriedade do tipo de implantação e outras propriedades específicas do SharePoint.

 Os arquivos de recurso de marcação ASPX também podem ser usados para localizar o código. Se você estiver usando os recursos para localizar o código além da marcação ASPX, deixe a configuração de propriedade da ação de compilação de cada arquivo como recurso incorporado para fazer com que o recurso seja compilado em um assembly satélite. No entanto, se você estiver usando os arquivos de recurso somente para localizar marcação, você pode opcionalmente alterar a ação de compilação para conteúdo para impedir que o arquivo seja compilado no assembly do aplicativo principal.

 Substitua todas as cadeias de caracteres de propriedades embutidas em código em suas páginas ASPX e controle a marcação com uma expressão no seguinte formato:

```aspx-csharp
<asp:<class> runat="server" Text="<%$Resources:<Resource File Name>, <String ID>%>" />
```

 Por exemplo:

```aspx-csharp
<asp:Button ID="btn1" runat="server" onclick="btn1_Click" Text="<%$Resources:Resource1,String7%>"></asp:Button>
```

 Para ASPX como texto, use uma expressão no seguinte formato:

```aspx-csharp
<asp:literal ID="<ID>" runat="server" Text="<%$Resources:<Resource File Name>, <String ID>%>" />
```

 Por exemplo:

```aspx-csharp
<asp:literal ID="Literal1" runat="server" Text="<%$Resources:Resource1, String9%>" />
```

 Para obter mais informações, consulte [como: localizar marcação aspx](../sharepoint/how-to-localize-aspx-markup.md).

### <a name="localize-code"></a>Código de localização
 Além de localizar cadeias de caracteres de recurso e [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] marcação, você também precisa localizar as cadeias de caracteres de mensagem e de erro que aparecem no código da solução. As mensagens informativas e de erro localizadas estão contidas em assemblies satélites. Os assemblies satélite contêm cadeias de caracteres que são visíveis para os usuários, como [!INCLUDE[TLA2#tla_ui](../sharepoint/includes/tla2sharptla-ui-md.md)] mensagens de texto e de saída como exceções.

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]usa o Hub de .NET Framework padrão e o modelo de spoke. O Hub ou o assembly do programa principal contém os recursos de idioma padrão. Os spokes, ou assemblies satélite, contêm os recursos específicos do idioma. Para obter mais informações, consulte [Empacotamento e implantação de recursos](/previous-versions/dotnet/netframework-4.0/sb6a8618(v=vs.100)). Os assemblies satélite são compilados a partir de arquivos de recurso (*. resx*). Quando você adiciona arquivos de recursos específicos a um idioma ao seu projeto e ao pacote de solução, o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] compila os arquivos de recurso em assemblies satélite chamados *{Project Name} .resources.dll*.

 Assim como acontece com a marcação ASPX, localize o código do aplicativo SharePoint adicionando itens de projeto de arquivo de recursos separados ao seu projeto; um para o idioma padrão e outro para cada idioma localizado. No entanto, como mencionado anteriormente, se você já tiver arquivos de recursos para localizar a marcação ASPX, poderá reutilizá-los para o código de localização. Se você precisar criar arquivos de recursos, dê ao arquivo de recurso de idioma padrão um nome de sua escolha anexado com uma extensão *. resx* . Nomeie os arquivos de recursos localizados com o mesmo nome anexado à cultura específica do idioma [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] . Defina a propriedade de ação de compilação de cada arquivo de recurso como recurso incorporado para habilitar a criação de assemblies de recursos de satélite.

 Para criar os assemblies satélite, compile o projeto e, em seguida, adicione os arquivos como assemblies adicionais por meio da guia **avançado** do **Designer de pacote**. Ao adicionar os assemblies, preceda uma [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] pasta de cultura no caminho do local, como *DE-de \\ {Project Item Name} .resources.dll*. Isso permite que o pacote contenha arquivos com o mesmo nome.

 Em seu código, substitua cadeias de caracteres embutidas em código por chamadas para o <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> método usando a seguinte sintaxe:

```aspx-csharp
HttpContext.GetGlobalResourceObject("<Resource File Name>", "<String ID>")
```

 Para obter mais informações, consulte [como: Localizar código](../sharepoint/how-to-localize-code.md).

#### <a name="web-part-code-localization"></a>Localização de código de Web Part
 As Web Parts incluem um recurso personalizado do editor de propriedades que inclui atributos de código que usam cadeias de caracteres embutidas em código, como WebDisplayName, categoria e WebDescription. Para substituir os valores de cadeia de caracteres para esses atributos, crie uma classe separada que derive da classe do atributo. Nessas classes, defina a propriedade do atributo. A propriedade de atributo depende da classe base. Por exemplo, a propriedade de atributo WebDisplayName é DisplayNamevalue e a propriedade de atributo WebDescription é Descriçãovalue.

 Na classe derivada, referencie a ID da cadeia de caracteres do arquivo de recursos e o objeto ResourceManager para obter o valor localizado para a ID da cadeia de caracteres. Retornar esse valor para o atributo do editor de propriedades.

## <a name="see-also"></a>Consulte também
- [Como localizar um recurso](../sharepoint/how-to-localize-a-feature.md)
- [Como: localizar marcação ASPX](../sharepoint/how-to-localize-aspx-markup.md)
- [Como: Localizar código](../sharepoint/how-to-localize-code.md)
- [Como adicionar um arquivo de recurso](../sharepoint/how-to-add-a-resource-file.md)
- [Como: usar um arquivo de recurso para especificar nomes, propriedades e permissões localizadas](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
