---
title: Adaptando um código herdado para o Editor | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - adapters
ms.assetid: a208d38e-9bea-41c9-9fe2-38bd86a359cb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e04ae5484b6c1fd5bcc56154c6cec23334e7ef8d
ms.sourcegitcommit: 8cdc6e2ad2341f34bd6b02859a7c975daa0c9320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53307785"
---
# <a name="adapt-legacy-code-to-the-editor"></a>Adaptar o código herdado para o editor
Editor do Visual Studio tem muitos recursos que você pode acessar de componentes de código existentes. As instruções a seguir mostram como adaptar um componente não MEF, por exemplo, um VSPackage, para consumir a funcionalidade do editor. As instruções também mostram como usar adaptadores para obter os serviços do editor no código gerenciado e não gerenciado.  
  
## <a name="editor-adapters"></a>Adaptadores do Editor  
 Adaptadores do Editor, ou shims, são invólucros para objetos de editor que também expõe as classes e interfaces no <xref:Microsoft.VisualStudio.TextManager.Interop> API. Você pode usar os adaptadores para mover entre os serviços não de editor, por exemplo, comandos de shell do Visual Studio e serviços do editor. (Isso é como o editor no momento está hospedado no Visual Studio.) Adaptadores também habilitar extensões herdadas de serviço de editor e linguagem funcione corretamente no Visual Studio.  
  
## <a name="use-editor-adapters"></a>Use adaptadores de editor  
 O <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> fornece métodos que alternar entre as novas interfaces de editor e as interfaces herdadas e também métodos que criam os adaptadores.  
  
 Se você estiver usando esse serviço em uma parte do componente MEF, você pode importar o serviço da seguinte maneira.  
  
```  
[Import(typeof(IVsEditorAdaptersFactoryService))]  
internal IVsEditorAdaptersFactoryService editorFactory;  
```  
  
 Se você quiser usar esse serviço em um componente não MEF, siga as instruções na seção "Usando o Visual Studio Editor serviços em um MEF não componente" mais adiante neste tópico.  
  
## <a name="switch-between-the-new-editor-api-and-the-legacy-api"></a>Alternar entre a nova API de editor e a API herdada  
 Use os seguintes métodos para alternar entre um objeto de editor e uma interface herdada.  
  
|Método|Conversão|  
|------------|----------------|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetBufferAdapter%2A>|Converte um <xref:Microsoft.VisualStudio.Text.ITextBuffer> em um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetDataBuffer%2A>|Converte um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> em um <xref:Microsoft.VisualStudio.Text.ITextBuffer>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetDocumentBuffer%2A>|Converte um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> em um <xref:Microsoft.VisualStudio.Text.ITextBuffer>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetViewAdapter%2A>|Converte um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> em um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.GetWpfTextView%2A>|Converte um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> em um <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>.|  
  
## <a name="create-adapters"></a>Criar adaptadores  
 Use os métodos a seguir para criar adaptadores para interfaces legadas.  
  
|Método|Conversão|  
|------------|----------------|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsCodeWindowAdapter%2A>|Cria um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferAdapter%2A>|Cria uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> para um <xref:Microsoft.VisualStudio.Utilities.IContentType>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferAdapter%2A>|Cria um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextBufferCoordinatorAdapter%2A>|Cria um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextViewAdapter%2A>|Cria um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextViewRoleSet>.|  
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService.CreateVsTextViewAdapter%2A>|Cria um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>.|  
  
## <a name="creating-adapters-in-unmanaged-code"></a>Criando adaptadores em código não gerenciado  
 Todas as classes de adaptadores são registradas como local conjunta pode ser criado e pode ser instanciado usando o `VsLocalCreateInstance()` função.  
  
 Todos os adaptadores são criados usando os GUIDs que são definidos na *vsshlids.h* arquivo na *\..\VisualStudioIntegration\Common\Inc\\* pasta do SDK do Visual Studio instalação. Para criar uma instância de VsTextBufferAdapter, use o código a seguir.  
  
```  
IVsTextBuffer *pBuf = NULL;  
VsLocalCreateInstance(CLSID_VsTextBuffer, NULL, CLSCTX_INPROC_SERVER, IID_IVsTextBuffer, (void**)&pBuf);  
```  
  
## <a name="create-adapters-in-managed-code"></a>Criar adaptadores em código gerenciado  
 No código gerenciado, você pode criar conjuntamente os adaptadores da mesma maneira que descrita para código não gerenciado. Você também pode usar um serviço MEF que permite criar e interagir com os adaptadores. Dessa maneira de obter um adaptador permite que um controle mais refinado do que você tem ao criar conjuntamente.  
  
