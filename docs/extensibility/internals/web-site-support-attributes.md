---
title: Atributos de suporte do Site da Web | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b312322c1d707f13c5121f1fd159f3fd7736886c
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31140830"
---
# <a name="web-site-support-attributes"></a>Atributos de suporte do Site da Web
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Projeto de site pode ser estendido para oferecer suporte para Web linguagens de programação. O idioma deve ser registrado com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para que os modelos de projeto podem aparecer no **novo Site** caixa de diálogo quando o idioma é selecionado.

O exemplo de IronPython Studio inclui suporte do site da web. O exemplo contém as seguintes classes de atributo para registrar o IronPython como uma linguagem de code-behind para novos projetos da Web.

## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute
 Esse atributo é colocado no projeto de idioma. Ele adiciona o idioma para a lista de idiomas de programação da Web a **idioma** lista o **novo Site** caixa de diálogo. Por exemplo, o código a seguir adiciona o IronPython à lista:

```
[WebSiteProject("IronPython", "Iron Python")]
public class PythonProjectPackage : ProjectPackage
```

 Esse atributo também define o caminho de modelos para apontar para a pasta de modelos. Para obter mais informações sobre o local da pasta de modelos, consulte [modelos de suporte do Site](../../extensibility/internals/web-site-support-templates.md).

## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute
 Esse atributo é colocado no projeto de idioma. Ele permite que o projeto de Site da Web aninhar um tipo de arquivo (relacionado) em outro tipo de arquivo (primário) no **Gerenciador de soluções**.

 Por exemplo, o código a seguir especifica que um arquivo de code-behind IronPython está relacionado a um arquivo. aspx. Quando uma nova página da Web. aspx é criada em uma solução de site da Web de IronPython, um novo arquivo de origem py é gerado e aparece como um nó filho da página. aspx.

```
[WebSiteProjectRelatedFiles("aspx", "py")]
public class PythonProjectPackage : ProjectPackage
```

## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute
 Esse atributo é colocado no pacote de idiomas do projeto. Ele seleciona o provedor do IntelliSense para o idioma.

 Por exemplo, o código a seguir especifica que uma instância de PythonIntellisenseProvider, que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>, devem ser criados sob demanda para fornecer serviços de idioma.

```
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]
public class PythonPackage : Package, IOleComponent
```

 A implementação IVsIntellisenseProject trata referências e chama o compilador de linguagem quando uma página da Web com o código foi solicitada, mas não é armazenado em cache.

## <a name="see-also"></a>Consulte também
 [Suporte ao site](../../extensibility/internals/web-site-support.md)