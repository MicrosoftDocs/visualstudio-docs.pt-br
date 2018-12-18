---
title: 'Como: marcar controles como controles seguros | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- SharePoint development in Visual Studio, advanced packaging tools
- safe controls [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 04470034f1fa1531a1677b4acd6b36f0b99c8a62
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118450"
---
# <a name="how-to-mark-controls-as-safe-controls"></a>Como: marcar controles como controles seguros
  Para segurança, o SharePoint faz distinção entre controles da Web que estão protegidos contra injeção de script e controles da Web que não são. Protegido por controles, ou *controles seguros*, pode ser acessado por usuários não confiáveis. Você pode marcar os controles como seguro em que a propriedade de entradas de controle seguro de um item de projeto do SharePoint ou nos **Designer de pacote** quando você adiciona um assembly no pacote. Para saber mais, veja  
  
 [Alteração das configurações de arquivo de Web. config](http://go.microsoft.com/fwlink/?LinkId=178965) e [Registrando um Assembly de Web Part como um controle seguro](http://go.microsoft.com/fwlink/?LinkId=171013).  
  
> [!IMPORTANT]  
>  Esses procedimentos são para fins ilustrativos. Marcar controles seguros apenas se você tiver certeza de que eles sejam seguros.  
  
## <a name="marking-safe-controls-in-the-safe-control-entries-property"></a>Marcação de controles seguros na propriedade de entradas de controle seguro  
  
#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-safe-control-entries-property"></a>Para marcar controles como seguro ou não seguro na propriedade de entradas de controle seguro
  
1.  Crie uma solução do SharePoint com um projeto de Web Part Visual.  
  
2.  Adicione dois controles para a Web part: uma caixa de texto e um botão. Deixe os nomes de seus valores padrão, TextBox1 e Button1, respectivamente.  
  
3.  Adicione duas entradas para a Web part **entradas de controle seguro** propriedade. Para fazer isso, escolha as reticências (![elipse do Designer de dispositivo móvel do ASP.NET](../sharepoint/media/mwellipsis.gif "elipse do Designer de dispositivo móvel do ASP.NET")) lado a **entradas de controle seguro** propriedade em que o  **Propriedades** janela.  
  
     O **entradas de controle seguro** caixa de diálogo é exibida.  
  
4.  No **entradas de controle seguro** caixa de diálogo, escolha o **Add** botão duas vezes para adicionar duas entradas de controle seguro para o **membros** painel: uma para o botão e uma caixa de texto.  
  
5.  Escolha a primeira entrada de controle seguro e, em seguida, altere o valor de seu **seguro** propriedade a ser **falso**, sua **nome do tipo** propriedade para **Button1**e sua **seguro contra Script** propriedade a ser **False**.  
  
     Esta etapa identifica o controle de botão como um controle que não é seguro.  
  
6.  Escolha a segunda entrada de controle seguro na lista. Deixe o valor de seu **seguro** a propriedade como **True** e defina seu **nome do tipo** propriedade **TextBox1** e seu **seguro Em relação ao Script** propriedade para **verdadeiro**.  
  
     O controle de caixa de texto está marcado como um controle que é seguro contra injeção de script.  
  
7.  Escolha o botão **OK** para fechar a caixa de diálogo.  
  
## <a name="marking-safe-controls-in-the-package-designer"></a>Marcação de controles seguros no Designer de pacote  
  
#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-package-designer"></a>Para marcar controles como seguro ou não seguro no Designer de pacote
  
1.  Crie uma solução do SharePoint com um projeto de Web Part Visual.  
  
2.  Adicione dois controles para a Web part: uma caixa de texto e um botão. Deixe os nomes de seus valores padrão, TextBox1 e Button1, respectivamente.  
  
     Anote o namespace do controle, porque ele é usado mais tarde.  
  
3.  Na barra de menus, escolha **construir** > **compilar solução** para compilar o projeto.  
  
4.  Crie outra solução do SharePoint.  
  
5.  Na **Gerenciador de soluções**, abra o menu de atalho para o *pacote* file e, em seguida, escolha **abrir** para abrir o **Package Designer**.  
  
6.  No **Designer de pacote**, escolha o **avançado** guia.  
  
7.  Sob **Assemblies adicionais**, escolha o **Add** botão e, em seguida, escolha **adicionar Assembly existente** na lista.  
  
8.  No **adicionar Assembly existente** diálogo caixa, escolha o botão de reticências (![elipse do Designer de dispositivo móvel do ASP.NET](../sharepoint/media/mwellipsis.gif "elipse do Designer de dispositivo móvel do ASP.NET")) lado  **Caminho de origem**.  
  
9. Escolha o assembly da solução do SharePoint que você criou na etapa 1 e, em seguida, escolha o **abrir** botão.  
  
10. Neste exemplo, deixe o **destino de implantação** opção como GlobalAssemblyCache.  
  
     Esta etapa faz com que o assembly implantar o sistema de Cache de Assembly Global (GAC). Se você quiser que o assembly para implantar para a pasta de aplicativo (Bin) da Web, selecione essa opção em vez disso. Para obter mais informações, consulte [implantação de Web Parts no SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=177509).  
  
11. No **controles seguros** , escolha o **clique aqui para adicionar um novo item** botão.  
  
12. Insira os valores para as propriedades da tabela a seguir.  
  
    |Nome da Propriedade|Valor|  
    |-------------------|-----------|  
    |Namespace|O namespace totalmente qualificado para o controle, tal como **BdcModelProject1.VisualWebPart1**.|  
    |Nome do tipo|Button1|  
    |Nome do Assembly|Nome de um conjunto de alta segurança, como: Microsoft.Office.SharePoint.ClientExtensions, versão = 14.0.0.0, Culture = neutral, PublicKeyToken = 71e9bce111e9429c.|  
    |Safe|Desmarque a **seguro** caixa de seleção.|  
    |Seguro em relação ao Script|Deixe o **seguro contra Script** caixa de seleção desmarcada.|  
  
    > [!NOTE]  
    >  O **nome do Assembly** valor adicionado por meio de assemblies a **avançado** guia da **Package Designer** não é possível um token, ele deve ser um assembly de nome forte. Para obter mais informações, consulte [Criando e usando assemblies de nomes fortes](http://go.microsoft.com/fwlink/?LinkId=177513).  
  
13. Escolha o **guia** tecla para criar outra entrada de controle seguro.  
  
14. Escolha o **clique aqui para adicionar um novo item** novamente no botão.  
  
15. Insira os valores para as propriedades da tabela a seguir.  
  
    |Nome da Propriedade|Valor|  
    |-------------------|-----------|  
    |Namespace|O namespace totalmente qualificado para o controle, tal como **BdcModelProject1.VisualWebPart1**.|  
    |Nome do tipo|TextBox1|  
    |Nome do Assembly|Nome de um conjunto de alta segurança, como: Microsoft.Office.SharePoint.ClientExtensions, versão = 14.0.0.0, Culture = neutral, PublicKeyToken = 71e9bce111e9429c.|  
    |Safe|Selecione o **seguro** caixa de seleção.|  
    |Seguro em relação ao Script|Selecione o **seguro contra Script** caixa de seleção.|  
  
16. Escolha o **guia** da chave e, em seguida, escolha o **Okey** botão para fechar a caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também
 [Fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)   
 [Pacote e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)  
  
