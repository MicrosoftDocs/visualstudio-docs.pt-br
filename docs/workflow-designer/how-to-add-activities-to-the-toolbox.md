---
title: 'Designer de Fluxo de Trabalho-como: adicionar atividades à caixa de ferramentas'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: b3a8a785-5928-457a-8a50-30267e29503d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0ebe3f4c3daf5ee3a0f64a0197967b6da62a467b
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815819"
---
# <a name="how-to-add-activities-to-the-toolbox"></a>Como: Adicione atividades a caixa de ferramentas

As atividades podem ser adicionadas à **caixa de ferramentas** em sua solução de várias maneiras diferentes. Você pode adicioná-los do seu projeto atual, referênciá-los de um projeto diferente, ou referênciá-los de um conjunto diferente.

## <a name="to-add-an-activity-from-within-your-current-project"></a>Para adicionar uma atividade do seu projeto atual

1. Adicionar uma nova atividade personalizado ao seu projeto atual de fluxo de trabalho. Para obter mais informações sobre como adicionar uma nova atividade personalizada ao seu projeto, consulte [como adicionar um novo item a um projeto de fluxo de trabalho](../workflow-designer/how-to-add-a-new-item-to-a-workflow-project.md).

2. Adicione lógica personalizada para a atividade.

3. Compile o projeto. Se a compilação tiver sido bem-sucedida, uma nova categoria na **caixa de ferramentas** chamada " \<*project name*> " com a atividade personalizada incluída nessa categoria será exibida.

    > [!NOTE]
    > Se a caixa de ferramentas é reiniciada, as atividades personalizados serão removidas, mesmo se a solução é compilado novamente. Para repopular a caixa de ferramentas com atividades personalizadas após sua redefinição, reinicie o Visual Studio.

    > [!NOTE]
    > A caixa de ferramentas só pode mostrar uma atividade de um determinado nome. Se duas atividades diferentes assemblies com o mesmo nome de classe, somente um exibirá.

    > [!NOTE]
    > O domínio de aplicativo é compartilhado entre instâncias do editor; se as variáveis estáticas são usados, serão compartilhados entre instâncias do editor também. Se esse não é o comportamento desejado, um serviço deve ser usado para controlar instâncias variáveis. Consulte [usando o contexto de edição do ModelItem](/dotnet/framework/windows-workflow-foundation/using-the-modelitem-editing-context) para obter informações sobre como usar serviços dentro do designer.

## <a name="to-add-an-activity-from-within-a-different-project"></a>Para adicionar uma atividade de dentro de um projeto diferente

1. Abra uma solução que contém pelo menos um projeto de fluxo de trabalho e um projeto personalizado de biblioteca de atividade ou outro projeto de fluxo de trabalho que define uma atividade personalizado.

2. Criar ambos os projetos. Se as compilações tiverem sido bem-sucedidas, uma nova categoria na **caixa de ferramentas** chamada " \<*project name*> " com a atividade personalizada incluída nessa categoria será exibida.

## <a name="to-add-an-activity-to-the-toolbox-from-an-assembly"></a>Para adicionar uma atividade à caixa de ferramentas de um assembly

1. Abra uma solução de fluxo de trabalho.

2. No menu **ferramentas** , selecione **escolher itens da caixa de ferramentas**.

3. Na caixa de diálogo **escolher itens de caixa de ferramentas** , selecione a guia **componentes do sistema. atividades** e clique em **procurar** para navegar até o assembly que contém a atividade personalizada que você deseja adicionar.

4. Selecione o assembly e clique em **OK**. O componente personalizado de atividade é adicionado à lista de componentes e automaticamente selecionado.

    1. Clique em **OK** para fechar o diálogo.

5. Para exibir a caixa de ferramentas, selecione **caixa de ferramentas** no menu **Exibir** .

6. A atividade personalizada é exibida na **caixa de ferramentas** sob a categoria que estava em foco antes de o item ser adicionado. Por exemplo, se a categoria **geral** foi selecionada na **caixa de ferramentas** antes de adicionar o item da caixa de ferramentas, a atividade aparecerá na categoria **geral** .

## <a name="see-also"></a>Veja também

- [Usando o Designer de Fluxo de Trabalho](developing-applications-with-the-workflow-designer.md)
