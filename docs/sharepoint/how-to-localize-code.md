---
title: 'Como: localizar o código | Microsoft Docs'
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
- localizing code [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d170906a66ffaaa0e73d4d7d236c8f41290abe55
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118445"
---
# <a name="how-to-localize-code"></a>Como: localizar o código
  O código não localizado usa valores de cadeia de caracteres embutida. Para localizar as cadeias de caracteres de código, substitua-as por chamadas para <xref:System.Web.HttpContext.GetGlobalResourceObject%2A>, que é um método que referencia recursos localizados.  
  
## <a name="localize-code"></a>Localizar código  
  
#### <a name="to-localize-code"></a>Para localizar o código  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para um item de projeto e, em seguida, escolha **Add** > **módulo**.  
  
     Escolha o **arquivo de recursos** modelo.  
  
    > [!NOTE]  
    >  Certifique-se de adicionar o arquivo de recurso a um item de projeto do SharePoint para que a propriedade de tipo de implantação está disponível. Essa propriedade é necessária neste procedimento.  
  
2.  Nomeie o arquivo de recurso de idioma padrão de sua escolha com uma *. resx* extensão, como *Myappresources*.  
  
3.  Repita as etapas 1 e 2 para adicionar arquivos de recurso separados ao item de projeto do SharePoint: um para cada idioma localizado.  
  
     Use o mesmo nome de base para cada arquivo de recurso localizado, mas adicione a ID de cultura. Por exemplo, o nome de um alemão recurso localizado *MyAppResources.de-de. resx*.  
  
4.  Abra cada arquivo de recurso e adicione cadeias de caracteres localizadas. Use a mesma cadeia de caracteres IDs em cada arquivo.  
  
5.  Altere o valor da **tipo de implantação** propriedade de cada arquivo de recurso para **AppGlobalResource** para fazer com que cada arquivo implante a pasta App_GlobalResources do servidor.  
  
6.  Deixe o valor da **ação de compilação** propriedade de cada arquivo como **Embedded Resource**.  
  
     Recursos incorporados são compilados na DLL do projeto.  
  
7.  Compile o projeto para criar o recurso de DLLs satélite.  
  
8.  No **Designer de pacote**, escolha o **avançado** guia e, em seguida, adicione o assembly satélite.  
  
9. No **local** caixa, preceda uma pasta de ID de cultura para o caminho local, como *de-DE\\\<nome do Item de projeto >. Resources*.  
  
10. Se sua solução não fizer referência o assembly System. Web, adicione uma referência a ele e adicione uma diretiva em seu código para <xref:System.Web>.  
  
11. Localize todas as cadeias de caracteres codificadas em seu código que são visíveis aos usuários, como o texto da interface do usuário, erros e texto da mensagem. Substituí-los por uma chamada para o <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> método usando a seguinte sintaxe:  
  
    ```csharp  
    HttpContext.GetGlobalResourceObject("Resource File Name", "String ID")  
    ```  
  
12. Escolha o **F5** tecla para compilar e executar o aplicativo.  
  
13. No SharePoint, altere o idioma de exibição do padrão.  
  
     As cadeias de caracteres localizadas aparecem no aplicativo. Para exibir recursos localizados, o servidor do SharePoint deve ter um pacote de idiomas instalado que corresponda à cultura do arquivo de recurso.  
  
## <a name="see-also"></a>Consulte também
 [Localizar soluções do SharePoint](../sharepoint/localizing-sharepoint-solutions.md)   
 [Como: localizar um recurso](../sharepoint/how-to-localize-a-feature.md)   
 [Como: localizar marcação ASPX](../sharepoint/how-to-localize-aspx-markup.md)   
 [Como: adicionar um arquivo de recurso](../sharepoint/how-to-add-a-resource-file.md)  

