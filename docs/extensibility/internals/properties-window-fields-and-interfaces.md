---
title: Interfaces e campos da janela Propriedades | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, fields and interfaces
ms.assetid: 0328f0e5-2380-4a7a-a872-b547cb775050
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 149c02918ec909c03c1102a5fc0f1643b79fb46d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49883400"
---
# <a name="properties-window-fields-and-interfaces"></a>Interfaces e campos da janela Propriedades
O modelo para a seleção determinar quais informações são exibidas na **propriedades** janela baseia-se na janela que tem o foco no IDE. Cada janela e o objeto dentro da janela selecionada, podem ter seu objeto de contexto de seleção enviados por push para o contexto da seleção global. O ambiente atualiza o contexto da seleção global com valores de um quadro de janela quando essa janela tem o foco. Quando o foco é alterado, portanto, não o contexto da seleção.  
  
## <a name="tracking-selection-in-the-ide"></a>Seleção do controle no IDE  
 O quadro de janela ou site, pertencentes a IDE, tem um serviço chamado <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>. As etapas a seguir mostram como uma alteração em uma seleção, causada pelo usuário alterando o foco para outra janela aberta ou selecionando um item de projeto diferente em **Gerenciador de soluções**, é implementado para alterar o conteúdo exibido na  **Propriedades** janela.  
  
1. O objeto criado pelo VSPackage que é localizado em chamadas a janela selecionada <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> ter <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> invocar <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>.  
  
2. O contêiner de seleção, fornecido pela janela selecionada, cria seu próprio <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> objeto. Quando a seleção é alterada, o VSPackage chama <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> notificar todos os ouvintes no ambiente, incluindo o **propriedades** janela, da alteração. Ele também fornece acesso às informações de hierarquia e de item relacionados à nova seleção.  
  
3. Chamando <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> e passando-os itens da hierarquia selecionada na `VSHPROPID_BrowseObject` parâmetro preenche o <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> objeto.  
  
4. Um objeto derivado de [IDispatch Interface](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) é retornado para <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> para o item solicitado e o ambiente encapsula-o em um <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> (consulte a etapa a seguir). Se a chamada falhar, o ambiente torna uma segunda chamada para `IVsHierarchy::GetProperty`, passando-o contêiner de seleção <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> que forneçam o item de hierarquia ou itens.  
  
    Seu projeto de VSPackage não cria <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> como a janela fornecida pelo ambiente de VSPackage que o implementa (por exemplo, **Gerenciador de soluções**) constrói <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> em seu nome.  
  
