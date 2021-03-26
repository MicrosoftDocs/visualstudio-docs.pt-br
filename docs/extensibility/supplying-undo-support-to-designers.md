---
title: Fornecendo suporte de desfazer para designers | Microsoft Docs
description: Saiba como fornecer suporte para desfazer em designers, seja automaticamente ou usando recursos no SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], undo support
ms.assetid: 43eb1f14-b129-404a-8806-5bf9b099b67b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6b56eb762cf4a2746af04ed69c7c4c49afc15dec
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056305"
---
# <a name="supply-undo-support-to-designers"></a>Fornecer suporte de desfazer para designers

Designers, como editores, normalmente precisam oferecer suporte a operações de desfazer para que os usuários possam reverter suas alterações recentes ao modificar um elemento de código.

A maioria dos designers implementados no Visual Studio têm suporte de "desfazer" automaticamente fornecido pelo ambiente.

Implementações de designer que precisam fornecer suporte para o recurso de desfazer:

- Fornecer gerenciamento de desfazer implementando a classe base abstrata <xref:System.ComponentModel.Design.UndoEngine>

- Forneça suporte a persistência e CodeDOM implementando <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> as  <xref:System.ComponentModel.Design.IComponentChangeService> classes e.

Para obter mais informações sobre como escrever designers usando .NET Framework, consulte [estender Design-Time support](/previous-versions/37899azc(v=vs.140)).

O [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] fornece uma infraestrutura de desfazer padrão por:

- Fornecer implementações de gerenciamento de desfazer por meio das <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> classes e.

- Fornecendo suporte a persistência e CodeDOM por meio do padrão <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> e das <xref:System.ComponentModel.Design.IComponentChangeService> implementações.

## <a name="obtain-undo-support-automatically"></a>Obter suporte de desfazer automaticamente

Qualquer designer criado no Visual Studio terá suporte a desfazer automático e completo se, o designer:

- Usa uma <xref:System.Windows.Forms.Control> classe baseada em sua interface do usuário.

- Emprega a geração de código baseado em CodeDOM padrão e o sistema de análise para a geração e persistência de código.

   Para obter mais informações sobre como trabalhar com o suporte a CodeDOM do Visual Studio, consulte [geração e compilação de código-fonte dinâmico](/dotnet/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation).

## <a name="when-to-use-explicit-designer-undo-support"></a>Quando usar o suporte de desfazer do designer explícito
 Os designers devem fornecer seu próprio gerenciamento de desfazer se usarem uma interface gráfica do usuário, conhecida como adaptador de exibição, diferente daquele fornecido pelo <xref:System.Windows.Forms.Control> .

 Um exemplo disso pode ser a criação de um produto com uma interface de design gráfico baseada na Web em vez de uma interface gráfica baseada em .NET Framework.

 Nesses casos, seria necessário registrar esse adaptador de exibição com o Visual Studio usando <xref:Microsoft.VisualStudio.Shell.Design.ProvideViewAdapterAttribute> e fornecer gerenciamento de desfazer explícito.

 Os designers precisam fornecer suporte a CodeDOM e persistência se não usarem o modelo de geração de código do Visual Studio fornecido no <xref:System.CodeDom> espaço de nome.

## <a name="undo-support-features-of-the-designer"></a>Desfazer recursos de suporte do designer
 O SDK do ambiente fornece implementações padrão de interfaces necessárias para fornecer suporte de desfazer que pode ser usado por designers que não usam <xref:System.Windows.Forms.Control> classes baseadas em suas interfaces de usuário ou o modelo CodeDOM e persistência padrão.

 A <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> classe deriva da <xref:System.ComponentModel.Design.UndoEngine> classe .NET Framework usando uma implementação da <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> classe para gerenciar operações de desfazer.

 O Visual Studio fornece o seguinte recurso para o designer desfazer:

- Funcionalidade de desfazer vinculada em vários designers.

- As unidades filhas dentro de um designer podem interagir com seus pais implementando <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> e <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> em <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> .

O SDK do ambiente fornece suporte a CodeDOM e persistência fornecendo:

- <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> como uma implementação do <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

- Um <xref:System.ComponentModel.Design.IComponentChangeService> fornecido pelo host de design do Visual Studio.

## <a name="use-the-environment-sdk-features-to-supply-undo-support"></a>Usar os recursos do SDK do ambiente para fornecer suporte de desfazer

Para obter o suporte de desfazer, um objeto que implementa um designer deve instanciar e inicializar uma instância da <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> classe com uma <xref:System.IServiceProvider> implementação válida. Essa <xref:System.IServiceProvider> classe deve fornecer os seguintes serviços:

- <xref:System.ComponentModel.Design.IDesignerHost>.

- <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

   Os designers que usam a serialização do CodeDOM do Visual Studio podem optar <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> pelo uso fornecido com o [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] como sua implementação do <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> .

   Nesse caso, a <xref:System.IServiceProvider> classe fornecida para o <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> Construtor deve retornar esse objeto como uma implementação da <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> classe.

- <xref:System.ComponentModel.Design.IComponentChangeService>

   Os designers que usam o padrão <xref:System.ComponentModel.Design.DesignSurface> fornecido pelo host de design do Visual Studio têm a garantia de ter uma implementação padrão da <xref:System.ComponentModel.Design.IComponentChangeService> classe.

Os designers que implementam um <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> mecanismo de desfazer baseado controlam automaticamente as alterações se:

- As alterações de propriedade são feitas por meio do <xref:System.ComponentModel.TypeDescriptor> objeto.

- <xref:System.ComponentModel.Design.IComponentChangeService> os eventos são gerados manualmente quando uma alteração desfeita é confirmada.

- A modificação no designer foi criada no contexto de um <xref:System.ComponentModel.Design.DesignerTransaction> .

- O designer opta por criar explicitamente unidades de desfazer usando a unidade de desfazer padrão fornecida por uma implementação <xref:System.ComponentModel.Design.UndoEngine.UndoUnit> ou a implementação específica do Visual Studio <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> , que deriva de <xref:System.ComponentModel.Design.UndoEngine.UndoUnit> e também fornece uma implementação de <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> e <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> .

## <a name="see-also"></a>Confira também

- <xref:System.ComponentModel.Design.UndoEngine>
- <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>
- [Estender suporte Design-Time](/previous-versions/37899azc(v=vs.140))