### <a name="to-create-an-adapter-for-ivstextview"></a>Para criar um adaptador para IVsTextView  
  
1.  Adicione uma referência ao *Microsoft.VisualStudio.Editor.dll*. Certifique-se de que `CopyLocal` é definido como `false`.  
  
2.  Criar uma instância de <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>, da seguinte maneira.  
  
    ```  
    using Microsoft.VisualStudio.Editor;  
    ...  
    IVsEditorAdaptersFactoryService adapterFactoryService = ComponentModel.GetService<IVsEditorAdaptersFactoryService>();  
    ```  
  
3.  Chame o método `CreateX()`.  
  
    ```  
    adapterFactoryService.CreateTextViewAdapter(textView);  
    ```  
  
## <a name="use-the-visual-studio-editor-directly-from-unmanaged-code"></a>Use o editor do Visual Studio diretamente do código não gerenciado  
 O namespace Microsoft.VisualStudio.Platform.VSEditor e o namespace Microsoft.VisualStudio.Platform.VSEditor.Interop expõem interfaces COM-callable como interfaces IVx *. Por exemplo, a interface Microsoft.VisualStudio.Platform.VSEditor.Interop.IVxTextBuffer é a versão COM do <xref:Microsoft.VisualStudio.Text.ITextBuffer> interface. Do `IVxTextBuffer`, obtenha acesso a instantâneos de buffer, modificam o buffer, escutar eventos de alteração de texto no buffer e criar pontos de controle e intervalos. As etapas a seguir mostram como acessar uma `IVxTextBuffer` de um `IVsTextBuffer`.  
  
### <a name="to-get-an-ivxtextbuffer"></a>Para obter um IVxTextBuffer  
  
1.  As definições para o IVx\* interfaces estão na *VSEditor.h* arquivo o *\..\VisualStudioIntegration\Common\Inc\\* pasta do Visual Studio Instalação do SDK.  
  
2.  O código a seguir cria uma instância de um buffer de texto usando o `IVsUserData->GetData()` método. No código a seguir `pData` é um ponteiro para um `IVsUserData` objeto.  
  
    ```cpp  
    #include <textmgr.h>  
    #include <VSEditor.h>  
    #include <vsshlids.h>  
  
    CComPtr<IVsTextBuffer> pVsTextBuffer;  
    CComPtr<IVsUserData> pData;  
    CComPtr<IVxTextBuffer> pVxBuffer;  
    ...  
    if (SUCCEEDED(pVsTextBuffer->QueryInterface(IID_IVsUserData, &pData))  
    {  
        CComVariant vt;  
        if (SUCCEEDED(pData->GetData(GUID_VxTextBuffer, &vt)) &&  
        (vt.Type == VT_UNKNOWN) && (vt.punkVal != NULL))  
        {  
            vt.punkVal->QueryInterface(IID_IVxTextBuffer, (void**)&pVxBuffer);  
        }  
    }  
    ```  
  
## <a name="use-visual-studio-editor-services-in-a-non-mef-component"></a>Usar serviços do editor do Visual Studio em um componente não MEF  
 Se você tiver um componente de código gerenciado existente que não usa o MEF e você deseja usar os serviços do editor do Visual Studio, você deve adicionar uma referência ao assembly que contém o ComponentModelHost VSPackage e obter seu serviço SComponentModel.  
  
### <a name="to-consume-visual-studio-editor-components-from-a-non-mef-component"></a>Para consumir componentes do editor do Visual Studio de um componente não MEF  
  
1.  Adicione uma referência para o *Microsoft.VisualStudio.ComponentModelHost.dll* assembly na *\..\Common7\IDE\\* pasta de instalação do Visual Studio. Certifique-se de que `CopyLocal` é definido como `false`.  
  
2.  Adicionar uma privada `IComponentModel` membro à classe na qual você deseja usar os serviços do editor do Visual Studio, da seguinte maneira.  
  
    ```  
    using Microsoft.VisualStudio.ComponentModelHost;  
    ....  
    private IComponentModel componentModel;  
    ```  
  
3.  Instancie o modelo de componente no método de inicialização para seu componente.  
  
    ```  
    componentModel =  
     (IComponentModel)Package.GetGlobalService(typeof(SComponentModel));  
    ```  
  
4.  Depois disso, você pode obter qualquer um dos serviços de editor do Visual Studio, chamando o `IComponentModel.GetService<T>()` método para o serviço desejado.  
  
    ```  
    textBufferFactoryService =  
         componentModel.GetService<ITextBufferFactoryService>();     
    ```
