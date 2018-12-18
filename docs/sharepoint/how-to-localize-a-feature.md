---
title: 'Como: localizar um recurso | Microsoft Docs'
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
- features [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c143016aaec81c65c118923ff9513bb4607353dc
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118371"
---
# <a name="how-to-localize-a-feature"></a>Como: localizar um recurso
  Por padrão, o recurso títulos e descrições de usam valores de cadeia de caracteres embutida. Para localizar o título do recurso e a descrição, substitua as cadeias de caracteres com expressões que fazem referência a recursos localizados.  
  
## <a name="localize-a-feature"></a>Localizar um recurso  
  
#### <a name="to-localize-a-feature"></a>Para localizar um recurso  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **Feature1** nó e, em seguida, escolha **adicionar recurso**.  
  
2.  No **adicionar recurso** diálogo caixa, escolha **idioma invariável** da lista como a cultura para o arquivo de recurso do recurso de idioma padrão.  
  
3.  Repita a etapa anterior para cada idioma localizado, escolhendo os idiomas de sua preferência para o recurso localizado em arquivos de recurso.  
  
     Os arquivos de recurso separados são criados: um para o idioma padrão e um para cada idioma que você deseja dar suporte a localizado.  
  
4.  Abra cada arquivo de recurso no Editor de recursos e, em seguida, insira todas as IDs de cadeia de caracteres e seus valores.  
  
     Por exemplo, no arquivo de recurso do recurso padrão, insira uma ID de cadeia de caracteres de **Title** com um valor de **meu título do recurso**, e uma segunda cadeia de caracteres ID da **descrição** com um valor de **Minha descrição do recurso**. Para cada arquivo de recurso localizado, usar a mesma cadeia de caracteres IDs usadas no recurso do recurso padrão, mas insira cadeias de caracteres localizadas para os valores.  
  
5.  Depois de inserir todos os valores de recursos, abra o menu de atalho para o recurso (por exemplo, *Feature1.feature*) e, em seguida, escolha **View Designer** para abrir o recurso no Designer de recurso.  
  
6.  Para localizar o **Title** e **descrição** campos no recurso, use o seguinte formato para inserir valores em suas caixas de:  
  
     `$Resources:` *ID de cadeia de caracteres*  
  
     Por exemplo, digite $Resources:**Title** na **título do recurso** caixa e $Resources:**descrição** no **descrição do recurso** caixa .  
  
     A IDs de cadeia de caracteres deve corresponder àqueles que são usados nos arquivos de recurso.  
  
7.  Escolha o **F5** tecla para compilar e executar o aplicativo.  
  
8.  No SharePoint, abra o **ações do Site** menu, escolha **configurações de Site**e, em seguida, no **ações do Site** seção escolher o **gerenciar recursos de Site** link.  
  
9. No SharePoint, altere o idioma de exibição do padrão.  
  
     O título do recurso localizado e a descrição são exibidos no aplicativo. Para exibir recursos localizados, o servidor do SharePoint deve ter um pacote de idiomas instalado que corresponda à cultura do arquivo de recurso.  
  
## <a name="see-also"></a>Consulte também
 [Localizar soluções do SharePoint](../sharepoint/localizing-sharepoint-solutions.md)   
 [Como: adicionar um arquivo de recurso](../sharepoint/how-to-add-a-resource-file.md)   
 [Como: localizar marcação ASPX](../sharepoint/how-to-localize-aspx-markup.md)   
 [Como: localizar o código](../sharepoint/how-to-localize-code.md)  
  
