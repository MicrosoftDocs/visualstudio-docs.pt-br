---
title: 'Como: Localizar código | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing code [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6c1963ff0b6ef317dfa1a2c8154a1628710dc562
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016688"
---
# <a name="how-to-localize-code"></a>Como: Localizar código
  O código não local usa valores de cadeia de caracteres embutidos em código. Para localizar cadeias de caracteres de código, substitua-as por chamadas para <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> , que é um método que faz referência a recursos localizados.

## <a name="localize-code"></a>Código de localização

#### <a name="to-localize-code"></a>Para localizar o código

1. No **Gerenciador de soluções**, abra o menu de atalho para um item de projeto e escolha **Adicionar**  >  **módulo**.

     Escolha o modelo de **arquivo de recursos** .

    > [!NOTE]
    > Certifique-se de adicionar o arquivo de recurso a um item de projeto do SharePoint para que a propriedade do tipo de implantação esteja disponível. Essa propriedade é necessária posteriormente neste procedimento.

2. Dê ao arquivo de recurso de idioma padrão um nome de sua escolha anexado com uma extensão *. resx* , como *MyAppResources. resx*.

3. Repita as etapas 1 e 2 para adicionar arquivos de recurso separados ao item de projeto do SharePoint: um para cada idioma localizado.

     Use o mesmo nome base para cada arquivo de recurso localizado, mas adicione a ID de cultura. Por exemplo, nomeie um recurso localizado *em alemão MyAppResources.de-de. resx*.

4. Abra cada arquivo de recurso e adicione cadeias de caracteres localizadas. Use as mesmas IDs de cadeia de caracteres em cada arquivo.

5. Altere o valor da propriedade **tipo de implantação** de cada arquivo de recurso para **AppGlobalResource** para fazer com que cada arquivo seja implantado na pasta App_GlobalResources do servidor.

6. Deixe o valor da propriedade **criar ação** de cada arquivo como **recurso incorporado**.

     Os recursos inseridos são compilados na DLL do projeto.

7. Compile o projeto para criar as DLLs de satélite de recurso.

8. No **Designer de pacotes**, escolha a guia **avançado** e, em seguida, adicione o assembly satélite.

9. Na caixa **local** , preceda uma pasta de ID de cultura para o caminho do local, como *de \\ \<Project Item Name>.resources.dll*.

10. Se sua solução ainda não fizer referência ao assembly System. Web, adicione uma referência a ele e adicione uma diretiva em seu código para <xref:System.Web> .

11. Localize todas as cadeias de caracteres embutidas em código em seu código que são visíveis para os usuários, como texto da interface do usuário, erros e texto da mensagem. Substitua-os por uma chamada para o <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> método usando a seguinte sintaxe:

    ```csharp
    HttpContext.GetGlobalResourceObject("Resource File Name", "String ID")
    ```

12. Escolha a tecla **F5** para compilar e executar o aplicativo.

13. No SharePoint, altere o idioma de exibição do padrão.

     As cadeias de caracteres localizadas aparecem no aplicativo. Para exibir recursos localizados, o servidor do SharePoint deve ter um pacote de idiomas instalado que corresponda à cultura do arquivo de recurso.

## <a name="see-also"></a>Consulte também
- [Localizar soluções do SharePoint](../sharepoint/localizing-sharepoint-solutions.md)
- [Como localizar um recurso](../sharepoint/how-to-localize-a-feature.md)
- [Como: localizar marcação ASPX](../sharepoint/how-to-localize-aspx-markup.md)
- [Como adicionar um arquivo de recurso](../sharepoint/how-to-add-a-resource-file.md)