5. O ambiente chama os métodos do <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> para obter os objetos com base em de `IDispatch` interface para preencher o **propriedades** janela.  
  
   Quando um valor na **propriedades** janela for alterada, implementar os VSPackages `IVsTrackSelectionEx::OnElementValueChangeEx` e `IVsTrackSelectionEx::OnSelectionChangeEx` para relatar a alteração para o valor do elemento. O ambiente, em seguida, invoca <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ou <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> para manter as informações exibidas na **propriedades** janela sincronizados com os valores de propriedade. Para obter mais informações, consulte [atualizando valores de propriedade na janela propriedades](#updating-property-values-in-the-properties-window).  
  
   Além de selecionar uma opção diferente de item de projeto no **Gerenciador de soluções** para exibir as propriedades relacionadas a esse item, você também pode escolher um objeto diferente de dentro de uma janela de formulário ou documento usando a lista suspensa disponível no **Propriedades** janela. Para obter mais informações, consulte [lista de objetos de janela de propriedades](../../extensibility/internals/properties-window-object-list.md).  
  
   Você pode alterar o modo de exibição de informações na **propriedades** grade da janela de em ordem alfabética em categórica, e, se disponível, você também pode abrir uma página de propriedades para um objeto selecionado clicando nos botões apropriados na  **Propriedades** janela. Para obter mais informações, consulte [botões da janela propriedades](../../extensibility/internals/properties-window-buttons.md) e [páginas de propriedade](../../extensibility/internals/property-pages.md).  
  
   Por fim, a parte inferior da **propriedades** janela também contém uma descrição do campo selecionado na **propriedades** grade da janela. Para obter mais informações, consulte [obtendo descrições do campo da janela propriedades](#getting-field-descriptions-from-the-properties-window).  
  
## <a name="updating-property-values-in-the-properties-window"></a> Atualizando valores de propriedade na janela Propriedades
Há duas maneiras de manter o **propriedades** janela em sincronia com o valor da propriedade muda. A primeira é chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface, que fornece acesso à funcionalidade de janelas básicas, incluindo acesso a e criação de janelas de documentos e de ferramentas fornecidas pelo ambiente. As etapas a seguir descrevem esse processo de sincronização.  
  
### <a name="updating-property-values-using-ivsuishell"></a>Atualizando valores de propriedade usando IVsUIShell  
  
#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>Para atualizar os valores de propriedade usando a interface IVsUIShell  
  
1.  Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> (por meio de <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> service) sempre que esse VSPackages, projetos, ou editores precisam criar ou enumerar as janelas de ferramenta ou documento.  
  
2.  Implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A> para manter o **propriedades** janela em sincronia com as alterações de propriedade para um projeto (ou qualquer outro objeto selecionado que está sendo procurado pela **propriedades** janela) sem implementar <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> e o disparo <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A> eventos.  
  
3.  Implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> métodos <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> para estabelecer e desabilitar, respectivamente, a notificação de cliente de eventos de hierarquia sem a necessidade de hierarquia para implementar <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>.  
  
### <a name="updating-property-values-using-iconnection"></a>Atualizando valores de propriedade usando IConnection  
 A segunda maneira de manter o **propriedades** janela em sincronia com alterações de valor da propriedade é implementar `IConnection` no objeto conectável para indicar a existência de interfaces de saída. Se você deseja localizar o nome da propriedade, derive seu objeto de <xref:System.ComponentModel.ICustomTypeDescriptor>. O <xref:System.ComponentModel.ICustomTypeDescriptor> implementação pode modificar os descritores de propriedade, ele retorna e altere o nome de uma propriedade. Para localizar a descrição, criar um atributo que deriva de <xref:System.ComponentModel.DescriptionAttribute> e substitua a propriedade de descrição.  
  
#### <a name="considerations-in-implementing-the-iconnection-interface"></a>Considerações na implementação da interface de IConnection  
  
1.  `IConnection` fornece acesso a um objeto de enumerador subdiretório com o <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface. Ele também fornece acesso a todos os os conexão ponto subobjetos, cada um dos que implementa o <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface.  
  
2.  Qualquer objeto procurado é responsável por implementar um <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> eventos. O **propriedades** janela informará para o evento definido por meio de `IConnection`.  
  
3.  Um ponto de conexão controla quantas conexões (um ou mais) permite em sua implementação de <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A>. Um ponto de conexão que permite que apenas uma interface pode retornar <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> do <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> método.  
  
4.  Um cliente pode chamar o `IConnection` interface para obter acesso a um objeto de enumerador subdiretório com o <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface. O <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface, em seguida, pode ser chamado para enumerar os pontos de conexão para cada interface de saída IID (ID).  
  
5.  `IConnection` também pode ser chamado para obter acesso a objetos de subpropriedades de ponto de conexão com o <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface para cada IID de saída. Por meio de <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface, um cliente inicia ou Finaliza um loop de consultoria com o objeto conectável e a sincronização do cliente. O cliente também pode chamar o <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface para obter um objeto de enumerador com o <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections> interface para enumerar as conexões que ele conhece.  
  
## <a name="getting-field-descriptions-from-the-properties-window"></a> Obtendo descrições dos campos na janela Propriedades
Na parte inferior a **propriedades** janela, uma área de descrição exibe informações relacionadas ao campo de propriedade selecionada. Esse recurso é ativado por padrão. Se você quiser ocultar o campo de descrição, clique com botão direito do **propriedades** janela e clique em **descrição**. Isso também remove a marca de seleção ao lado de **descrição** título na janela de menu. Você pode exibir o campo novamente, seguindo as mesmas etapas para ativar/desativar **descrição** novamente.  
  
 As informações no campo de descrição é proveniente <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>. Cada método, interface, coclass e assim por diante podem ter um não localizado `helpstring` atributo na biblioteca de tipos. O **propriedades** janela recupera a cadeia de caracteres de <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo.GetDocumentation%2A>.  
  
### <a name="to-specify-localized-help-strings"></a>Para especificar cadeias de caracteres localizada da Ajuda  
  
1. Adicione a `helpstringdll` para a instrução library na biblioteca de tipos de atributo (`typelib`).  
  
   > [!NOTE]
   >  Esta etapa é opcional se a biblioteca de tipos está em um arquivo de biblioteca (. olb) do objeto.  
  
2. Especificar `helpstringcontext` atributos para as cadeias de caracteres. Você também pode especificar `helpstring` atributos.  
  
    Esses atributos são distintos do `helpfile` e `helpcontext` atributos que estão contidos nos tópicos de Ajuda do arquivo. chm real.  
  
   Para recuperar as informações de descrição a ser exibida para o nome da propriedade realçado, o **propriedades** janela chamadas <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetDocumentation2%2A> para a propriedade que está selecionada, especificando o desejado `lcid` de atributo para o cadeia de caracteres de saída. Internamente, <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2> localiza o arquivo. dll especificado na `helpstringdll` atributo e chamadas `DLLGetDocumentation` nesse arquivo. dll com o contexto especificado e `lcid` atributo.  
  
   A assinatura e a implementação de `DLLGetDocumentation` são:  
  
```cpp  
STDAPI DLLGetDocumentation  
(  
   ITypeLib * /* ptlib */,  
   ITypeInfo * /* ptinfo */,  
   LCID /* lcid */,  
   DWORD dwCtx,  
   BSTR * pbstrHelpString  
);  
```  
  
 O `DLLGetDocumentation` função deve ser uma exportação definida no arquivo. def para a DLL.  
  
 Internamente, é criado um arquivo. olb que é, na verdade, uma DLL. Essa DLL contém um recurso, o arquivo de biblioteca (. tlb) de tipo e uma função exportada, `DLLGetDocumentation`.  
  
 No caso de arquivos. olb, o `helpstringdll` atributo é opcional, pois ele é o mesmo arquivo que contém o próprio arquivo. tlb.  
  
 Para obter cadeias de caracteres sejam exibidos na **descrições** painel, portanto, o mínimo que você precisa fazer é especificar o `helpstring` atributo na biblioteca de tipos. Se você quiser que essas cadeias de caracteres a ser localizada, você precisará especificar o `helpstringdll` atributo (opcional) e o `helpstringcontext` atributo (obrigatório) e implementar `DLLGetDocumentation`.  
  
 Não existem interfaces adicionais que precisam ser implementados quando obtendo localizado informações por meio do idl `helpstringcontext` atributo e `DLLGetDocumentation`.  
  
 Outra maneira de obter o nome localizado e a descrição de uma propriedade é implementando <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.GetLocalizedPropertyInfo%2A>. Para obter mais informações relacionadas à implementação desse método, consulte [campos da janela Propriedades e Interfaces](../../extensibility/internals/properties-window-fields-and-interfaces.md).  

## <a name="see-also"></a>Consulte também  
 [Estender as propriedades](../../extensibility/internals/extending-properties.md)