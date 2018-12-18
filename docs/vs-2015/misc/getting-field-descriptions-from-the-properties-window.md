---
title: Obtendo descrições dos campos na janela Propriedades | Microsoft Docs
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
- Properties window, field descriptions
ms.assetid: 7d92bb6a-b9b9-4cd8-99e9-b5ee129b52a3
caps.latest.revision: 9
manager: douge
ms.openlocfilehash: fc5d2c8553ccdb6c554f9a8364e9fd21eaa324d1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49814786"
---
# <a name="getting-field-descriptions-from-the-properties-window"></a>Obtendo descrições dos campos na janela Propriedades
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
  
```  
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
  
 Outra maneira de obter o nome localizado e a descrição de uma propriedade é implementando <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.GetLocalizedPropertyInfo%2A>. Para obter mais informações relacionadas à implementação desse método, consulte [campos da janela Propriedades e Interfaces](../extensibility/internals/properties-window-fields-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>   
 [Interfaces e campos da janela Propriedades](../extensibility/internals/properties-window-fields-and-interfaces.md)   
 [Estendendo propriedades](../extensibility/internals/extending-properties.md)   
 [helpstringdll](http://msdn.microsoft.com/library/121271fa-f061-492b-b87f-bbfcf4b02e7b)   
 [HelpString](http://msdn.microsoft.com/library/0401e905-a63e-4fad-98d0-d1efea111966)   
 [helpstringcontext](http://msdn.microsoft.com/library/d4cd135e-d91c-4aa3-9353-8aeb096f52cf)   
 [HelpContext](http://msdn.microsoft.com/library/6fbb022d-a4b7-4989-a02f-7f18a9b0ad96)   
 [Arquivo de ajuda](http://msdn.microsoft.com/library/d75161c1-1363-4019-ae09-e7e3b8a3971e)   
 [lcid](http://msdn.microsoft.com/library/7f248c69-ee1c-42c3-9411-39cf27c9f43d)