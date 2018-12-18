---
title: Gerenciando a caixa de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Toolbox [Visual Studio SDK], automatic tab selection
- Toolbox [Visual Studio SDK], managing
ms.assetid: 3b052047-f6db-46dd-b3bf-da1c348ee410
caps.latest.revision: 33
manager: douge
ms.openlocfilehash: 227001e827057ffab4c851a985f7e36afaf0f351
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49873416"
---
# <a name="managing-the-toolbox"></a>Gerenciando a caixa de ferramentas
O [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] permite que um VSPackage, como um editor ou designer, para gerenciar a associação e a aparência do **caixa de ferramentas**.  
  
 Além disso, o **caixa de ferramentas** em si pode ser gerenciada usando a automação. Para obter mais informações sobre como gerenciar uma caixa de ferramentas por meio da automação, consulte [como: controle de caixa de ferramentas](http://msdn.microsoft.com/library/c9d8a18a-d2bc-43d4-a803-601bfc6a6599).  
  
## <a name="automatic-toolbox-tab-selection"></a>Seleção automática de caixa de ferramentas da guia  
 Um determinado **caixa de ferramentas** guia ou categoria pode ser automaticamente feita Active Directory com base em qual editor ou designer está ativo no momento. Por exemplo, se um designer de formulários estiver ativado, você pode querer a **todos os Windows Forms** guia selecionada.  
  
 Esse suporte é limitado a editores e designers que exigem:  
  
1.  A implementação de um objeto de fábrica para fornecer instâncias do editor ou designer. Para obter mais informações sobre como implementar um designer ou editor de objeto de fábrica, consulte [fábricas](../extensibility/editor-factories.md).  
  
2.  Registro do guia da caixa de ferramentas é ativado automaticamente se o editor ou designer estiver presente.  
  
## <a name="controlling-the-toolbox"></a>Controlando a caixa de ferramentas  
 Complementando o suporte de automação, o [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] fornece as seguintes interfaces para fornecer os VSPackages maior controle sobre como o **caixa de ferramentas** é gerenciado.  
  
|Interface|Descrição|  
|---------------|-----------------|  
|<xref:System.Drawing.Design.IToolboxService>|Permite que os aplicativos gerenciar, adicionar e remover <xref:System.Drawing.Design.ToolboxItem> objetos do **caixa de ferramentas**. Também permite a configuração de aparência e **caixa de ferramentas** categorias.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>|Permite que os aplicativos gerenciar, adicionar e remover baseada no Active Directory **caixa de ferramentas** controles, bem como configure **caixa de ferramentas** categorias e aparência.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3>|Estende a funcionalidade encontrada em <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> , fornecendo suporte completo para persistência e localização.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox4>||  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox5>||  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox6>||  
  
 Há vários pontos importantes para ter em mente ao trabalhar com essas interfaces:  
  
- <xref:System.Drawing.Design.IToolboxService> está disponível somente para VSPackages com base em estrutura de pacote gerenciado.  
  
- Controles não podem ser adicionados diretamente para o **caixa de ferramentas** usando <xref:System.Drawing.Design.IToolboxService>.  
  
- Um VSPackage deverá usar <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> para adicionar controles ou hospedar o controle em um controle wrapper derivado de <xref:System.Windows.Forms.AxHost>.  
  
   O Visual Studio fornece o `Aximp.exe` de ferramentas para automatizar o encapsulamento de um controle ActiveX em um controle derivado de <xref:System.Windows.Forms.AxHost>. Para obter mais informações, consulte [Aximp.exe (Windows Forms ActiveX Control Importer)](http://msdn.microsoft.com/library/482c0d83-7144-4497-b626-87d2351b78d0).  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox>, <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>, e <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> estão COM base em interfaces disponíveis por meio de assemblies de interoperabilidade.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> deriva de <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox> e implementa todos os seus métodos.  
  
   Objetos apenas obter uma instância do <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> não é derivado de <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> e implementa seus métodos.  
  
   Objetos que precisam de funcionalidade em ambas as interfaces devem obter as instâncias de ambas as interfaces do ambiente.  
  
- Ao trabalhar com <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3>, informações sobre os nomes canônicos (não localizado) das guias são tratadas pelos <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3.GetIDOfTab%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3.SetIDOfTab%2A> métodos.  
  
- Ao usar <xref:System.Drawing.Design.IToolboxService>, ele cabe ao implementador para gerenciar informações localizadas, como nomes de categorias.  
  
  Usar o mecanismo de configurações para habilitar os usuários salvem **caixa de ferramentas** configurações acessadas por usuários da **configurações de importação/exportação** comando, encontrado o IDE **ferramentas** menu. Para obter mais informações sobre como usar as configurações, consulte [opções e configurações do usuário estendendo](../extensibility/extending-user-settings-and-options.md).  
  
## <a name="see-also"></a>Consulte também  
 [Estendendo a caixa de ferramentas](../misc/extending-the-toolbox.md)