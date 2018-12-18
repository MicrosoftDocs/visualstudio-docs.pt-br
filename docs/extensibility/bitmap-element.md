---
title: Elemento bitmap | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Bitmaps
- Bitmaps element (VSCT XML schema)
ms.assetid: edcd7891-f4e7-416d-809d-5e2eed9f17e4
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 624a8e4a47e7043c2e3726f23b9d2a94defdea32
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49846649"
---
# <a name="bitmap-element"></a>Elemento bitmap
Define um bitmap. O bitmap é carregado de um recurso ou de um arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<Bitmap guid="guidImages" href="images\MyImage.bmp" usedList="bmp1, bmp2, bmp3" />  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|GUID|Necessário. GUID do identificador de comando/ID de GUID.<br /><br /> O atributo de guid para um bitmap não está associado a qualquer VSPackage ou outro grupo de comando.  Ele deve ser exclusivo para a definição de bitmap e não deve ser usado para qualquer outra finalidade.|  
|resID|ID do identificador de comando/ID de GUID. É necessário o resID ou o atributo href.<br /><br /> O atributo resID é uma ID de recurso de inteiro que determina a faixa de bitmap que deve ser carregada durante a mesclagem de tabela de comando.  Quando a tabela de comando está sendo carregada, os bitmaps especificados pela ID de recurso serão carregados do recurso do mesmo módulo.|  
|usedlist do bloco|Necessário se o atributo resID estiver presente. Seleciona as imagens disponíveis na faixa de bitmap.|  
|href|Caminho para o bitmap. É necessário o resID ou o atributo href.<br /><br /> O caminho de inclusão é pesquisado para o arquivo de imagem indicada, o que é inserido no binário resultante.  Durante a mesclagem de tabela de comando, a imagem é copiada e nenhuma pesquisa de recursos adicionais ou a carga é necessária.  Se o atributo usedlist do bloco não estiver presente, todas as imagens na faixa de estão disponíveis. **Observação:** imagens podem ser fornecidas em vários formatos que incluem *bmp*, *PNG*, e *. gif*.  Versões anteriores do compilador não dava suporte a imagens de bitmap de 32 bits que tinha informações de alfa para transparência parcial. A solução alternativa para essas versões é usar o *PNG* formato.|  
|Condição|Opcional. Ver [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Elemento bitmaps](../extensibility/bitmaps-element.md)|Agrupa elementos do Bitmap.|  
  
## <a name="example"></a>Exemplo  
  
```  
<Bitmap guid="guidWidgetIcons" href="WidgetToolbarIcons_32.bmp" />  
<Bitmap guid="guidWidgetIcons2" resID="IDBMP_WIDGETICONS"  
  usedList="1, 2, 3, 4"/>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de tabela (. VSCT) de comando do Visual Studio](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)