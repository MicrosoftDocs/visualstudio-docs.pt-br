---
title: Atualizando valores de propriedade na janela Propriedades | Microsoft Docs
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
- Properties window, updating property values
- property values, updating in Properties window
ms.assetid: 9358e8c3-b9d2-4fd4-aaab-cf48d1526db4
caps.latest.revision: 9
manager: douge
ms.openlocfilehash: 8db48e1f746afa8f8f219935555815587ce5823c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49290479"
---
# <a name="updating-property-values-in-the-properties-window"></a>Atualizando valores de propriedade na janela Propriedades
Há duas maneiras de manter o **propriedades** janela em sincronia com o valor da propriedade muda. A primeira é chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface, que fornece acesso à funcionalidade de janelas básicas, incluindo acesso a e criação de janelas de documentos e de ferramentas fornecidas pelo ambiente. As etapas a seguir descrevem esse processo de sincronização.  
  
## <a name="updating-property-values-using-ivsuishell"></a>Atualizando valores de propriedade usando IVsUIShell  
  
#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>Para atualizar os valores de propriedade usando a interface IVsUIShell  
  
1.  Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> (por meio de <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> service) sempre que esse VSPackages, projetos, ou editores precisam criar ou enumerar as janelas de ferramenta ou documento.  
  
2.  Implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A> para manter o **propriedades** janela em sincronia com as alterações de propriedade para um projeto (ou qualquer outro objeto selecionado que está sendo procurado pela **propriedades** janela) sem implementar <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> e o disparo <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A> eventos.  
  
3.  Implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> métodos <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> para estabelecer e desabilitar, respectivamente, a notificação de cliente de eventos de hierarquia sem a necessidade de hierarquia para implementar <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>.  
  
## <a name="updating-property-values-using-iconnection"></a>Atualizando valores de propriedade usando IConnection  
 A segunda maneira de manter o **propriedades** janela em sincronia com alterações de valor da propriedade é implementar `IConnection` no objeto conectável para indicar a existência de interfaces de saída. Se você deseja localizar o nome da propriedade, derive seu objeto de <xref:System.ComponentModel.ICustomTypeDescriptor>. O <xref:System.ComponentModel.ICustomTypeDescriptor> implementação pode modificar os descritores de propriedade, ele retorna e altere o nome de uma propriedade. Para localizar a descrição, criar um atributo que deriva de <xref:System.ComponentModel.DescriptionAttribute> e substitua a propriedade de descrição.  
  
#### <a name="considerations-in-implementing-the-iconnection-interface"></a>Considerações na implementação da interface de IConnection  
  
1.  `IConnection` fornece acesso a um objeto de enumerador subdiretório com o <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface. Ele também fornece acesso a todos os os conexão ponto subobjetos, cada um dos que implementa o <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface.  
  
2.  Qualquer objeto procurado é responsável por implementar um <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> eventos. O **propriedades** janela informará para o evento definido por meio de `IConnection`.  
  
3.  Um ponto de conexão controla quantas conexões (um ou mais) permite em sua implementação de <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A>. Um ponto de conexão que permite que apenas uma interface pode retornar <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> do <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> método.  
  
4.  Um cliente pode chamar o `IConnection` interface para obter acesso a um objeto de enumerador subdiretório com o <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface. O <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface, em seguida, pode ser chamado para enumerar os pontos de conexão para cada interface de saída IID (ID).  
  
5.  `IConnection` também pode ser chamado para obter acesso a objetos de subpropriedades de ponto de conexão com o <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface para cada IID de saída. Por meio de <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface, um cliente inicia ou Finaliza um loop de consultoria com o objeto conectável e a sincronização do cliente. O cliente também pode chamar o <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface para obter um objeto de enumerador com o <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections> interface para enumerar as conexões que ele conhece.  
  
## <a name="see-also"></a>Consulte também  
 [Anunciando a seleção da janela de propriedades de controle](../misc/announcing-property-window-selection-tracking.md)   
 [Estender as propriedades](../extensibility/internals/extending-properties.md)