---
title: Como criar e aplicar um recurso
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: conceptual
f1_keywords:
- VS.XamlDesigner.CreateResource
- VS.XamlDesigner.EditResource
ms.assetid: 3ff4006d-659d-4073-9a41-06ff85e6cfdf
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: df8c3a225b4e8f4e65826c1db0c806c716d8fb0f
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53903858"
---
# <a name="how-to-create-and-apply-a-resource"></a>Como criar e aplicar um recurso
Os estilos e modelos de elementos no Designer XAML são armazenados em entidades reutilizáveis chamadas recursos. Os estilos permitem que você defina propriedades de elemento e reutilize essas configurações para obter uma aparência consistente entre vários elementos. Um [ControlTemplate](/uwp/api/Windows.UI.Xaml.Controls.ControlTemplate) define a aparência de um controle e também pode ser aplicado como um recurso. Para obter mais informações, confira [Início Rápido: Controles de estilo](http://go.microsoft.com/fwlink/?LinkID=248239) e [Início Rápido: Modelos de controle](http://go.microsoft.com/fwlink/?LinkID=247982).

 Sempre que você cria um novo recurso de uma propriedade existente, [Estilo](/uwp/api/Windows.UI.Xaml.Style), `ControlTemplate` ou caixa de diálogo **Criar Recurso** permite definir o recurso no nível do aplicativo, no nível do documento ou no nível do elemento. Esses níveis determinam onde você pode usar o recurso. Por exemplo, se você definir o recurso no nível de elemento, o recurso só poderá ser aplicado ao elemento no qual ele foi criado. Você também pode optar por armazenar o recurso em um dicionário de recursos, que é um arquivo separado que você pode usar novamente em outro projeto.

### <a name="to-create-a-new-resource"></a>Para criar um novo recurso

1.  Com um arquivo XAML aberto no Designer XAML, crie um elemento ou selecione um elemento na janela Estrutura de Tópicos de Documento.

2.  Na janela Propriedades, escolhe o marcador de propriedade exibido como um símbolo de caixa à direita de um valor da propriedade e escolha **Converter em Novo Recurso**. Um símbolo de caixa branca indica um valor padrão e um símbolo de caixa preta normalmente indica que um recurso local foi aplicado.

     A caixa de diálogo apropriada para criar um recurso é exibida. Esta caixa de diálogo é exibida quando você cria um recurso com um pincel:

     ![Caixa de diálogo Criar recurso](../designers/media/xaml_create_resource.png)

3.  Na caixa **Nome (Chave)**, insira um nome de chave. Este é o nome que você pode usar quando quer que outros elementos façam referência ao recurso.

4.  Em **Definir em**, escolha opção que especifica onde você deseja que o recurso seja definido:

    -   Para disponibilizar o recurso para qualquer documento em seu aplicativo, escolha **Aplicativo**.

    -   Para disponibilizar o recurso somente para o documento atual, escolha **Este documento**.

    -   Para disponibilizar o recurso somente para o elemento com base no qual você criou o recurso ou para seus elementos filho, clique em **Este documento** e, na lista suspensa, selecione **element**: **name**.

    -   Para definir o recurso em um arquivo de dicionário de recursos que pode ser reutilizado em outros projetos, clique em **Dicionário de recursos** e selecione um arquivo de dicionário de recursos existente, como **StandardStyles.xaml** na lista suspensa.

5.  Escolha o botão **OK** para criar o recurso e aplicá-lo ao elemento do qual você o criou.

### <a name="to-apply-a-resource-to-an-element-or-property"></a>Para aplicar um recurso a um elemento ou propriedade

1. Na janela Estrutura de Tópicos do Documento, escolha o elemento em que você deseja aplicar um recurso.

2. Realize um dos seguintes procedimentos:

   - Aplique um recurso a uma propriedade. Na janela Propriedades, escolha o marcador de propriedade ao lado do valor da propriedade, escolha **Recurso Local** ou **Recurso do Sistema** e escolha um recurso disponível na lista que é exibida.

      Se um recurso que você esperava ver não aparecer, poderá ser porque o tipo de recurso não corresponde ao tipo da propriedade.

   - Aplique um estilo ou recurso de modelo de controle a um controle. Abra o menu de contexto para um controle na janela Estrutura de Tópicos de Documento, escolha **Editar Modelo** ou **Editar Modelos Adicionais**, escolha **Aplicar Recurso** e selecione o nome do modelo de controle na lista que é exibida.

     > [!NOTE]
     >  **Editar Modelo** aplica modelos de controle. **Editar Modelos Adicionais** aplica outros tipos de modelo.

     É possível aplicar recursos sempre que eles são compatíveis. Por exemplo, você pode aplicar um recurso de pincel à propriedade **Primeiro plano** de um controle <xref:Windows.UI.Xaml.Controls.TextBox>.

### <a name="to-edit-a-resource"></a>Para editar um recurso

1.  Escolha um elemento na prancheta ou na janela Estrutura de Tópicos de Documento.

2.  Escolha no marcador de propriedade Padrão ou Local à direita da propriedade na janela Propriedades e clique em **Editar Recurso** para abrir a caixa de diálogo **Editar Recurso**.

3.  Modifique as opções do recurso.

## <a name="see-also"></a>Consulte também

- [Criando uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)