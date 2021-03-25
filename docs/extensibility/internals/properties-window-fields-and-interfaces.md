---
title: Propriedades e interfaces campos de janela | Microsoft Docs
description: Saiba mais sobre a seleção que determina quais informações são exibidas na janela Propriedades com base na janela que tem o foco no IDE do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, fields and interfaces
ms.assetid: 0328f0e5-2380-4a7a-a872-b547cb775050
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9f445d31fe995321ad6ec334a5b6eb93570b8875
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061024"
---
# <a name="properties-window-fields-and-interfaces"></a>Interfaces e campos da janela Propriedades
O modelo de seleção para determinar quais informações são exibidas na janela **Propriedades** baseia-se na janela que tem o foco no IDE. Cada janela e objeto dentro da janela selecionada podem ter seu objeto de contexto de seleção enviado por push para o contexto de seleção global. O ambiente atualiza o contexto de seleção global com valores de um quadro de janela quando essa janela tem o foco. Quando o foco muda, o contexto de seleção é alterado.

## <a name="tracking-selection-in-the-ide"></a>Controlando a seleção no IDE
 O quadro de janela ou site, pertencente ao IDE, tem um serviço chamado <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> . As etapas a seguir mostram como uma alteração em uma seleção, causada pelo usuário que está alterando o foco para outra janela aberta ou selecionando um item de projeto diferente no **Gerenciador de soluções**, é implementada para alterar o conteúdo exibido na janela **Propriedades** .

1. O objeto criado por seu VSPackage que está no local na janela selecionada chama <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> para ter <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> Invoke <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> .

2. O contêiner de seleção, fornecido pela janela selecionada, cria seu próprio <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> objeto. Quando a seleção é alterada, o VSPackage chama <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> para notificar quaisquer ouvintes no ambiente, incluindo a janela **Propriedades** da alteração. Ele também fornece acesso a informações de hierarquia e de item relacionadas à nova seleção.

3. Chamar <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> e passar os itens de hierarquia selecionados no `VSHPROPID_BrowseObject` parâmetro popula o <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> objeto.

4. Um objeto derivado da [interface IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) é retornado para [__VSHPROPID. VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>) para o item solicitado e o ambiente o encapsula em um <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> (consulte a etapa a seguir). Se a chamada falhar, o ambiente fará uma segunda chamada para `IVsHierarchy::GetProperty` , passando-a para o contêiner de seleção [__VSHPROPID. VSHPROPID_SelContainer](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>) que o item de hierarquia ou os itens são fornecidos.

    O projeto VSPackage não cria <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> porque a janela VSPackage fornecida pelo ambiente que a implementa (por exemplo, **Gerenciador de soluções**) constrói <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> em seu nome.

