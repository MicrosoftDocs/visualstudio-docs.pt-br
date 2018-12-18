---
title: assemblies de Interoperabilidade primária do Office
ms.custom: ''
ms.date: 09/20/2018
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies
- assemblies [Office development in Visual Studio], primary interop assemblies
- Office primary interop assemblies
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b44352996c1f6cf343f8100abb4f75814765c22a
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672984"
---
# <a name="office-primary-interop-assemblies"></a>assemblies de Interoperabilidade primária do Office

Para usar os recursos de um aplicativo do Microsoft Office a partir de um projeto do Office, você deve usar o PIA (assembly de interoperabilidade primário ) para o aplicativo. O PIA permite que código gerenciado interaja com modelo de objeto baseado em COM de um aplicativo do Microsoft Office.  
  
Quando você cria um novo projeto do Office, o Visual Studio adiciona referências aos PIAs necessários na compilação do projeto. Em alguns cenários, pode ser necessário adicionar referências a PIAs extras (por exemplo, se você quiser usar um recurso do Microsoft Office Word em um projeto do Microsoft Office Excel).  
  
Este tópico descreve os seguintes aspectos de uso de PIAs do Microsoft Office em projetos do Office:  
  
- [Assemblies de interoperabilidade primários separados para criar e executar projetos](#separateassemblies)  
  
- [Usar recursos de vários aplicativos do Microsoft Office em um único projeto](#usingfeatures)  
  
- [Lista completa de assemblies de interoperabilidade primários para aplicativos do Microsoft Office](#pialist)  
  
Para obter mais informações sobre assemblies de interoperabilidade primários, consulte [assemblies de interoperabilidade primários](/previous-versions/dotnet/netframework-4.0/aax7sdch(v=vs.100)).  

<a name="separateassemblies"></a> 

## <a name="separate-primary-interop-assemblies-to-build-and-run-projects"></a>Assemblies de interoperabilidade primários separados para criar e executar projetos  

O Visual Studio usa diferentes conjuntos de PIAs no computador de desenvolvimento. Esses diferentes conjuntos de assemblies estão nos seguintes locais:  
  
- Uma pasta no diretório de arquivos de programa  
  
  Essas cópias de assemblies são usadas ao gravar códigos e compilar projetos. O Visual Studio instala esses assemblies automaticamente.  
  
- O cache de assembly global  
  
  Essas cópias de assemblies são usadas durante algumas tarefas de desenvolvimento, tais como ao executar ou depurar projetos. O Visual Studio não instala nem registra esses assemblies. Você deve fazer isso sozinho.  
  
### <a name="primary-interop-assemblies-in-the-program-files-directory"></a>Assemblies de interoperabilidade primários no diretório de arquivos de programa  

Quando você instala o Visual Studio, os PIAs são automaticamente instalados em um local no sistema de arquivos, fora do cache de assembly global. Quando você cria um novo projeto, o Visual Studio adiciona automaticamente referências a essas cópias de PIAs ao seu projeto. O Visual Studio usa essas cópias de PIAs, em vez dos assemblies no cache de assembly global, para resolver referências de tipo quando você desenvolve e compila seu projeto.  
  
Essas cópias de PIAs ajudam o Visual Studio a evitar vários problemas de desenvolvimento que podem ocorrer quando diferentes versões de PIAs estão registradas no cache de assembly global.  
  
O Visual Studio instala essas cópias de PIAs nos seguintes locais no computador de desenvolvimento:  
  
- *%ProgramFiles%\Microsoft visual Studio 12.0\Visual Studio Tools for Office\PIA\Office14*  
  
  (ou *% ProgramFiles (x86) %\Microsoft Visual Studio 12.0\Visual Studio Tools for Office\PIA\Office14* em sistemas operacionais de 64 bits)  
  
- *%ProgramFiles%\Microsoft visual Studio 12.0\Visual Studio Tools for Office\PIA\Office15*  
  
  (ou *% ProgramFiles (x86) %\Microsoft Visual Studio 12.0\Visual Studio Tools for Office\PIA\Office15* em sistemas operacionais de 64 bits)  
  
### <a name="primary-interop-assemblies-in-the-global-assembly-cache"></a>Assemblies de interoperabilidade primários no cache de assembly global  

Para realizar certas tarefas de desenvolvimento, os PIAs devem ser instalados e registrados no cache de assembly global no computador de desenvolvimento. Normalmente, os PIAs são instalados automaticamente quando você instala o Office no computador de desenvolvimento. Para obter mais informações, consulte [configurar um computador para desenvolver soluções do Office](../vsto/configuring-a-computer-to-develop-office-solutions.md).  
  
Os PIAs do Office não são necessários em computadores de usuário final para executar soluções do Office. Para obter mais informações, consulte [Design e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md).  

<a name="usingfeatures"></a>

## <a name="use-features-of-multiple-microsoft-office-applications-in-a-single-project"></a>Usar recursos de vários aplicativos do Microsoft Office em um único projeto  

Cada modelo de projeto do Office em Visual Studio é projetado para funcionar com um único aplicativo do Microsoft Office. Para usar recursos em vários aplicativos do Microsoft Office ou usar recursos em um aplicativo ou componente que não tem projeto no Visual Studio, você deve adicionar uma referência aos PIAs necessários.  
  
Na maioria dos casos, você deve adicionar referências aos PIAs são instalados pelo Visual Studio sob o `%ProgramFiles%\Microsoft Visual Studio 12.0\Visual Studio Tools for Office\PIA\` directory. Estas versões de assemblies aparecem na **Framework** guia da **Gerenciador de referências** caixa de diálogo. Para obter mais informações, consulte [como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md).  
  
Se você tiver instalado e registrado os PIAs no cache de assembly global, estas versões de assemblies aparecem na **COM** guia o **Gerenciador de referências** caixa de diálogo. Você deve evitar adicionar referências a essas versões de assemblies, porque alguns problemas de desenvolvimento podem ocorrer ao usá-las. Por exemplo, se você registrou diferentes versões de PIAs no cache de assembly global, seu projeto se associará automaticamente para a versão do assembly que foi registrado por último — mesmo se você especificar uma versão diferente do assembly no  **COM** guia do **Gerenciador de referências** caixa de diálogo.  
  
> [!NOTE]  
>  Alguns assemblies são adicionados a um projeto automaticamente quando um assembly que lhes faz referência é adicionado. Por exemplo, a referência para o *dll* e *Office* assemblies são adicionados automaticamente quando você adiciona uma referência para o Word, Excel, Outlook, Microsoft Forms ou gráfico assemblies.  

<a name="pialist"></a> 

## <a name="primary-interop-assemblies-for-microsoft-office-applications"></a>Assemblies de interoperabilidade primários para aplicativos do Microsoft Office  

A tabela a seguir lista os assemblies de interoperabilidade primários disponíveis para [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)].  

<br/>

|Aplicativo ou componente do Office|Nome do assembly de interoperabilidade primário|  
|-------------------------------------|-----------------------------------|  
|Biblioteca de Objetos do Microsoft Access 14.0<br /><br /> Biblioteca de Objetos do Microsoft Access 15.0|Microsoft.Office.Interop.Access.dll|  
|Biblioteca de Objetos do Mecanismo de Banco de Dados do Microsoft Office 14.0 Access<br /><br /> Biblioteca de Objetos do Mecanismo de Banco de Dados do Microsoft Office 15.0 Access|Microsoft.Office.Interop.Access.Dao.dll|  
|Biblioteca de Objetos do Microsoft Excel 14.0<br /><br /> Biblioteca de Objetos do Microsoft Excel 15.0|[Microsoft.Office.Interop.Excel.dll](https://docs.microsoft.com/dotnet/api/microsoft.office.interop.excel?view=excel-pia)|  
|Biblioteca de Objetos do Microsoft Graph 14.0 (usado pelo PowerPoint, Access e Word para gráficos)<br /><br /> Biblioteca de Objetos do Microsoft Graph 15.0|Microsoft.Office.Interop.Graph.dll|  
|Biblioteca de Tipos do Microsoft InfoPath 2.0 (apenas para InfoPath 2007)|[Microsoft.Office.Interop.InfoPath.dll](https://docs.microsoft.com/dotnet/api/microsoft.office.interop.infopath?view=infopath-form)|  
|Assembly de Interoperabilidade do Microsoft InfoPath XML (apenas para InfoPath 2007)|Microsoft.Office.Interop.InfoPath.Xml.dll|  
|Biblioteca de Objetos do Microsoft Office 14.0 (funcionalidade compartilhada do Office)<br /><br /> Biblioteca de Objetos do Microsoft Office 15.0 (funcionalidade compartilhada do Office)|office.dll|  
|Controle de Exibição do Microsoft Office Outlook (pode ser usado em páginas Web e aplicativos para acessar a sua caixa de entrada)|Microsoft.Office.Interop.OutlookViewCtl.dll|  
|Biblioteca de Objetos do Microsoft Outlook 14.0<br /><br /> Biblioteca de Objetos do Microsoft Outlook 15.0|[Microsoft.Office.Interop.Outlook.dll](https://docs.microsoft.com/dotnet/api/microsoft.office.interop.outlook?view=outlook-pia)|  
|Biblioteca de Objetos do Microsoft PowerPoint 14.0<br /><br /> Biblioteca de Objetos do Microsoft PowerPoint 15.0|Microsoft.Office.Interop.PowerPoint.dll|  
|Biblioteca de Objetos do Microsoft Project 14.0<br /><br /> Biblioteca de Objetos do Microsoft Project 15.0|[Microsoft.Office.Interop.MSProject.dll](https://docs.microsoft.com/dotnet/api/microsoft.office.interop.msproject?view=office-project-server)|  
|Biblioteca de Objetos do Microsoft Publisher 14.0<br /><br /> Biblioteca de Objetos do Microsoft Publisher 15.0|Microsoft.Office.Interop.Publisher.dll|  
|Biblioteca de Referência de Objetos da Web do Microsoft SharePoint Designer 14.0|Microsoft.Office.Interop.SharePointDesigner.dll|  
|Biblioteca de Referência de Objetos de Página do Microsoft SharePoint Designer 14.0|Microsoft.Office.Interop.SharePointDesignerPage.dll|  
|Biblioteca de tipos do Microsoft Smart Tags 2.0 **Observação:** marcas inteligentes foram preteridas no [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] e [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].|Microsoft.Office.Interop.SmartTag.dll|  
|Biblioteca de Tipos do Microsoft Visio 14.0<br /><br /> Biblioteca de Tipos do Microsoft Visio 15.0|Microsoft.Office.Interop.Visio.dll|  
|Biblioteca de Tipos Salvar como Web do Microsoft Visio 14.0<br /><br /> Biblioteca de Tipos Salvar como Web do Microsoft Visio 15.0|Microsoft.Office.Interop.Visio.SaveAsWeb.dll|  
|Biblioteca de Tipos de Controle de Desenho do Microsoft Visio 14.0<br /><br /> Biblioteca de Tipos de Controle de Desenho do Microsoft Visio 15.0|Microsoft.Office.Interop.VisOcx.dll|  
|Biblioteca de Objetos do Microsoft Word 14.0<br /><br /> Biblioteca de Objetos do Microsoft Word 15.0|[Microsoft.Office.Interop.Word.dll](https://docs.microsoft.com/dotnet/api/microsoft.office.interop.word?view=word-pia)|  
|Microsoft Visual Basic for Applications Extensibility 5.3|Microsoft.Vbe.Interop.dll|  
  
### <a name="binding-redirect-assemblies"></a>Assemblies de redirecionamento de associação  

Quando você instala e registra os PIAs do Office no cache de assembly global (seja com o Office ou instalando o pacote redistribuível para PIAs), os assemblies de redirecionamento de associação também são instalados apenas no cache de assembly global. Esses assemblies ajudam a garantir que a versão correta dos assemblies de interoperabilidade primários é carregada no tempo de execução. 

Por exemplo, quando uma solução que faz referência ao assembly do [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] é executada em um computador que tem a versão [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] do mesmo assembly de interoperabilidade primário, o assembly de redirecionamento de associação instrui o tempo de execução do [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] para carregar a versão do [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] do assembly de interoperabilidade primário. 

Para obter mais informações, consulte [como: habilitar e desabilitar o redirecionamento de associação automática](/dotnet/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection).  
  
## <a name="see-also"></a>Consulte também  

- [Como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)   
- [Visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md)   
- [Soluções InfoPath](../vsto/infopath-solutions.md)   
- [Visão geral de modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md)   
- [Soluções PowerPoint](../vsto/powerpoint-solutions.md)   
- [Soluções de projeto](../vsto/project-solutions.md)   
- [Visão geral do modelo de objeto do Visio](../vsto/visio-object-model-overview.md)   
- [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)   
- [Referência geral &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/general-reference-office-development-in-visual-studio.md)  
  
  
