---
title: 'Como: criar marcadores de texto personalizado | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - custom text markers
ms.assetid: 6e32ed81-c604-4a32-9012-8db3bec7c846
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3b0a280b44ad468ba44baf81efcc4e4569638e8b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783075"
---
# <a name="how-to-create-custom-text-markers"></a>Como: criar marcadores de texto personalizado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você quiser criar um marcador de texto personalizado para enfatizar ou organizar o código, você deve executar as seguintes etapas:  
  
- Registrar o novo marcador de texto, de modo que outras ferramentas podem acessá-lo  
  
- Fornecer uma implementação padrão e a configuração do marcador de texto  
  
- Criar um serviço que pode ser usado por outros processos para fazer uso do marcador de texto  
  
  Para obter detalhes sobre como aplicar um marcador de texto em uma região de código, consulte [como: Use marcadores de texto](../extensibility/how-to-use-text-markers.md).  
  
### <a name="to-register-a-custom-marker"></a>Para registrar um marcador personalizado  
  
1. Crie uma entrada de registro da seguinte maneira:  
  
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*\<versão >* \Text Editor\External marcadores\\*\<MarkerGUID >*  
  
    <em>\<MarkerGUID ></em>é um `GUID` usado para identificar o marcador que está sendo adicionado  
  
    *\<Versão >* é a versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], por exemplo 8.0  
  
    *\<PackageGUID >* é o GUID do VSPackage implementa o objeto de automação.  
  
   > [!NOTE]
   >  O caminho raiz do HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*\<versão >* pode ser substituído por uma raiz alternativa quando o shell do Visual Studio é inicializado, para obter mais informações, consulte [De linha de comando](../extensibility/command-line-switches-visual-studio-sdk.md).  
  
2. Crie quatro valores em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*\<versão >* \Text Editor\External marcadores\\*\<MarkerGUID >*  
  
   -   (Padrão)  
  
   -   Serviço  
  
   -   DisplayName  
  
   -   Pacote  
  
   -   `Default` é uma entrada opcional do tipo REG_SZ. Quando definido, o valor da entrada é uma cadeia de caracteres que contém algumas informações úteis de identifica, por exemplo "marcador de texto personalizada".  
  
   -   `Service` é uma entrada do tipo REG_SZ que contém a cadeia de caracteres do GUID do serviço que fornece o marcador de texto personalizado por proffering <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider>. O formato é {XXXXXX XXXX XXXX XXXX XXXXXXXXX}.  
  
   -   `DisplayName` é uma entrada do tipo REG_SZ que contém a ID de recurso do nome do marcador de texto personalizado. O formato é #YYYY.  
  
   -   `Package` é a entrada do tipo REG_SZ que contém o `GUID` de VSPackage que fornece o serviço listado em serviço. O formato é {XXXXXX XXXX XXXX XXXX XXXXXXXXX}.  
  
### <a name="to-create-a-custom-text-marker"></a>Para criar um marcador de texto personalizado  
  
1.  Implementar a interface <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>.  
  
     A implementação dessa interface define o comportamento e aparência do seu tipo de marcador personalizado.  
  
     Essa interface é chamada quando  
  
    1.  Um usuário inicia o IDE pela primeira vez.  
  
    2.  Um usuário seleciona o **Redefinir padrões** botão sob o **fontes e cores** página de propriedades no **ambiente** pasta, localizada no painel esquerdo do  **Opções** caixa de diálogo obtido o **ferramentas** menu do IDE.  
  
2.  Implemente a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider.GetTextMarkerType%2A> método, especificando qual `IVsPackageDefinedTextMarkerType` implementação deve ser retornada com base no tipo de marcador GUID especificado na chamada do método.  
  
     O ambiente chama desta vez o método primeiro seu tipo de marcador personalizada é criado e especifica um GUID que identifica o tipo de marcador personalizado.  
  
### <a name="to-proffer-your-marker-type-as-a-service"></a>Ao oferecer o seu tipo de marcador como um serviço  
  
1.  Chame o <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager.QueryService%2A> método para <xref:Microsoft.VisualStudio.Shell.Interop.SProfferService>.  
  
     Um ponteiro para <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> é retornado.  
  
2.  Chame o <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.ProfferService%2A> método, especificando o GUID que identifica o serviço do tipo de marcador personalizado e fornecendo um ponteiro para sua implementação do <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> interface. Sua <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> implementação deve retornar um ponteiro para sua implementação de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider> interface.  
  
     Um cookie exclusivo de identificação que seu serviço será retornado. Mais tarde você pode usar esse cookie revogar seu serviço do tipo de marcador personalizadas por meio da chamada a <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService.RevokeService%2A> método da <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> interface especificar esse valor de cookie.  
  
## <a name="see-also"></a>Consulte também  
 [Usar marcadores de texto com a API herdada](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [Como: adicionar marcadores de texto padrão](../extensibility/how-to-add-standard-text-markers.md)   
 [Como: implementar o marcador de erros](../extensibility/how-to-implement-error-markers.md)   
 [Como usar marcadores de texto](../extensibility/how-to-use-text-markers.md)

