---
title: Como solucionar problemas de modelos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio templates, troubleshooting
ms.assetid: 3e577ad2-f725-4c11-93b3-477f2404ec81
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: a68097745de1f1d94e5c09963a474a0095588fba
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49296420"
---
# <a name="how-to-troubleshoot-templates"></a>Como solucionar problemas de modelos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se houver falha no carregamento de um modelo no ambiente de desenvolvimento, haverá várias maneiras de localizar o problema.  
  
## <a name="validating-the-vstemplate-file"></a>Validando o arquivo .vstemplate  
 Se o arquivo .vstemplate em um modelo não estiver de acordo com o esquema de modelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], talvez o modelo não seja exibido na caixa de diálogo **Novo Projeto**.  
  
#### <a name="to-validate-the-vstemplate-file"></a>Para validar o arquivo .vstemplate  
  
1.  Localize o arquivo .zip que contém o modelo.  
  
2.  Extraia o arquivo .zip.  
  
3.  No menu **Arquivo** no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], clique em **Abrir** e, em seguida, em **Arquivo**.  
  
4.  Selecione o arquivo .vstemplate para o modelo e clique em **Abrir**.  
  
5.  Verifique se o XML do arquivo .vstemplate está de acordo com o esquema de modelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Para obter mais informações sobre o esquema .vstemplate, consulte [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md).  
  
    > [!NOTE]
    >  Para obter suporte do IntelliSense enquanto cria o arquivo. vstemplate, adicione uma `xmlns` de atributo para o `VSTemplate` elemento e atribua um valor de http://schemas.microsoft.com/developer/vstemplate/2005.  
  
6.  Salve e feche o arquivo .vstemplate.  
  
7.  Selecione os arquivos incluídos em seu modelo, clique com o botão direito do mouse, selecione **Enviar Para** e clique em **Pasta Compactada (Zipada)**. Os arquivos selecionados são compactados em um arquivo .zip.  
  
8.  Insira o novo arquivo .zip no mesmo diretório do antigo arquivo .zip.  
  
9. Exclua os arquivos de modelo extraídos e o arquivo .zip de modelo antigo.  
  
## <a name="monitoring-the-event-log"></a>Monitorando o log de eventos  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] registra erros encontrados ao processar arquivos .zip de modelo. Se um modelo não for exibido na caixa de diálogo **Novo Projeto** conforme esperado, é possível usar o **Visualizador de Eventos** para solucionar o problema.  
  
#### <a name="to-locate-template-errors-in-event-viewer"></a>Para localizar erros de modelo no Visualizador de Eventos  
  
1.  No Windows, clique em **Iniciar**, em **Painel de Controle**, clique duas vezes em **Ferramentas Administrativas** e clique duas vezes em **Visualizador de Eventos**.  
  
2.  No painel esquerdo, clique em **Aplicativo**.  
  
3.  Procure eventos com um valor de **Origem** de `Visual Studio - VsTemplate`.  
  
4.  Clique duas vezes em um evento de modelo para exibir o erro.  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando modelos](../ide/customizing-project-and-item-templates.md)   
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)



