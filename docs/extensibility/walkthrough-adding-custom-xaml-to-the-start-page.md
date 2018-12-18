---
title: 'Passo a passo: Adicionar XAML personalizado à página inicial | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b0b6d095ad9fb45d5cc9bd8979a267cb2ccf961f
ms.sourcegitcommit: 9765b3fcf89375ca499afd9fc42cf4645b66a8a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46495616"
---
# <a name="walkthrough-add-custom-xaml-to-the-start-page"></a>Passo a passo: Adicionar XAML personalizado à página inicial
Este passo a passo mostra como criar um Visual Studio iniciar página personalizada que contém um navegador da Web.  
  
## <a name="adding-custom-xaml"></a>Adicionar XAML personalizado  
  
1.  Criar uma página inicial, seguindo as instruções em [criar uma página inicial personalizada](../extensibility/creating-a-custom-start-page.md).  
  
2.  No *MainWindow. XAML* do arquivo, localize o \<grade > seção.  
  
3.  Adicionar um \<TabControl > elemento e um \<TabItem > dentro de \< grade > elemento, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    <Grid>  
        <TabControl>  
            <TabItem Header="Bing" Height="Auto">  
                <Frame Source="http://www.bing.com" />  
            </TabItem>  
        </TabControl>  
    </Grid>  
    ```  
  
4.  Adicione um segundo \<TabItem >, com um \<botão > elemento que abre um novo projeto:  
  
    ```xml  
    <Grid>  
        <TabControl>  
            <TabItem Header="MyButton" Height="Auto">  
                <Button Name="btnNewProj" Content="New Project"   
                    Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
                    CommandParameter="File.NewProject" >  
                </Button>  
            </TabItem>  
            <TabItem Header="Bing" Height="Auto">  
                <Frame Source="http://www.bing.com" />  
            </TabItem>  
        </TabControl>  
    </Grid>  
    ```  
  
## <a name="testing-the-custom-start-page"></a>Testando a página inicial personalizada  
  
1.  Pressione **F5**.  
  
     A instância experimental do Visual Studio é aberto, com a página inicial personalizada instalada, mas não selecionada.  
  
2.  Na instância experimental do Visual Studio, abra o **/Ferramentas opções / ambiente** página.  
  
3.  Selecione **inicialização**. Sobre o **Personalizar página inicial** lista, selecione sua *. XAML* de arquivo e, em seguida, clique em **Okey**.  
  
4.  Sobre o **modo de exibição** menu, clique em **Start Page**.  
  
5.  Clique o **Bing** guia.  
  
     Você deve ver uma página da web do Bing.  
  
6.  Clique o **MyButton** guia.  
  
     Você deve ver uma **MyProject** botão que abre o **novo projeto** caixa de diálogo.  
  
7.  Feche a instância experimental.  
  
## <a name="apply-the-custom-start-page"></a>Aplicar a página inicial personalizada  
  
### <a name="to-test-the-custom-start-page"></a>Para testar a página inicial personalizada  
  
1.  Na **Ferramentas / opções / ambiente**, selecione **inicialização**. Sobre o **Personalizar página inicial** lista, selecione sua *. XAML* de arquivo e, em seguida, clique em **Okey**.  
  
## <a name="next-steps"></a>Próximas etapas  
 A página do Visual Studio iniciar agora contém uma guia que exibe uma guia de MyButton e uma guia do navegador da Web. Você pode criar páginas personalizadas Iniciar que têm outras funcionalidades usando o *de lógica* modelo para adicionar um arquivo. dll personalizado, conforme mostrado na [adicionando o controle de usuário para a página início](../extensibility/adding-user-control-to-the-start-page.md). Você pode compartilhar páginas de inicialização personalizada com outros usuários ao publicar o arquivo. VSIX resultante para o [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847) site da Web ou para outro site da Web ou de rede no compartilhamento. Para obter mais informações, consulte [implantação de páginas de inicialização personalizada](../extensibility/deploying-custom-start-pages.md).  
  
## <a name="see-also"></a>Consulte também  
 [Personalizar a página inicial](../ide/customizing-the-start-page-for-visual-studio.md)   
 [Controles de contêiner do WPF](https://msdn.microsoft.com/library/a0177167-d7db-4205-9607-8ae316952566)