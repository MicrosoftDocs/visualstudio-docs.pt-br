---
title: Como localizar um recurso | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- features [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b0d15654ba48b6c95cf2b2f7fa4f9cd665f0959a
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016137"
---
# <a name="how-to-localize-a-feature"></a>Como localizar um recurso
  Por padrão, títulos e descrições de recursos usam valores de cadeia de caracteres embutidos em código. Para localizar o título e a descrição do recurso, substitua as cadeias de caracteres por expressões que fazem referência a recursos localizados.

## <a name="localize-a-feature"></a>Localizar um recurso

#### <a name="to-localize-a-feature"></a>Para localizar um recurso

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó **Feature1** e escolha **Adicionar recurso**de recurso.

2. Na caixa de diálogo **Adicionar recurso** , escolha **Idioma invariável** na lista como a cultura do arquivo de recurso de recurso de idioma padrão.

3. Repita a etapa anterior para cada idioma localizado, escolhendo os idiomas de sua escolha para os arquivos de recurso de recurso localizado.

     Arquivos de recurso de recurso separados são criados: um para o idioma padrão e outro para cada idioma localizado que você deseja dar suporte.

4. Abra cada arquivo de recurso no editor de recursos e, em seguida, insira todas as IDs de cadeia de caracteres e seus valores.

     Por exemplo, no arquivo de recurso de recurso padrão, insira uma ID de cadeia de caracteres de **título** com um valor de **meu título de recurso**e uma segunda ID de **cadeia de caracteres** com um valor de **Descrição de meu recurso**. Para cada arquivo de recurso localizado, use as mesmas IDs de cadeias de caracteres usadas no recurso de recurso padrão, mas insira cadeias localizadas para os valores.

5. Depois de inserir todos os valores de recurso, abra o menu de atalho para o recurso (por exemplo, *Feature1. Feature*) e escolha **Designer de exibição** para abrir o recurso no designer de recursos.

6. Para localizar os campos **título** e **Descrição** no recurso, use o seguinte formato para inserir valores em suas caixas:

     `$Resources:` *ID da Cadeia de Caracteres*

     Por exemplo, digite $Resources:**título** na caixa **título do recurso** e $Resources:**Descrição** na caixa **Descrição do recurso** .

     As IDs de cadeia de caracteres devem corresponder às que são usadas nos arquivos de recurso.

7. Escolha a tecla **F5** para compilar e executar o aplicativo.

8. No SharePoint, abra o menu **ações do site** , escolha configurações do **site**e, na seção **ações do site** , escolha o link **gerenciar recursos do site** .

9. No SharePoint, altere o idioma de exibição do padrão.

     O título e a descrição do recurso localizado aparecem no aplicativo. Para exibir recursos localizados, o servidor do SharePoint deve ter um pacote de idiomas instalado que corresponda à cultura do arquivo de recurso.

## <a name="see-also"></a>Consulte também
- [Localizar soluções do SharePoint](../sharepoint/localizing-sharepoint-solutions.md)
- [Como adicionar um arquivo de recurso](../sharepoint/how-to-add-a-resource-file.md)
- [Como: localizar marcação ASPX](../sharepoint/how-to-localize-aspx-markup.md)
- [Como: Localizar código](../sharepoint/how-to-localize-code.md)
