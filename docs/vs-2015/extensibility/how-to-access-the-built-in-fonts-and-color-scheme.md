---
title: 'Como: acessar o esquema de cores e fontes internas | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- fonts, accessing built-in
- font and color control [Visual Studio SDK], categories
- colors, accessing built-in schemes
ms.assetid: 6905845e-e88e-4805-adcf-21da39108ec7
caps.latest.revision: 24
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6b96cb16182447ca636ee363a2cf62a33dcd6823
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51752934"
---
# <a name="how-to-access-the-built-in-fonts-and-color-scheme"></a>Como: acessar o esquema de cores e fontes internas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O ambiente de desenvolvimento integrado (IDE) do Visual Studio tem um esquema de fontes e cores que está associado com a janela do editor. Você pode acessar esse esquema por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface.  
  
 Para usar o esquema de cores e fontes internas, um VSPackage deve:  
  
- Defina uma categoria a ser usado com o serviço de fontes e cores padrão.  
  
- Registre-se a categoria com o servidor de fontes e cores padrão.  
  
- Aconselhamos o IDE que uma janela específica usa os itens de exibição interna e as categorias usando o `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer` e `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer` interfaces.  
  
  O IDE usa a categoria resultante como um identificador para a janela. Nome da categoria é exibido na **Mostrar configurações de:** caixa de lista suspensa na **fontes e cores** página de propriedades.  
  
### <a name="to-define-a-category-using-built-in-fonts-and-colors"></a>Para definir uma categoria usando cores e fontes internas  
  
1. Crie um GUID arbitrário.  
  
    Esse GUID é usado para identificar exclusivamente uma categoria<strong>.</strong> Esta categoria reutiliza a especificação de cores e fontes de padrão do IDE.  
  
   > [!NOTE]
   >  Ao recuperar dados de fontes e cores com o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> ou outras interfaces, VSPackages usará esse GUID para fazer referência a informações internas.  
  
2. Nome da categoria deve ser adicionado a uma tabela de cadeia de caracteres dentro do arquivo de recursos (. rc) do VSPackage, para que ele pode ser localizado conforme necessário, quando exibidas no IDE.  
  
    Para obter mais informações, consulte [adicionando ou excluindo uma cadeia de caracteres](http://msdn.microsoft.com/library/077077b4-0f4b-4633-92d6-60b321164cab).  
  
### <a name="to-register-a-category-using-built-in-fonts-and-colors"></a>Para registrar uma categoria usando cores e fontes internas  
  
1.  Construa um tipo especial de entrada de registro de categoria no seguinte local:  
  
     [HKLM\Software\Microsoft. \Visual Studio\\*\<versão do Visual Studio >* \FontAndColors\\*\<categoria >*]  
  
     *\<Categoria >* é o nome não localizado da categoria.  
  
2.  Preencha o registro para usar as fontes de estoque e o esquema de cores com quatro valores:  
  
    |Nome|Tipo|Dados|Descrição|  
    |----------|----------|----------|-----------------|  
    |Categoria|REG_SZ|GUID|Um GUID arbitrária que identifica uma categoria que contém o esquema de fontes e cores das ações.|  
    |Pacote|REG_SZ|GUID|{F5E7E71D-1401-11D1-883B-0000F87579D2}<br /><br /> Esse GUID é usado por todos os VSPackages que usam as configurações de fonte e cor padrão.|  
    |NameID|REG_DWORD|ID|A ID de recurso de um nome de categoria localizáveis em VSPackage.|  
    |ToolWindowPackage|REG_SZ|GUID|O GUID da implementação de VSPackage o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface.|  
  
3.  
  
### <a name="to-initiate-the-use-of-system-provided-fonts-and-colors"></a>Para iniciar o uso de cores e fontes fornecidas pelo sistema  
  
1. Criar uma instância da `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer` interface como parte da implementação e a inicialização da janela.  
  
2. Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer.GetPropertyCategory%2A> método para obter uma instância das `T:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer` interface correspondente ao atual <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> instância.  
  
3. Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A> duas vezes.  
  
   - Chamar uma vez com `VSEDITPROPID_ViewGeneral_ColorCategory`como um argumento.  
  
   - Chamar uma vez com `VSEDITPROPID_ViewGeneral_FontCategory` como um argumento.  
  
     Isso define e expõe os serviços de fontes e cores padrão como uma propriedade da janela.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir inicia o uso de cores e fontes internas.  
  
```  
CComVariant vt;  
CComQIPtr<IVsTextEditorPropertyCategoryContainer> spPropCatContainer(m_spView);  
if (spPropCatContainer != NULL){  
    CComPtr<IVsTextEditorPropertyContainer> spPropContainer;  
    if (SUCCEEDED(spPropCatContainer->GetPropertyCategory(GUID_EditPropCategory_View_MasterSettings,   
                                                          &spPropContainer))){  
        CComVariant vt;CComVariant VariantGUID(bstrGuidText);  
        spPropContainer->SetProperty(VSEDITPROPID_ViewGeneral_FontCategory, VariantGUID);  
        spPropContainer->SetProperty(VSEDITPROPID_ViewGeneral_ColorCategory, VariantGUID);  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usando fontes e cores](../extensibility/using-fonts-and-colors.md)   
 [Obtendo informações de cores para colorização de texto e fonte](../extensibility/getting-font-and-color-information-for-text-colorization.md)   
 [Acessando configurações de cor e a fonte armazenada](../extensibility/accessing-stored-font-and-color-settings.md)   
 [Visão geral de cor e de fonte](../extensibility/font-and-color-overview.md)

