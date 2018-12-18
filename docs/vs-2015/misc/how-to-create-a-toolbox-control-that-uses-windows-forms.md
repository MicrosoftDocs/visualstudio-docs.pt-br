---
title: 'Como: criar um controle de caixa de ferramentas que usa o Windows Forms | Microsoft Docs'
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
- Toolbox control
- winforms
- toolbox
ms.assetid: abbd3c3c-3a6e-4539-bd6c-a5891dead234
caps.latest.revision: 12
manager: douge
ms.openlocfilehash: 2860f3fca32b3a87967a404fb47626416d9f5dce
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49263712"
---
# <a name="how-to-create-a-toolbox-control-that-uses-windows-forms"></a>Como: criar um controle de caixa de ferramentas que usa o Windows Forms
O modelo de controle de caixa de ferramentas do Windows Forms que está incluído na [!INCLUDE[vssdk_dev11_long](../includes/vssdk-dev11-long-md.md)] permite que você crie controles de formulários do Windows que são adicionados automaticamente para o **caixa de ferramentas** quando a extensão está instalada. Este tópico mostra como usar o modelo para criar uma **caixa de ferramentas** controle que você pode distribuir a outros usuários...  
  
> [!NOTE]
>  Para saber como baixar o SDK do Visual Studio, consulte [Visual Studio Extensibility Developer Center](http://go.microsoft.com/fwlink/?linkid=121964) no site do MSDN.  
  
## <a name="creating-a-toolbox-control"></a>Criando um controle de caixa de ferramentas  
 Usar o modelo de controle de caixa de ferramentas do Windows Forms para criar o projeto e, em seguida, crie uma interface do usuário (IU) no designer.  
  
#### <a name="to-create-a-windows-forms-toolbox-control-project"></a>Para criar um projeto de controle de caixa de ferramentas do Windows Forms  
  
1.  No menu **Arquivo**, clique em **Novo** e clique em **Projeto**.  
  
2.  No **novo projeto** caixa de diálogo **modelos instalados**, clique no nó de linguagem de programação preferencial e, em seguida, clique em **extensibilidade**. Na lista de tipos de projeto, selecione **controle de caixa de ferramentas do Windows Forms**.  
  
3.  No **nome** , digite o nome que você deseja usar para o projeto. Clique em **OK**.  
  
     O Visual Studio cria uma solução que contém um controle de usuário para colocar o controle um atributo de **caixa de ferramentas**, e de manifesto de um VSIX para implantação.  
  
#### <a name="to-build-the-control-ui"></a>Para criar o controle da interface do usuário  
  
1.  Na **Gerenciador de soluções**, clique duas vezes em ToolboxControl.cs para abri-lo no designer.  
  
2.  Dos **caixa de ferramentas**, arraste os controles que você deseja para a superfície de design e organizá-los de acordo com seu design.  
  
3.  No **propriedades** janela, defina as propriedades públicas no controle de usuário e no filho controles.  
  
## <a name="coding-the-control"></a>O controle de codificação  
 Por padrão, o controle será exibido na **caixa de ferramentas** como **ToolboxControl1** em um **caixa de ferramentas** grupo de item que tem o mesmo nome que sua solução. Você pode alterar esses nomes no arquivo ToolboxControl.cs.  
  
#### <a name="to-code-the-control"></a>Para o controle do código  
  
1.  Na **Gerenciador de soluções**, clique com botão direito ToolboxControl.cs e, em seguida, clique em **Exibir código** para abrir o arquivo no modo de exibição de código.  
  
2.  A definição de classe parcial que implementa o controle, clique no nome de classe, clique em **refatorar**e, em seguida, clique em **Renomear**. Altere o nome da classe para o nome que você deseja exibir na **caixa de ferramentas** quando o controle está instalado.  
  
3.  Imediatamente acima da definição de classe, na `ProvideToolboxControl` declaração de atributo, altere o valor do primeiro parâmetro para o nome do grupo de itens que hospedará o controle em de **caixa de ferramentas**.  
  
     A exemplo a seguir mostra a `ProvideToolboxControl` atributo e a definição de classe ajustado para um controle chamado `Counter` no `General` grupo de itens.  
  
     [!code-csharp[ToolboxControlWinForms#07](../snippets/csharp/VS_Snippets_VSSDK/toolboxcontrolwinforms/cs/toolboxcontrol.cs#07)]  
  
4.  Implemente as propriedades, métodos e eventos do controle.  
  
## <a name="building-testing-and-deployment"></a>Criação, teste e implantação  
 Pressionando F5 compila o projeto, que inclui um arquivo de implantação. VSIX e abre uma segunda instância do Visual Studio que tem o controle instalado na **caixa de ferramentas**.  
  
#### <a name="to-build-and-test-the-control"></a>Para compilar e testar o controle  
  
1.  Pressione F5.  
  
2.  Na nova instância do Visual Studio, crie um projeto de aplicativo do Windows Forms.  
  
3.  Localizar seu controle na **caixa de ferramentas** e arraste-o para a superfície de design.  
  
4.  No **propriedades** janela, verifique se suas propriedades aparecem conforme o esperado.  
  
5.  Adicione qualquer código ou controles adicionais que são necessárias para testar seus métodos e eventos.  
  
6.  Pressione F5 para abrir o aplicativo de formulários do Windows.  
  
7.  Verifique se que as propriedades, métodos e eventos do seu controle se comportar conforme o esperado.  
  
#### <a name="to-deploy-the-control"></a>Para implantar o controle  
  
1.  Depois de compilar o projeto testado, abra a pasta de \bin\debug\ do projeto no Explorador de arquivos e localize o arquivo. VSIX.  
  
2.  Carregar o arquivo. VSIX para uma rede ou em um site da Web.  
  
     Se você carregar o arquivo para o [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847) site da Web, outros usuários podem usar **Gerenciador de extensões** no Visual Studio para localizar o controle e instalá-lo.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um controle de caixa de ferramentas do WPF](../extensibility/creating-a-wpf-toolbox-control.md)