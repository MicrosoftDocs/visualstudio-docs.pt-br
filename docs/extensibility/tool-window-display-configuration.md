---
title: Configuração de exibição da janela de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, configuring
- tool windows, appearance
ms.assetid: 502a4926-bb83-473e-94e2-8e833c5f8b53
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 087fc8bc20b8ed70001b44ae06c614fad58c1439
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839694"
---
# <a name="tool-window-display-configuration"></a>Configuração de exibição da janela de ferramenta
Quando um VSPackage registra uma janela de ferramentas, a posição padrão, tamanho, estilo de encaixe e outras informações de visibilidade é especificado em valores opcionais. Para obter mais informações sobre o registro de janela da ferramenta, consulte [ferramenta Windows no registro](../extensibility/tool-windows-in-the-registry.md)  

## <a name="window-display-information"></a>Informações de exibição da janela  
 Configuração de exibição básica da janela de ferramentas é armazenada em até seis valores opcionais:  

```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        <Version>\  
          ToolWindows\  
            <Tool Window GUID>\  
              (Default)       = reg_sz: <Package GUID>Name            = reg_sz: <name of tool window>Float           = reg_sz: <position>Style           = reg_sz: <dock style>Window          = reg_sz: <window GUID>Orientation     = reg_sz: <orientation>DontForceCreate = reg_dword: 0x00000000  
```  


| Nome | Tipo | Dados | Descrição |
|-----------------|-----------| - | - |
| Nome | REG_SZ | "O nome curto aqui" | Um nome curto que descreve a janela da ferramenta. Usado apenas para referência no registro. |
| Float | REG_SZ | "X1, Y1, X2, Y2" | Quatro valores separados por vírgula. X1, Y1 é a coordenada do canto superior esquerdo da janela de ferramentas. X2, Y2 é a coordenada do canto inferior direito. Todos os valores estão em coordenadas da tela. |
| Estilo | REG_SZ | "MDI"<br /><br /> "Float"<br /><br /> "Vinculado"<br /><br /> "Com guias"<br /><br /> "AlwaysFloat" | Uma palavra-chave especificando inicial exibem o estado da janela de ferramenta.<br /><br /> "MDI" = encaixado com janela MDI.<br /><br /> "Flutuar" = flutuante.<br /><br /> "Vinculado" = vinculado a outra janela (especificada na entrada de janela).<br /><br /> "Com guias" = combinada com outra janela de ferramenta.<br /><br /> "AlwaysFloat" = não pode ser encaixada.<br /><br /> Para obter mais informações, consulte a seção comentários abaixo. |
| Janela | REG_SZ | *\<GUID &GT;* | O GUID de uma janela para o qual a janela de ferramentas pode ser vinculada ou com guias. O GUID pode pertencer a uma das suas próprias janelas ou uma das janelas no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE. |
| {1&gt;Orientação&lt;1} | REG_SZ | "Esquerda"<br /><br /> "Right"<br /><br /> "Top"<br /><br /> "Inferior" | Consulte a seção de comentários abaixo. |
| DontForceCreate | REG_DWORD | 0 ou 1 | Quando essa entrada estiver presente e seu valor não for zero, a janela é carregada, mas não imediatamente exibida. |

### <a name="comments"></a>Comentários  
 A entrada de orientação define a posição em que a janela da ferramenta encaixa quando sua barra de título é clicado duas vezes. É a posição relativa à janela do especificado na entrada de janela. Se a entrada de estilo é definida como "Vinculado", a entrada de orientação pode ser "Esquerda", "Direita", "Top" ou "Inferior". Se a entrada de estilo é "com guias", a orientação de entrada pode ser "esquerda" ou "Direita" e especifica em que a guia é adicionada. Se a entrada de estilo é "Flutuar", a janela da ferramenta flutua pela primeira vez. Quando a barra de título é clicado duas vezes, as entradas de orientação e a janela se aplicam, e a janela usa o estilo "com guias". Se a entrada de estilo é "AlwaysFloat", a janela da ferramenta não pode ser encaixada. Se a entrada de estilo é "MDI", a janela da ferramenta está vinculada à área de MDI e a entrada de janela é ignorada.  

### <a name="example"></a>Exemplo  

```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        8.0Exp\  
          ToolWindows\  
            {A0C5197D-0AC7-4B63-97CD-8872A789D233}\  
              (Default)       = reg_sz: {DA9FB551-C724-11D0-AE1F-00A0C90FFFC3}  
              DontForceCreate = reg_dword: 0x00000000  
              Float           = reg_sz: 100,100,450,300  
              Name            = reg_sz: Bookmarks  
              Orientation     = reg_sz: Left  
              Style           = reg_sz: Tabbed  
              Window          = reg_sz: {34E76E81-EE4A-11D0-00A0C90FFFC3}  
```  

## <a name="tool-window-visibility"></a>Visibilidade da janela de ferramenta  
 Valores na subchave visibilidade opcional determinam as configurações de visibilidade da janela de ferramentas. Os nomes dos valores são usados para armazenar os GUIDs dos comandos que exigem a visibilidade da janela. Se o comando é executado, o IDE garante que a janela da ferramenta é criada e tornada visível.  

```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        <Version>\  
          ToolWindows\  
            <Tool Window GUID>\  
              Visibility\  
                (Default) = reg_sz:  
                <GUID>    = reg_dword:  
                <GUID>    = reg_dword:  
                <GUID>    = reg_sz:  
```  

|Nome|Tipo|Dados|Descrição|  
|----------|----------|----------|-----------------|  
|(Padrão)|REG_SZ|Nenhum|Deixe em branco.|  
|*\<GUID &GT;*|REG_DWORD ou REG_SZ|0 ou uma cadeia de caracteres descritiva.|Opcional. Nome da entrada deve ser o GUID de um comando que exigem a visibilidade. O valor contém apenas uma cadeia de caracteres informativa. Normalmente, o valor é um `reg_dword` definido como 0.|  

### <a name="example"></a>Exemplo  

```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        8.0Exp\  
          ToolWindows\  
            {EEFA5220-E298-11D0-8F78-00A0C9110057}\  
              Visibility\  
                (Default) = reg_sz:  
                {93694fa0-0397-11d1-9f4e-00a0c911004f} = reg_dword: 0x00000000  
                {9DA22B82-6211-11d2-9561-00600818403B} = reg_dword: 0x00000000  
                {adfc4e66-0397-11d1-9f4e-00a0c911004f} = reg_dword: 0x00000000  
```  

## <a name="see-also"></a>Consulte também  
 [VSPackages](../extensibility/internals/vspackages.md)