---
title: Testando os aplicativos do SharePoint 2010 com testes de IU codificados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 51b53778-469c-4cc9-854c-4e4992d6389b
caps.latest.revision: 32
ms.author: gewarren
manager: douge
ms.openlocfilehash: e450cd333c01e4e2e557013ef106337fe5a80a71
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49937272"
---
# <a name="testing-sharepoint-2010-applications-with-coded-ui-tests"></a>Testando os aplicativos do SharePoint 2010 com testes de interface do usuário codificada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Incluir testes de IU codificados em um aplicativo do SharePoint permite verificar se o aplicativo inteiro, incluindo seus controles de interface do usuário, está funcionando corretamente. Testes de IU codificados também podem validar valores e lógica na interface do usuário.  
  
 **Requisitos**  
  
-   Visual Studio Enterprise  
  
## <a name="what-else-should-i-know-about-coded-ui-tests"></a>O que mais eu deveria saber sobre testes de IU codificados?  
 Para saber mais sobre os benefícios de usar testes de IU codificados, consulte [Usar a automação da interface do usuário para testar seu código](../test/use-ui-automation-to-test-your-code.md) e [Teste para entrega contínua com Visual Studio 2012 – capítulo 5 Automatizando testes do sistema](http://go.microsoft.com/fwlink/?LinkID=255196).  
  
 **Observações**  
  
-   ![Pré-requisito](../test/media/prereq.png "Prereq") Testes de IU codificado para aplicativos do SharePoint têm suporte apenas com SharePoint 2010.  
  
-   ![Pré-requisito](../test/media/prereq.png "Prereq") Não há suporte para controles do Visio e PowerPoint 2010 no seu aplicativo do SharePoint.  
  
## <a name="creating-a-coded-ui-test-for-your-sharepoint-app"></a>Criando um teste de IU codificado para seu aplicativo do SharePoint  
 [Criar testes de IU codificados](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate) para seus aplicativos do SharePoint 2010 é o mesmo processo que criar testes para outros tipos de aplicativos. A gravação e reprodução têm suporte para todos os controles na interface de edição na Web. A interface para a seleção de categorias e as Web parts são controles da Web padrão.  
  
 ![Web parts do SharePoint](../test/media/cuit-sharepoint.png "CUIT_SharePoint")  
  
> [!NOTE]
>  Se você estiver registrando a ação, valide as ações antes de gerar código. Como há vários comportamentos associados à passagem do Mouse, ela é ativada por padrão. Tenha cuidado para remover passagens redundantes de testes de IU codificados. Você pode fazer isso editando o código para o teste ou usando o [Editor de testes de IU codificados](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md).  
  
## <a name="including-testing-of-office-2010-controls-within-your-sharepoint-app"></a>Incluindo testes dos controles do Office 2010 em seu aplicativo do SharePoint  
 Para habilitar a automação de algumas Web parts do Office 2010 em seu aplicativo do SharePoint, você precisa fazer algumas modificações secundárias no código.  
  
> [!WARNING]
>  Não há suporte para controles do Visio e do PowerPoint 2010.  
  
### <a name="excel-2010-cell-controls"></a>Controles de célula do Excel 2010  
 Para incluir controles de célula do Excel, você deve fazer algumas alterações no código do teste de IU codificado.  
  
> [!WARNING]
>  Inserir texto em uma célula do Excel, seguida por uma ação de teclas de direção, não registrará corretamente. Use o mouse para selecionar células.  
  
 Se você estiver gravando ações em uma célula vazia, você deverá modificar o código clicando duas vezes na célula e, em seguida, executando uma operação de definição de texto. Isso é necessário porque um clique na célula, seguido por qualquer ação de teclado, ativa o `textarea` dentro da célula. Registrar um `setvalue` na célula vazia pesquisaria o `editbox` que não está presente até que a célula tenha sido clicada. Por exemplo:  
  
```csharp  
Mouse.DoubliClick(uiItemCell,new Point(31,14));  
uiGridKeyboardInputEdit.Text=value;  
```  
  
 Se você estiver gravando ações em uma célula não vazia, a gravação ficará um pouco mais complicada, porque, no momento em que você adicionar texto a uma célula, um novo controle \<div > é adicionado como um filho da célula. O novo controle \<div > contém o texto que você acabou de inserir. O gravador precisa registrar ações no novo controle \<div >; no entanto, ele não pode porque o novo controle \<div > não existe até depois que o teste for inserido. Você deve fazer as seguintes alterações de código manualmente para corrigir esse problema.  
  
1.  Vá para a inicialização de célula e realize as propriedades primárias `RowIndex` e `ColumnIndex`:  
  
    ```csharp  
    this.mUIItemCell.SearchProperties[HtmlCell.PropertyNames. RowIndex] = "3";   
    this.mUIItemCell.SearchProperties[HtmlCell.PropertyNames. ColumnIndex] = "3";  
    ```  
  
2.  Encontre o `HtmlDiv` filho da célula:  
  
    ```csharp  
    private UITestControl getControlToDoubleClick(HtmlCell cell)   
    {   
         if (String.IsNullOrEmpty(cell.InnerText)) return cell;   
         HtmlDiv pane = new HtmlDiv(cell);   
         pane.FilterProperties[HtmlDiv.PropertyNames.InnerText] = cell.InnerText;   
         // Class is an important property in finding pane   
         pane.FilterProperties[HtmlDiv.PropertyNames.Class] = "cv-nwr";   
         UITestControlCollection panes = pane.FindMatchingControls();   
         return panes[0];   
    }  
  
    ```  
  
3.  Adicione o código para a ação de clicar duas vezes no mouse em `HtmlDiv`:  
  
    ```csharp  
    Mouse.DoubleClick(uIItemPane, new Point(31, 14)); )  
    ```  
  
4.  Adicione código para definir o texto em `TextArea`:  
  
    ```csharp  
    uIGridKeyboardInputEdit.Text = value; }  
    ```  
  
## <a name="enabling-coded-ui-testing-of-silverlight-web-parts-in-your-sharepoint-2010-app"></a>Habilitando o teste de IU codificado de Web parts do Silverlight no seu aplicativo do SharePoint 2010  
 O teste do Silverlight não tem suporte no Visual Studio 2012 e versões posteriores. Mas, se quiser testar as Web parts do Silverlight em seu aplicativo do SharePoint 2010, será possível instalar um plug-in do Silverlight separado da Galeria do Visual Studio.  
  
#### <a name="setting-up-your-machine"></a>Configurando seu computador  
  
1. Certifique-se de que você tenha o Visual Studio 2012.1 ou posterior instalado.  
  
2. Instale o [Plug-in de teste de IU do Microsoft Visual Studio para o Silverlight](http://visualstudiogallery.msdn.microsoft.com/28312a61-9451-451a-990c-c9929b751eb4).  
  
3. Instale o [Fiddler](http://www.fiddler2.com/fiddler2/). Essa é apenas uma ferramenta que captura e registra o tráfego HTTP.  
  
4. Baixe o [projeto fiddlerXap](http://blogs.msdn.com/cfs-file.ashx/__key/communityserver-components-postattachments/00-10-36-48-70/FiddlerXapProxy.zip). Descompacte-o, compile-o e execute o script de "CopySLHelper.bat" para instalar a DLL auxiliar que é necessária para testar as Web parts do Silverlight quando você usar a ferramenta Fiddler.  
  
   Depois de configurar seu computador, para começar a testar seu aplicativo do SharePoint 2010 com Web parts do Silverlight, siga estas etapas:  
  
#### <a name="testing-silverlight-web-parts"></a>Testando Web parts do Silverlight  
  
1.  Inicie o Fiddler.  
  
2.  Limpe o cache do navegador. Isso é necessário porque o arquivo XAP, que contém a DLL auxiliar de automação de interface do usuário do Silverlight, normalmente é armazenado em cache. Temos que ter certeza de que o arquivo XAP modificado é obtido, portanto, limpe o cache do navegador.  
  
3.  Abra a página da Web.  
  
4.  Inicie o gravador e gere o código como você faria para um teste de aplicativo Web normal.  
  
5.  Você deve confirmar que o código gerado faz referência a Microsoft.VisualStudio.TestTools.UITest.Extension.Silverlight.dll.  
  
     Para obter mais informações, consulte [Testando a interface do usuário do SharePoint 2010 com o Visual Studio 2012](http://blogs.msdn.com/b/visualstudioalm/archive/2012/11/01/ui-testing-sharepoint-2010-with-visual-studio-2012.aspx)  
  
## <a name="external-resources"></a>Recursos externos  
  
### <a name="blogs"></a>Blogs  
 [Testando a interface do usuário do SharePoint 2010 com o Visual Studio 2012](http://blogs.msdn.com/b/visualstudioalm/archive/2012/11/01/ui-testing-sharepoint-2010-with-visual-studio-2012.aspx)  
  
 [Noções básicas sobre a lógica de pesquisa para controles do Silverlight no teste de IU codificado](http://blogs.msdn.com/b/tapas_sahoos_blog/archive/2010/11/16/understanding-the-search-logic-for-silverlight-controls-in-coded-ui-test.aspx)  
  
 [Buscando propriedade de um controle do Silverlight](http://blogs.msdn.com/b/tapas_sahoos_blog/archive/2010/11/16/fetching-property-of-a-silverlight-control.aspx)  
  
 [Índice de conteúdo para o teste de IU codificado](http://blogs.msdn.com/b/mathew_aniyan/archive/2010/02/11/content-index-for-coded-ui-test.aspx)  
  
### <a name="guidance"></a>Diretrizes  
 [Teste de entrega contínua com o Visual Studio 2012 – Capítulo 5: Automatizando testes do sistema](http://go.microsoft.com/fwlink/?LinkID=255196)  
  
### <a name="forum"></a>Fórum  
 [Visual Studio ALM + Team Foundation Server Blog](http://go.microsoft.com/fwlink/?LinkID=254496)  
  
## <a name="see-also"></a>Consulte também  
 [Usar a automação de interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)   
 [Teste de carga e de desempenho Web para aplicativos do SharePoint 2010 e 2013](http://msdn.microsoft.com/library/20c2e469-0e4e-4296-a739-c0e8fff36e54)   
 [Criar soluções do SharePoint](http://msdn.microsoft.com/library/4bfb1e59-97c9-4594-93f8-3068b4eb9631)   
 [Verificando e depurando código do SharePoint](http://msdn.microsoft.com/library/b5f3bce2-6a51-41b1-a292-9e384bae420c)   
 [Compilando e depurando soluções do SharePoint](http://msdn.microsoft.com/library/c9e7c9ab-4eb3-40cd-a9b9-6c2a896f70ae)   
 [Criando o perfil do desempenho de aplicativos do SharePoint](http://msdn.microsoft.com/library/61ae02e7-3f37-4230-bae1-54a498c2fae8)



