---
title: Localizando soluções do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.GlobalAndFeatureResource
- VS.SharePoint.Project.AddResourceDialog
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- globalizing [SharePoint development in Visual Studio]
- localizing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ba02d8811fc6633a55e06ae63c9399c70f59634f
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118457"
---
# <a name="localize-sharepoint-solutions"></a>Localizar soluções do SharePoint

  O processo de preparação de seus aplicativos para que possa ser usados em todo o mundo é conhecido como localização. Localização é traduzir recursos para uma cultura específica. Para obter mais informações, consulte [Globalizing e Localizando aplicativos](/visualstudio/ide/globalizing-and-localizing-applications). Este tópico fornece uma visão geral de como localizar uma solução do SharePoint.  
  
 Para localizar uma solução, você remove cadeias de caracteres codificadas do código e abstrai-as em arquivos de recurso. Um arquivo de recurso é um [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]-com base em arquivo com um *resx* extensão. O arquivo de recurso contém as versões traduzidas das cadeias de caracteres usadas em sua solução. Para obter mais informações, consulte [recursos em aplicativos](http://go.microsoft.com/fwlink/?LinkID=155844).  
  
> [!NOTE]  
>  Adicione recursos de cadeia de caracteres apenas para arquivos de recurso de solução do SharePoint. Embora o Editor de recursos permite que você adicione recursos de não cadeia de caracteres, os recursos de não cadeia de caracteres não são implantados no SharePoint.  
  
## <a name="resource-files"></a>Arquivos de recurso
 Há três tipos de arquivos de recurso: padrão, neutralidade de idioma e específicos do idioma.  
  
|Tipo de arquivo de recurso|Descrição|  
|------------------------|-----------------|  
|Padrão|Também conhecido como um recurso de fallback, arquivos de recurso padrão contêm cadeias de caracteres localizadas para a cultura padrão, como o inglês. Eles são usados se nenhum arquivo de recurso localizado para o idioma especificado puder ser encontrado. Recursos padrão não têm arquivos separados, eles são armazenados no assembly principal do aplicativo.|  
|Com neutralidade de idioma|Um arquivo de recurso que contém cadeias de caracteres localizadas para um idioma, mas não uma cultura específica. Por exemplo, "fr" para francês.|  
|Específico do idioma|Um arquivo de recurso que contém cadeias de caracteres localizadas para um idioma e uma cultura. Por exemplo, "fr-CA" para francês canadense.|  
  
 Para obter mais informações, consulte [organização hierárquica de recursos para localização](http://go.microsoft.com/fwlink/?LinkId=178360).  
  
 Para especificar os arquivos de recurso padrão em projetos do SharePoint que você desenvolve no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], escolha **idioma invariável (país invariável)** na lista de cultura a **adicionar recurso** caixa de diálogo quando você Adicione um arquivo de recurso.  
  
## <a name="localize-visual-studio-sharepoint-solutions"></a>Localizar soluções do SharePoint para Visual Studio
 Quando você localiza uma solução, você deve considerar todas as informações textuais que sua solução exibe aos usuários. Mensagens informativas, mensagens de erro e [!INCLUDE[TLA2#tla_ui](../sharepoint/includes/tla2sharptla-ui-md.md)] cadeias de caracteres devem ser traduzidas e as traduções são colocados nos arquivos de recurso.  
  
 Cada cadeia de caracteres em um arquivo de recurso tem um identificador exclusivo. Use o mesmo identificador para a cadeia de caracteres traduzida em cada arquivo de recurso. Por exemplo, se "String1" é o identificador para a primeira cadeia de caracteres no arquivo de recurso padrão, use o mesmo identificador para a primeira cadeia de caracteres nos arquivos de recurso específico do idioma.  
  
 Há três áreas, você localiza normalmente em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] aplicativos do SharePoint: recursos, marcação de página ASPX e código. Para fins de ilustração, as seções a seguir pressupõem que você tem uma solução do SharePoint que você deseja localizar em alemão e japonês. O idioma padrão é inglês.  
  
### <a name="localize-features"></a>Localizar recursos
 Para localizar um recurso, você precisa substituir o título embutido em código e a descrição do recurso com uma expressão que referencia o título traduzido e a cadeia de caracteres no arquivo de recursos localizados. Faça essa alteração na **Designer de recursos** em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para obter mais informações, consulte [como: localizar um recurso](../sharepoint/how-to-localize-a-feature.md).  
  
 Para localizar seu recurso inglês no alemão e japonês, adicione três itens de projeto do arquivo de recurso ao seu projeto: um para inglês, um para alemão e um para japonês. Os arquivos de recurso não podem ser usados para localizar marcação ASPX ou código; arquivos de recurso separados são necessários para eles.  
  
 Depois de criar o recurso de arquivos de recurso, adicione cadeias de caracteres traduzidas a eles. Acesse as cadeias de caracteres localizadas com uma expressão no seguinte formato:  
  
```aspx-csharp  
$Resources:String ID  
```  
  
 Recursos em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] são nomeados sempre como recursos. Se você selecionar um idioma diferente do idioma invariável, em seguida, uma cultura [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] é adicionado ao nome do arquivo de recurso. Por exemplo, se você adicionar um arquivo de recurso do recurso de idioma invariável (padrão), ele é chamado *resx*. Se você adicionar um recurso de recurso específico do idioma, selecionando uma cultura de japonês (Japão), o arquivo é chamado *ja-JP*. Nomes de arquivo de recurso do recurso são atribuídos automaticamente e não podem ser alterados.  
  
 O escopo de recursos é local para o recurso que eles são adicionados ao. Para criar recursos que podem ser usados por qualquer arquivo de recurso ou de elemento na solução, adicione uma **arquivo de recursos globais** item de projeto em vez de um arquivo de recurso. O **arquivo de recursos globais** item de projeto está localizado na **2010** pasta sob **SharePoint** no **Add New Item** caixa de diálogo. Implantar arquivos de recursos globais para a pasta \Resources da pasta raiz do SharePoint.  
  
### <a name="localize-aspx-page-markup"></a>Localizar a marcação da página ASPX
 Para localizar [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] páginas, adicione três itens de projeto do arquivo de recursos ao seu projeto: um para inglês, um para alemão e um para japonês. Se você não precisa localizar código além da marcação, você pode adicionar arquivos de recursos globais.  
  
 Forneça um nome para o arquivo de recurso de idioma padrão. Fornecer arquivos de recursos localizados o mesmo nome anexado a uma cultura específica de idioma [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]. Por exemplo, *MyAppResources.de-de. resx* para o alemão e *Myappresources JP* para japonês.  
  
 Defina as **tipo de implantação** propriedade de cada arquivo de recurso para **AppGlobalResource**. Isso faz com que os arquivos de recurso implantar na pasta App_GlobalResources, onde eles estão disponíveis para todas as páginas e controles ASPX na solução. A pasta App_GlobalResources está localizada em C:\inetpub\wwwroot\wss\VirtualDirectories\\< número da porta\>\App_GlobalResources.  
  
> [!NOTE]  
>  Se você usar arquivos de recurso não globais, mova-os para a pasta de item de projeto para habilitar a propriedade de tipo de implantação e outras propriedades específicas do SharePoint.  
  
 Arquivos de recurso de marcação ASPX também podem ser usados para localizar o código. Se você estiver usando os recursos para localizar o código, além de marcação ASPX, deixe a configuração de propriedade do Build Action de cada arquivo como recurso inserido para fazer com que o recurso seja compilado em um assembly satélite. No entanto, se você estiver usando os arquivos de recurso somente para localizar a marcação, você pode, opcionalmente, alterar Build Action ao conteúdo para impedir que o arquivo que está sendo compilado no assembly principal do aplicativo.  
  
 Substitua todas as cadeias de caracteres codificadas na sua marcação de páginas e controles ASPX com uma expressão no seguinte formato:  
  
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
  
 Para obter mais informações, consulte [como: marcação ASPX localizar](../sharepoint/how-to-localize-aspx-markup.md).  
  
### <a name="localize-code"></a>Localizar código
 Além de localizar cadeias de caracteres de recurso e [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] marcação, você também precisa localizar as cadeias de caracteres de mensagem e cadeias de caracteres de erro que aparecem no código da solução. Informativos localizados e mensagens de erro estão contidas em assemblies satélites. Assemblies satélite contêm cadeias de caracteres que são visíveis aos usuários, tais como [!INCLUDE[TLA2#tla_ui](../sharepoint/includes/tla2sharptla-ui-md.md)] exceções, como mensagens de texto e de saída.  
  
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] usa o modelo padrão de hub e spoke do .NET Framework. O hub ou o assembly de programa principal, contém os recursos de idioma padrão. Os spokes, ou assemblies satélites, contêm os recursos de idioma específico. Para obter mais informações, consulte [Empacotamento e implantação de recursos](http://go.microsoft.com/fwlink/?LinkId=179280). Assemblies satélites são compilados do recurso (*. resx*) arquivos. Quando você adiciona arquivos de recurso específico do idioma ao seu projeto e o pacote de solução [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] compila os arquivos de recurso assemblies satélites nomeados *{nome do projeto}.resources.dll*.  
  
 Assim como acontece com marcação ASPX, localizar o código do aplicativo SharePoint adicionando itens de projeto separados do arquivo de recursos ao seu projeto; um para o idioma padrão e um para cada idioma de localizado. No entanto, como mencionado anteriormente, se você já tiver arquivos de recursos para localização de marcação ASPX, você pode reutilizá-los para localizar o código. Se você precisar criar arquivos de recurso, nomeie o arquivo de recurso de idioma padrão de sua escolha com uma *. resx* extensão. Nomeie os arquivos de recurso localizados o mesmo nome anexado a uma cultura específica de idioma [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]. Defina a propriedade Build Action de cada arquivo de recurso como recurso inserido para habilitar a criação de assemblies satélite de recursos.  
  
 Para criar os assemblies satélite, compile o projeto e, em seguida, adicione os arquivos como assemblies adicionais por meio de **avançado** guia da **Package Designer**. Ao adicionar os assemblies, preceda uma cultura [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] pasta para o caminho local, como *de-DE\\{nome do Item de projeto}.resources.dll*. Isso permite que o pacote contenha arquivos que têm o mesmo nome.  
  
 Em seu código, substitua cadeias de caracteres embutidas com chamadas para o <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> método usando a seguinte sintaxe:  
  
```aspx-csharp  
HttpContext.GetGlobalResourceObject("<Resource File Name>", "<String ID>")  
```  
  
 Para obter mais informações, consulte [como: localizar o código](../sharepoint/how-to-localize-code.md).  
  
#### <a name="web-part-code-localization"></a>Localização de código da Web part
 Web parts incluem um recurso do editor de propriedade personalizada que inclui os atributos de código que usam cadeias de caracteres embutidas, como WebDisplayName, categoria e WebDescription. Para substituir os valores de cadeia de caracteres para esses atributos, crie uma classe separada que deriva da classe do atributo. Nessas classes, defina a propriedade do atributo. A propriedade de atributo depende da classe base. Por exemplo, a propriedade de atributo WebDisplayName é DisplayNameValue e a propriedade de atributo WebDescription é DescriptionValue.  
  
 Na classe derivada, referencie a ID de cadeia de caracteres do arquivo de recurso e o objeto de ResourceManager para obter o valor localizado para a ID da cadeia de caracteres. Retorne este valor para o atributo de editor de propriedade.  
  
## <a name="see-also"></a>Consulte também
 [Como: localizar um recurso](../sharepoint/how-to-localize-a-feature.md)   
 [Como: localizar marcação ASPX](../sharepoint/how-to-localize-aspx-markup.md)   
 [Como: localizar o código](../sharepoint/how-to-localize-code.md)   
 [Como: adicionar um arquivo de recurso](../sharepoint/how-to-add-a-resource-file.md)   
 [Como: usar um arquivo de recurso para especificar nomes localizados, propriedades e permissões](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)  
  
