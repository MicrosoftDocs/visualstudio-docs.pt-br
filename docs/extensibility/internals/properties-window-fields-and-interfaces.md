---
title: Campos e interfaces da janela Propriedades | Microsoft Docs
description: Saiba mais sobre a seleção que determina quais informações são exibidas no janela Propriedades com base na janela que tem o foco no Visual Studio IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window, fields and interfaces
ms.assetid: 0328f0e5-2380-4a7a-a872-b547cb775050
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7a74e82480d1a4c71179c0e0b0671bac4ae97191
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899622"
---
# <a name="properties-window-fields-and-interfaces"></a>Interfaces e campos da janela Propriedades
O modelo para seleção para determinar quais  informações são exibidas na janela Propriedades baseia-se na janela que tem o foco no IDE. Cada janela e objeto dentro da janela selecionada podem ter seu objeto de contexto de seleção pressionado para o contexto de seleção global. O ambiente atualiza o contexto de seleção global com valores de um quadro de janela quando essa janela tem o foco. Quando o foco muda, o contexto de seleção também é.

## <a name="tracking-selection-in-the-ide"></a>Seleção de acompanhamento no IDE
 O quadro de janela ou site, pertencente ao IDE, tem um serviço chamado <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> . As etapas **a** seguir mostram como uma alteração em uma seleção, causada pelo usuário alterando o foco para outra janela aberta ou selecionando um item de projeto diferente no Gerenciador de Soluções , é implementada para alterar o conteúdo exibido na janela **Propriedades.**

1. O objeto criado pelo VSPackage que está na janela selecionada chama <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> para <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> invocar <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> .

2. O contêiner de seleção, fornecido pela janela selecionada, cria seu <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> próprio objeto. Quando a seleção é muda, o VSPackage chama para notificar todos os ouvintes no ambiente, incluindo a janela <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> Propriedades, da  alteração. Ele também fornece acesso a informações de hierarquia e de item relacionadas à nova seleção.

3. Chamar <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> e passar os itens de hierarquia selecionados no parâmetro preenche o objeto `VSHPROPID_BrowseObject` <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> .

4. Um objeto derivado da [Interface IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) é retornado para [__VSHPROPID. VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>) para o item solicitado e o ambiente o envolve em um <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> (consulte a etapa a seguir). Se a chamada falhar, o ambiente fará uma segunda chamada para , passando a ele o `IVsHierarchy::GetProperty` contêiner de [seleção __VSHPROPID. VSHPROPID_SelContainer](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>) que o item de hierarquia ou itens fornecem.

    Seu projeto VSPackage não cria porque o VSPackage da janela fornecida pelo ambiente que o implementa (por exemplo, Gerenciador de Soluções ) constrói em <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> seu  <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> nome.

