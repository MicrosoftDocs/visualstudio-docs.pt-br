---
title: Atributos condicionais do esquema XML do VSCT | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 071f13420fe9482e99189ca29eeb09d319f182bf
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49936414"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>Atributos condicionais do esquema XML do VSCT
Você pode aplicar atributos condicionais para todas as listas e itens. Operadores lógicos e expressões de expansão de símbolo avaliadas como true ou false. Se for true, a lista associada ou o item será incluído na saída resultante.  
  
 Você pode testar as expansões de token em relação a outras expansões de token ou constantes. A função `Defined()` testa se um determinado nome tiver sido definido, mesmo se ele não tem nenhum valor.  
  
 Quando um atributo Condition é aplicado a uma lista, a condição é aplicada a todos os elementos filho na lista. Se um elemento filho em si contém um atributo Condition, sua condição é combinada com a expressão pai por uma operação AND.  
  
 Os valores 1, '1' e 'true' são avaliados como true e 0, '0' e 'false' são avaliadas como false.  
  
## <a name="operators"></a>Operadores  
 Use os operadores a seguir para avaliar expressões condicionais.  
  
|Operador|Definição|  
|--------------|----------------|  
|(,)|Agrupamento|  
|!|Não lógico|  
|\<, >, \<=, >=, ==, !=|Relacional e igualdade|  
|e|Boolean|  
|ou|Boolean|  
  
## <a name="examples"></a>Exemplos  
  
```xml  
<Menu Condition="Defined(DEBUG)" ...  
</Menu>  
  
<Menu Condition="%(SKU_MODE) = 'Demo'" ...  
</Menu>  
  
<Menus Condition="Defined(DEBUG)">  
    <Menu ...  
    </Menu>  
</Menus>  
  
<Menus Condition="Defined(DEMO_SKU)">  
    <Menus Condition="!Defined(DEBUG)">  
        <Menu ...  
        </Menu>  
    </Menus>  
  
    <Menu ...  
    </Menu>  
</Menus>  
  
<Menus Condition="(Defined(DEMO_SKU) or Defined(SAMPLE_SKU))   
and !Defined(DEBUG)">  
    <Menu ...  
    </Menu>  
</Menus>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tabela de comando do Visual Studio (. Arquivos de VSCT)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)