5. O ambiente invoca os métodos de <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> para obter os objetos com base na `IDispatch` interface para preencher a janela **Propriedades** .

   Quando um valor na janela **Propriedades** é alterado, VSPackages implementa `IVsTrackSelectionEx::OnElementValueChangeEx` e `IVsTrackSelectionEx::OnSelectionChangeEx` relata a alteração para o valor do elemento. Em seguida, o ambiente invoca <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ou <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> mantém as informações exibidas na janela **Propriedades** sincronizadas com os valores de propriedade. Para obter mais informações, consulte [atualizando valores de propriedade na janela Propriedades](#updating-property-values-in-the-properties-window).

   Além de selecionar um item de projeto diferente em **Gerenciador de soluções** para exibir as propriedades relacionadas a esse item, você também pode escolher um objeto diferente de dentro de uma janela de formulário ou de documento usando a lista suspensa disponível na janela **Propriedades** . Para obter mais informações, consulte [lista de objetos da janela de propriedades](../../extensibility/internals/properties-window-object-list.md).

   Você pode alterar a maneira como as informações são exibidas na grade da janela **Propriedades** de ordem alfabética para categórica e, se disponíveis, você também pode abrir uma página de propriedades para um objeto selecionado clicando nos botões apropriados na janela **Propriedades** . Para obter mais informações, consulte [botões da janela de propriedades](../../extensibility/internals/properties-window-buttons.md) e páginas de [Propriedades](../../extensibility/internals/property-pages.md).

   Por fim, a parte inferior da janela **Propriedades** também contém uma descrição do campo selecionado na grade da janela **Propriedades** . Para obter mais informações, consulte [obtendo descrições de campo na janela Propriedades](#getting-field-descriptions-from-the-properties-window).

## <a name="updating-property-values-in-the-properties-window"></a><a name="updating-property-values-in-the-properties-window"></a> Atualizando valores de propriedade na janela Propriedades
Há duas maneiras de manter a janela **Propriedades** em sincronia com as alterações no valor da propriedade. A primeira é chamar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> interface, que fornece acesso à funcionalidade básica de janelas, incluindo acesso e criação de ferramentas e janelas de documentos fornecidas pelo ambiente. As etapas a seguir descrevem esse processo de sincronização.

### <a name="updating-property-values-using-ivsuishell"></a>Atualizando valores de propriedade usando IVsUIShell

#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>Para atualizar valores de propriedade usando a interface IVsUIShell

1. Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> (por meio do <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> serviço) sempre que VSPackages, projetos ou editores precisarem criar ou enumerar janelas de ferramentas ou documentos.

2. Implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A> para manter a janela **Propriedades** em sincronia com as alterações de propriedade de um projeto (ou qualquer outro objeto selecionado que esteja sendo navegado pela janela **Propriedades** ) sem implementar <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> e acionar <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A> eventos.

3. Implemente os <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> métodos <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> estabeleça e desabilite, respectivamente, a notificação do cliente de eventos de hierarquia sem exigir que a hierarquia seja implementada <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> .

### <a name="updating-property-values-using-iconnection"></a>Atualizando valores de propriedade usando IConnection
 A segunda maneira de manter a janela **Propriedades** em sincronia com as alterações no valor da propriedade é implementar `IConnection` no objeto connectável para indicar a existência das interfaces de saída. Se você quiser localizar o nome da propriedade, derive o objeto de <xref:System.ComponentModel.ICustomTypeDescriptor> . A <xref:System.ComponentModel.ICustomTypeDescriptor> implementação pode modificar os descritores de propriedade que ele retorna e alterar o nome de uma propriedade. Para localizar a descrição, crie um atributo que deriva de <xref:System.ComponentModel.DescriptionAttribute> e substitua a propriedade Description.

#### <a name="considerations-in-implementing-the-iconnection-interface"></a>Considerações sobre a implementação da interface IConnection

1. `IConnection` fornece acesso a um subobjeto enumerador com a <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface. Ele também fornece acesso a todos os subobjetos de ponto de conexão, cada um implementando a <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface.

2. Qualquer objeto de procura é responsável pela implementação de um <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> evento. A janela **Propriedades** aconselhará o conjunto de eventos por meio de `IConnection` .

3. Um ponto de conexão controla quantas conexões (um ou mais) ela permite em sua implementação de <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> . Um ponto de conexão que permite que apenas uma interface possa retornar <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> do <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> método.

4. Um cliente pode chamar a `IConnection` interface para obter acesso a um subobjeto do enumerador com a <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface. A <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface pode então ser chamada para enumerar pontos de conexão para cada ID de interface de saída (IID).

5. `IConnection` também pode ser chamado para obter acesso a subobjetos de ponto de conexão com a <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface para cada IID de saída. Por meio da <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface, um cliente inicia ou termina um loop de consultoria com o objeto que pôde ser conectado e a própria sincronização do cliente. O cliente também pode chamar a <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface para obter um objeto de enumerador com a <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections> interface para enumerar as conexões que ele conhece.

## <a name="getting-field-descriptions-from-the-properties-window"></a><a name="getting-field-descriptions-from-the-properties-window"></a> Obtendo descrições de campo na janela Propriedades
Na parte inferior da janela **Propriedades** , uma área de descrição exibe informações relacionadas ao campo de propriedade selecionado. Este recurso permanece ligado por padrão. Se você quiser ocultar o campo Descrição, clique com o botão direito do mouse na janela **Propriedades** e clique em **Descrição**. Isso também remove a marca de seleção ao lado do título da **Descrição** na janela do menu. Você pode exibir o campo novamente seguindo as mesmas etapas para alternar a **Descrição** novamente.

 As informações no campo Descrição vêm de <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> . Cada método, interface, coclasse e assim por diante pode ter um atributo não local `helpstring` na biblioteca de tipos. A janela **Propriedades** recupera a cadeia de caracteres de <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo.GetDocumentation%2A> .

### <a name="to-specify-localized-help-strings"></a>Para especificar cadeias de caracteres de ajuda localizadas

1. Adicione o `helpstringdll` atributo à instrução da biblioteca na biblioteca de tipos ( `typelib` ).

   > [!NOTE]
   > Esta etapa será opcional se a biblioteca de tipos estiver em um arquivo de biblioteca de objetos (. olb).

2. Especifique `helpstringcontext` atributos para as cadeias de caracteres. Você também pode especificar `helpstring` atributos.

    Esses atributos são distintos dos `helpfile` `helpcontext` atributos e, que estão contidos nos tópicos de ajuda de arquivo. chm reais.

   Para recuperar as informações de descrição a serem exibidas para o nome da propriedade realçado, a janela **Propriedades** chama <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetDocumentation2%2A> a propriedade selecionada, especificando o `lcid` atributo desejado para a cadeia de caracteres de saída. Internamente, <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2> localiza o arquivo. dll especificado no `helpstringdll` atributo e chama `DLLGetDocumentation` esse arquivo. dll com o contexto e o atributo especificados `lcid` .

   A assinatura e a implementação do `DLLGetDocumentation` são:

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

 A `DLLGetDocumentation` função deve ser uma exportação definida no arquivo. def para a dll.

 Internamente, um arquivo. olb é criado, o que é, na verdade, uma DLL. Essa DLL contém um recurso, o arquivo de biblioteca de tipos (. tlb) e uma função exportada, `DLLGetDocumentation` .

 No caso de arquivos. olb, o `helpstringdll` atributo é opcional porque ele é o mesmo arquivo que contém o próprio arquivo. tlb.

 Para que as cadeias de caracteres sejam exibidas no painel de **descrições** , portanto, o mínimo que você precisa fazer é especificar o `helpstring` atributo na biblioteca de tipos. Se desejar que essas cadeias de caracteres sejam localizadas, você precisará especificar o `helpstringdll` atributo (opcional) e o `helpstringcontext` atributo (obrigatório) e implementá-los `DLLGetDocumentation` .

 Não há interfaces adicionais que precisam ser implementadas ao obter informações localizadas por meio do `helpstringcontext` atributo de IDL e `DLLGetDocumentation` .

 Outra maneira de obter o nome localizado e a descrição de uma propriedade é implementando <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.GetLocalizedPropertyInfo%2A> . Para obter mais informações relacionadas à implementação desse método, consulte [Propriedades e campos da janela de propriedade](../../extensibility/internals/properties-window-fields-and-interfaces.md).

## <a name="see-also"></a>Confira também

- [Estendendo propriedades](../../extensibility/internals/extending-properties.md)