5. O ambiente invoca os métodos de para obter os objetos com base na <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> interface para preencher a janela `IDispatch` Propriedades. 

   Quando um valor na **janela Propriedades** é alterado, os VSPackages implementam e `IVsTrackSelectionEx::OnElementValueChangeEx` `IVsTrackSelectionEx::OnSelectionChangeEx` relatam a alteração ao valor do elemento. Em seguida, o ambiente invoca <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ou para manter as informações <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> exibidas na janela **Propriedades** sincronizadas com os valores de propriedade. Para obter mais informações, consulte [Atualizando valores de propriedade na janela Propriedades](#updating-property-values-in-the-properties-window).

   Além de selecionar um item de projeto diferente no **Gerenciador de Soluções** para exibir propriedades relacionadas a esse item, você também pode escolher um objeto diferente de dentro de um formulário ou janela de documento usando a listada disponível na **janela Propriedades.** Para obter mais informações, consulte [Lista de objetos da janela Propriedades](../../extensibility/internals/properties-window-object-list.md).

   Você pode alterar a maneira como  as informações são exibidas na grade da janela Propriedades de ordem alfabética para categórica e, se disponível, você também pode abrir uma página de propriedades para um objeto selecionado clicando nos botões apropriados na janela **Propriedades.** Para obter mais informações, consulte [Botões da janela Propriedades](../../extensibility/internals/properties-window-buttons.md) e Páginas de [Propriedades](../../extensibility/internals/property-pages.md).

   Por fim, a parte inferior **da janela Propriedades** também contém uma descrição do campo selecionado na grade **janela** Propriedades. Para obter mais informações, consulte [Getting Field Descriptions from the Properties Window](#getting-field-descriptions-from-the-properties-window).

## <a name="updating-property-values-in-the-properties-window"></a><a name="updating-property-values-in-the-properties-window"></a> Atualizando valores de propriedade na janela Propriedades
Há duas maneiras de manter a janela **Propriedades** em sincronia com as alterações de valor da propriedade. A primeira é chamar a interface , que fornece acesso à funcionalidade básica de janelas, incluindo o acesso e a criação de janelas de ferramentas e documentos fornecidas <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> pelo ambiente. As etapas a seguir descrevem esse processo de sincronização.

### <a name="updating-property-values-using-ivsuishell"></a>Atualizando valores de propriedade usando IVsUIShell

#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>Para atualizar valores de propriedade usando a interface IVsUIShell

1. Chame (por meio do serviço) sempre que <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> o VSPackages, projetos ou editores precisar criar ou enumerar janelas de documentos ou <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> ferramentas.

2. Implemente para manter a janela Propriedades em sincronia com as alterações de propriedade de um projeto (ou qualquer outro objeto selecionado que está sendo navegado pela janela Propriedades) sem implementar e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A> disparar   <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A> eventos.

3. Implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> os métodos e para estabelecer e <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> desabilitar, respectivamente, a <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> notificação do cliente de eventos de hierarquia sem exigir que a hierarquia implemente .

### <a name="updating-property-values-using-iconnection"></a>Atualizando valores de propriedade usando IConnection
 A segunda maneira  de manter a janela Propriedades em sincronia com as alterações de valor da propriedade é implementar no objeto conectável para indicar a existência das `IConnection` interfaces de saída. Se você quiser localizar o nome da propriedade, derive seu objeto de <xref:System.ComponentModel.ICustomTypeDescriptor> . A <xref:System.ComponentModel.ICustomTypeDescriptor> implementação pode modificar os descritores de propriedade que ela retorna e alterar o nome de uma propriedade. Para localizar a descrição, crie um atributo que deriva de <xref:System.ComponentModel.DescriptionAttribute> e substitua a propriedade Description.

#### <a name="considerations-in-implementing-the-iconnection-interface"></a>Considerações sobre como implementar a interface IConnection

1. `IConnection` fornece acesso a um sub-objeto de enumerador com a <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface . Ele também fornece acesso a todos os subpro objetos do ponto de conexão, cada um dos quais implementa a <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> interface .

2. Qualquer objeto browse é responsável por implementar um <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> evento. A **janela** Propriedades orientará o conjunto de eventos por meio de `IConnection` .

3. Um ponto de conexão controla quantas conexões (uma ou mais) ele permite em sua implementação de <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> . Um ponto de conexão que permite que apenas uma interface possa retornar <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> do <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> método .

4. Um cliente pode chamar a `IConnection` interface para obter acesso a um sub-objeto enumerador com a interface <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> . A <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> interface pode ser chamada para enumerar pontos de conexão para cada ID de interface de saída (IID).

5. `IConnection` também pode ser chamado para obter acesso a sub-objetos de ponto de conexão com <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> a interface para cada IID de saída. Por meio da interface , um cliente inicia ou encerra um loop de consultoria com o objeto <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> conectável e a própria sincronização do cliente. O cliente também pode chamar a interface para obter um objeto enumerador com a interface para enumerar as <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections> conexões que ele conhece.

## <a name="getting-field-descriptions-from-the-properties-window"></a><a name="getting-field-descriptions-from-the-properties-window"></a> Obter descrições de campo da janela Propriedades
Na parte inferior da janela **Propriedades,** uma área de descrição exibe informações relacionadas ao campo de propriedade selecionado. Este recurso permanece ligado por padrão. Se você quiser ocultar o campo de descrição, clique com o botão direito do mouse **na janela Propriedades** e clique em **Descrição**. Isso também remove a marca de seleção ao lado do título **Descrição** na janela do menu. Você pode exibir o campo novamente seguindo as mesmas etapas para alternar a **Descrição** novamente.

 As informações no campo de descrição vêm de <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> . Cada método, interface, coclasse e assim por diante pode ter um atributo não localizado `helpstring` na biblioteca de tipos. A **janela Propriedades** recupera a cadeia de caracteres de <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo.GetDocumentation%2A> .

### <a name="to-specify-localized-help-strings"></a>Para especificar cadeias de caracteres de ajuda localizadas

1. Adicione o `helpstringdll` atributo à instrução de biblioteca na biblioteca de tipos ( `typelib` ).

   > [!NOTE]
   > Esta etapa será opcional se a biblioteca de tipos estiver em um arquivo de biblioteca de objetos (.olb).

2. `helpstringcontext`Especifique atributos para as cadeias de caracteres. Você também pode especificar `helpstring` atributos.

    Esses atributos são distintos dos atributos e , que estão contidos nos tópicos reais da Ajuda do `helpfile` `helpcontext` arquivo .chm.

   Para recuperar as informações de descrição a serem  exibidas para o nome da propriedade realçada, a janela Propriedades chama a propriedade selecionada, especificando o atributo desejado para a cadeia de caracteres <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetDocumentation2%2A> de `lcid` saída. Internamente, localiza o .dll especificado no atributo e chama nesse arquivo .dll com <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2> o contexto e o atributo `helpstringdll` `DLLGetDocumentation` `lcid` especificados.

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

 A `DLLGetDocumentation` função deve ser uma exportação definida no arquivo .def para a DLL.

 Internamente, um arquivo .olb é criado, que é, na verdade, uma DLL. Essa DLL contém um recurso, o arquivo de biblioteca de tipos (.tlb) e uma função exportada, `DLLGetDocumentation` .

 No caso de arquivos .olb, o atributo é opcional porque é o mesmo arquivo que contém o próprio arquivo `helpstringdll` .tlb.

 Para obter cadeias de caracteres para aparecer no painel **Descrições,** portanto, o mínimo que você precisa fazer é especificar o atributo `helpstring` na biblioteca de tipos. Se você quiser que essas cadeias de caracteres sejam localizadas, especifique o atributo `helpstringdll` (opcional) e `helpstringcontext` o atributo (obrigatório) e implemente `DLLGetDocumentation` .

 Não há interfaces adicionais que precisam ser implementadas ao obter informações localizadas por meio do atributo idl `helpstringcontext` e `DLLGetDocumentation` .

 Outra maneira de obter o nome localizado e a descrição de uma propriedade é implementando <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.GetLocalizedPropertyInfo%2A> . Para obter mais informações relacionadas à implementação desse método, consulte Interfaces e [campos de janela de propriedades.](../../extensibility/internals/properties-window-fields-and-interfaces.md)

## <a name="see-also"></a>Confira também

- [Estendendo propriedades](../../extensibility/internals/extending-properties.md)
