---
title: Controle de glifo (VSPackage de controle do código-fonte) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- glyphs, source control packages
- source control packages, glyphs
ms.assetid: b9413b08-b3c3-4fc3-a6e0-3dc0db3652d7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c791647e9718686c5a6c7cf250ca84c74aabbfcc
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39499244"
---
# <a name="glyph-control-source-control-vspackage"></a>Controle de glifo (VSPackage de controle de origem)
Parte da profunda integração disponível para os VSPackages de controle de origem é a capacidade de exibir suas próprias glifos para indicar o status dos itens no controle de origem.  
  
## <a name="levels-of-glyph-control"></a>Níveis de controle de glifo  
 Um glifo de estado é um ícone que indica o status atual de um item quando exibidos, por exemplo, no **Gerenciador de soluções** ou na **exibição de classe**. Um VSPackage de controle do código-fonte pode utilizar dois níveis de controle de glifo. Ele pode limitar a escolha dos glifos a um conjunto predefinido de glifos fornecidos pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE ou ele pode definir um conjunto personalizado de glifos a ser exibido.  
  
### <a name="default-set-of-glyphs"></a>Conjunto padrão de glifos  
 Para determinar os glifos de estado que estão associados um item na **Gerenciador de soluções**, um projeto solicita o glifo de estado do controle do código-fonte usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.GetSccGlyph%2A>. Um controle de fonte VSPackage poderá optar por manter a opção de glifos limitado a glifos predefinidos fornecidos pelo IDE. Nesse caso, o VSPackage passa de uma matriz de valores que representam as enumerações de glifo que são definidas em volta *vsshell.idl*. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>. Isso é um conjunto predefinido de glifos definido pelo IDE, como um cadeado para o glifo de check-in e uma marca de seleção para o glifo de check-out.  
  
### <a name="custom-set-of-glyphs"></a>Conjunto personalizado de glifos  
 Um VSPackage de controle do código-fonte pode usar seus próprio glifos para uma aparência exclusiva quando ele está instalado. Quando um novo controle do código-fonte VSPackage está ativo, ele deve ser capaz de começar a usar seus próprio glifos, mesmo se VSPackage de controle de uma fonte de anterior ainda está carregado, mas inativo. Nesse modo, o VSPackage de controle de origem ainda pode usar os ícones existentes para manter uma aparência consistente com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] se optar por.  
  
 O <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> serviço dá suporte a uma interface, <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>, que pode implementar o VSPackage e que será solicitado pelo IDE. Quando o IDE faz uma solicitação, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] por sua vez tentarão obter essa interface o registrados atualmente do controle de origem VSPackage. Se a interface existir no VSPackage registrado, a solicitação do IDE para glifos personalizados for bem-sucedida; Caso contrário, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE usa seu conjunto padrão de glifos.  
  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs.GetCustomGlyphList%2A> método é usado pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para obter uma lista de imagens mostrando o controle de fonte de vários estados. O VSPackage de controle de origem retorna para o IDE um identificador para a lista de imagens para suas glifos personalizados. O IDE faz uma cópia da lista de imagens no momento e usa-o posteriormente para escolher os glifos para exibir. Se não há suporte para a nova interface ou o `IVsSccGlyphs::GetCustomGlyphList` retorn `E_NOTIMPL`, em seguida, o IDE obtém seus glifos na lista padrão de glifos fornecido pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>   
 <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>