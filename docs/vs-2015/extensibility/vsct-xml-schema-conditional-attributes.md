---
title: Atributos condicionais do esquema XML do VSCT | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
caps.latest.revision: 6
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9524f1306c86f110498d71d4057378cd834d207b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817237"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>Atributos condicionais do esquema XML do VSCT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Atributos condicionais podem ser aplicados a todas as listas e itens. Operadores lógicos e expressões de expansão de símbolo avaliadas como true ou false. Se for true, a lista associada ou o item será incluído na saída resultante.  
  
 Expansões de token podem ser testados em relação a outras expansões de token ou constantes. A função Defined é usada para testar se um determinado nome tiver sido definido, mesmo se ele não tem nenhum valor.  
  
 Quando um atributo Condition é aplicado a uma lista, a condição é aplicada a todos os elementos filho na lista. Se um elemento filho em si contém um atributo Condition, sua condição é combinada com a expressão pai por uma operação AND.  
  
 Os valores 1, '1' e 'true' são avaliados como true e 0, '0' e 'false' são avaliadas como false.  
  
## <a name="operators"></a>Operadores  
 Os operadores a seguir podem ser usados para avaliar expressões condicionais.  
  
|Operador|Definição|  
|--------------|----------------|  
|(,)|Agrupamento|  
|!|Não lógico|  
|\<, >, \<=, >=, ==, !=|Relacional e igualdade|  
|e|Boolean|  
|ou|Boolean|  
  
## <a name="examples"></a>Exemplos  
  
```  
<Menu Condition="Defined(DEBUG)" …  
</Menu>  
  
<Menu Condition="%(SKU_MODE) = 'Demo'" …  
</Menu>  
  
<Menus Condition="Defined(DEBUG)">  
    <Menu …  
    </Menu>  
</Menus>  
  
<Menus Condition="Defined(DEMO_SKU)">  
    <Menus Condition="!Defined(DEBUG)">  
        <Menu …  
        </Menu>  
    </Menus>  
  
    <Menu …  
    </Menu>  
</Menus>  
  
<Menus Condition="(Defined(DEMO_SKU) or Defined(SAMPLE_SKU))   
and !Defined(DEBUG)">  
    <Menu …  
    </Menu>  
</Menus>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

