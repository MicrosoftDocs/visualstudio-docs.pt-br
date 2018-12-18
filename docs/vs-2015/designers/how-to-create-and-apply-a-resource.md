---
title: Como criar e aplicar um recurso | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.XamlDesigner.CreateResource
- VS.XamlDesigner.EditResource
ms.assetid: 3ff4006d-659d-4073-9a41-06ff85e6cfdf
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ef5dc15db983a54e60df447a2457d9dbc6804d85
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915796"
---
# <a name="how-to-create-and-apply-a-resource"></a>Como criar e aplicar um recurso
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os estilos e modelos de elementos no Designer XAML são armazenados em entidades reutilizáveis chamadas recursos. Os estilos permitem que você defina propriedades de elemento e reutilize essas configurações para obter uma aparência consistente entre vários elementos. Um [ControlTemplate](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.controltemplate.aspx) define a aparência de um controle e também pode ser aplicado como um recurso. Para obter mais informações, consulte [Guia de início rápido: definindo o estilo dos controles](http://go.microsoft.com/fwlink/?LinkID=248239) e [Guia de início rápido: modelos de controle](http://go.microsoft.com/fwlink/?LinkID=247982).  
  
 Sempre que você cria um novo recurso de uma propriedade existente, [Estilo](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.style.aspx), `ControlTemplate` ou caixa de diálogo **Criar Recurso** permite definir o recurso no nível do aplicativo, no nível do documento ou no nível do elemento. Esses níveis determinam onde você pode usar o recurso. Por exemplo, se você definir o recurso no nível de elemento, o recurso só poderá ser aplicado ao elemento no qual ele foi criado. Você também pode optar por armazenar o recurso em um dicionário de recursos, que é um arquivo separado que você pode usar novamente em outro projeto.  
  
### <a name="to-create-a-new-resource"></a>Para criar um novo recurso  
  
1.  Com um arquivo XAML aberto no Designer XAML, crie um elemento ou selecione um elemento na janela Estrutura de Tópicos de Documento.  
  
2.  Na janela Propriedades, escolhe o marcador de propriedade exibido como um símbolo de caixa à direita de um valor da propriedade e escolha **Converter em Novo Recurso**. Um símbolo de caixa branca indica um valor padrão, e um símbolo de caixa preta normalmente indica que um recurso local foi aplicado  
  
     A caixa de diálogo apropriada para criar um recurso é exibida. Esta caixa de diálogo é exibida quando você cria um recurso com um pincel:  
  
     ![Criar caixa de diálogo Recurso](../designers/media/xaml-create-resource.png "xaml_create_resource")  
  
3.  Na caixa **Nome (Chave)**, insira um nome de chave. Este é o nome que você pode usar quando quer que outros elementos façam referência ao recurso.  
  
4.  Em **Definir em**, escolha opção que especifica onde você deseja que o recurso seja definido:  
  
    -   Para disponibilizar o recurso para qualquer documento em seu aplicativo, escolha **Aplicativo**.  
  
    -   Para disponibilizar o recurso somente para o documento atual, escolha **Este documento**.  
  
    -   Para disponibilizar o recurso somente para o elemento com base no qual você criou o recurso ou para seus elementos filho, clique em **Este documento** e, na lista suspensa, selecione *element*: *name*.  
  
    -   Para definir o recurso em um arquivo de dicionário de recursos que pode ser reutilizado em outros projetos, clique em **Dicionário de recursos** e selecione um arquivo de dicionário de recursos existente, como **StandardStyles.xaml** na lista suspensa.  
  
5.  Escolha o botão **OK** para criar o recurso e aplicá-lo ao elemento do qual você o criou.  
  
### <a name="to-apply-a-resource-to-an-element-or-property"></a>Para aplicar um recurso a um elemento ou propriedade  
  
1. Na janela Estrutura de Tópicos de Documento, escolha o elemento ao qual você deseja aplicar um recurso.  
  
2. Realize um dos seguintes procedimentos:  
  
   - Aplique um recurso a uma propriedade. Na janela Propriedades, escolha o marcador de propriedade ao lado do valor da propriedade, escolha **Recurso Local** ou **Recurso do Sistema** e escolha um recurso disponível na lista que é exibida.  
  
      Se você não vir um recurso que esperava ver, é possível que o tipo do recurso não corresponda ao tipo da propriedade.  
  
   - Aplique um estilo ou recurso de modelo de controle a um controle. Abra o menu de contexto para um controle na janela Estrutura de Tópicos de Documento, escolha **Editar Modelo** ou **Editar Modelos Adicionais**, escolha **Aplicar Recurso** e selecione o nome do modelo de controle na lista que é exibida.  
  
     > [!NOTE]
     >  **Editar Modelo** é usado para aplicar modelos de controle. **Editar Modelos Adicionais** é usado para aplicar outros tipos de modelo.  
  
     Recursos podem ser aplicados sempre que forem compatíveis. Por exemplo, um recurso de pincel pode ser aplicado à propriedade **Primeiro plano** de um controle <xref:Windows.UI.Xaml.Controls.TextBox>.  
  
### <a name="to-edit-a-resource"></a>Para editar um recurso  
  
1.  Escolha um elemento na prancheta ou na janela Estrutura de Tópicos de Documento.  
  
2.  Escolha no marcador de propriedade Padrão ou Local à direita da propriedade na janela Propriedades e clique em **Editar Recurso** para abrir a caixa de diálogo **Editar Recurso**.  
  
3.  Modifique as opções do recurso.  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)



