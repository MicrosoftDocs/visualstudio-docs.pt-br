---
title: Atributos de suporte do site | Microsoft Docs
description: Saiba mais sobre os atributos de suporte do site que são necessários para estender a funcionalidade do Visual Studio usando projetos de site da Web.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 348fd16234e38cd7832ae18e7b28e6abe0bc63d9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901767"
---
# <a name="web-site-support-attributes"></a>Atributos de suporte a site
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] O projeto do site pode ser estendido para dar suporte a linguagens de programação da Web. O idioma deve se registrar com para que os modelos de projeto possam aparecer na caixa de diálogo Novo Site quando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o idioma for selecionado. 

O exemplo do IronPython Studio inclui suporte ao site. O exemplo contém as classes de atributo a seguir para registrar o IronPython como uma linguagem codebehind para novos projetos Web.

## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute
 Esse atributo é colocado no projeto de linguagem. Ele adiciona o idioma à lista de linguagens de programação da Web na **lista Linguagem** na caixa de diálogo **Novo Site.** Por exemplo, o código a seguir adiciona IronPython à lista:

```
[WebSiteProject("IronPython", "Iron Python")]
public class PythonProjectPackage : ProjectPackage
```

 Esse atributo também define o caminho dos modelos para apontar para a pasta templates. Para obter mais informações sobre o local da pasta templates, consulte [Modelos de suporte do site.](../../extensibility/internals/web-site-support-templates.md)

## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute
 Esse atributo é colocado no projeto de linguagem. Ele permite que o projeto site aninhar um tipo de arquivo (relacionado) em outro tipo de arquivo **(primário)** no Gerenciador de Soluções .

 Por exemplo, o código a seguir especifica que um arquivo codebehind do IronPython está relacionado a um arquivo .aspx. Quando uma nova página da Web .aspx é criada em uma solução de site do IronPython, um novo arquivo de origem .py é gerado e aparece como um nó filho da página .aspx.

```
[WebSiteProjectRelatedFiles("aspx", "py")]
public class PythonProjectPackage : ProjectPackage
```

## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute
 Esse atributo é colocado no pacote de projeto de linguagem. Ele seleciona o provedor do IntelliSense para o idioma.

 Por exemplo, o código a seguir especifica que uma instância do PythonIntellisenseProvider, que implementa , deve ser criada sob demanda para fornecer serviços <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject> de linguagem.

```
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]
public class PythonPackage : Package, IOleComponent
```

 A implementação IVsIntellisenseProject trata referências e chama o compilador de linguagem quando uma página da Web com código é solicitada, mas não é armazenada em cache.

## <a name="see-also"></a>Confira também
- [Suporte a site](../../extensibility/internals/web-site-support.md)
