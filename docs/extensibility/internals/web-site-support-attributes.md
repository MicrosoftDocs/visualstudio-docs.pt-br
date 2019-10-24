---
title: Atributos de suporte do site | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 07486ea3a962bcb81f65ad0b61ea2e41b3248678
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721607"
---
# <a name="web-site-support-attributes"></a>Atributos de suporte a site
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projeto de site pode ser estendido para fornecer suporte a linguagens de programação da Web. O idioma deve se registrar com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para que os modelos de projeto possam aparecer na caixa de diálogo **novo site** quando o idioma for selecionado.

O exemplo do IronPython Studio inclui suporte a sites da Web. O exemplo contém as classes de atributo a seguir para registrar o IronPython como uma linguagem codebehind para novos projetos Web.

## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute
 Esse atributo é colocado no projeto de idioma. Ele adiciona o idioma à lista de linguagens de programação da Web na lista **idioma** da caixa de diálogo **novo site da Web** . Por exemplo, o código a seguir adiciona o IronPython à lista:

```
[WebSiteProject("IronPython", "Iron Python")]
public class PythonProjectPackage : ProjectPackage
```

 Esse atributo também define o caminho de modelos para apontar para a pasta modelos. Para obter mais informações sobre o local da pasta modelos, consulte [modelos de suporte do site](../../extensibility/internals/web-site-support-templates.md).

## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute
 Esse atributo é colocado no projeto de idioma. Ele permite que o projeto de site aninhe um tipo de arquivo (relacionado) em outro tipo de arquivo (primário) no **Gerenciador de soluções**.

 Por exemplo, o código a seguir especifica que um arquivo codebehind do IronPython está relacionado a um arquivo. aspx. Quando uma nova página da Web. aspx é criada em uma solução de site da IronPython, um novo arquivo de origem. py é gerado e exibido como um nó filho da página. aspx.

```
[WebSiteProjectRelatedFiles("aspx", "py")]
public class PythonProjectPackage : ProjectPackage
```

## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute
 Esse atributo é colocado no pacote de projeto de idioma. Ele seleciona o provedor IntelliSense para o idioma.

 Por exemplo, o código a seguir especifica que uma instância de PythonIntellisenseProvider, que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>, deve ser criada sob demanda para fornecer serviços de linguagem.

```
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]
public class PythonPackage : Package, IOleComponent
```

 A implementação de IVsIntellisenseProject manipula referências e chama o compilador de linguagem quando uma página da Web com código é solicitada, mas não é armazenada em cache.

## <a name="see-also"></a>Consulte também
- [Suporte ao site](../../extensibility/internals/web-site-support.md)