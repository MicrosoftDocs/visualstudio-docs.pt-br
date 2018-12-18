---
title: Atributos de suporte do Site da Web | Microsoft Docs
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
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 312d8a760cc7005afc4308b637b12a292bd20329
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756670"
---
# <a name="web-site-support-attributes"></a>Atributos de suporte a site
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Projeto de site pode ser estendido para fornecer suporte para Web linguagens de programação. O idioma deve ser registrado com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para que os modelos de projeto podem aparecer em de **New Web Site** caixa de diálogo quando o idioma é selecionado.  
  
 O exemplo de IronPython Studio inclui suporte ao site. Você pode encontrá-lo com o [exemplos de VSSDK](../../misc/vssdk-samples.md). Ele inclui as seguintes classes de atributo para registrar o IronPython como uma linguagem de code-behind para novos projetos da Web.  
  
## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute  
 Esse atributo é colocado no projeto de linguagem. Ele adiciona o idioma à lista de idiomas de programação da Web a **linguagem** listar na **New Web Site** caixa de diálogo. Por exemplo, o seguinte adiciona IronPython à lista:  
  
```  
[WebSiteProject("IronPython", "Iron Python")]public class PythonProjectPackage : ProjectPackage  
```  
  
 Esse atributo também define o caminho de modelos para apontar para a pasta de modelos. Para obter mais informações sobre o local da pasta de modelos, consulte [modelos de suporte do Site da Web](../../extensibility/internals/web-site-support-templates.md).  
  
## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute  
 Esse atributo é colocado no projeto de linguagem. Isso permite que o projeto de Site da Web aninhar um tipo de arquivo (relacionado) em outro tipo de arquivo (primário) na **Gerenciador de soluções**.  
  
 Por exemplo:  
  
```  
[WebSiteProjectRelatedFiles("aspx", "py")]public class PythonProjectPackage : ProjectPackage  
```  
  
 Especifica que um arquivo de code-behind do IronPython está relacionado a um arquivo. aspx. Quando uma nova página da Web. aspx é criada em uma solução de site da Web da IronPython, um novo arquivo de origem. py é gerado e aparece como um nó filho da página. aspx.  
  
## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute  
 Esse atributo é colocado sobre o pacote de idioma do projeto. Ele seleciona o provedor do Intellisense para o idioma.  
  
 Por exemplo:  
  
```  
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]public class PythonPackage : Package, IOleComponent  
```  
  
 Especifica que uma instância de PythonIntellisenseProvider, que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>, devem ser criados sob demanda para fornecer serviços de linguagem.  
  
 A implementação de IVsIntellisenseProject trata referências e chama o compilador de linguagem quando uma página da Web com o código é solicitada, mas não é armazenado em cache.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao site](../../extensibility/internals/web-site-support.md)

