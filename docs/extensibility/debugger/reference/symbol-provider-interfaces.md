---
title: Interfaces de provedor de símbolo | Microsoft Docs
description: Este artigo fornece links para descrições das interfaces de tratamento de símbolo do SDK do Visual Studio, que avaliam variáveis em uma pilha de chamadas durante o modo de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- interfaces, symbol handler
- symbol handler, interfaces
- symbol handler, evaluating variables
ms.assetid: 4201f10e-c9f7-4b38-bb45-40fe0082d5bf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7be44c623f93d9ecc4f9f5d4488c462ed8a9969d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061427"
---
# <a name="symbol-provider-interfaces"></a>Interfaces de provedor de símbolos
A seguir estão as interfaces de tratamento de símbolos para o [!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)] .

## <a name="discussion"></a>Discussão
 Essas interfaces são usadas para avaliar variáveis em uma pilha de chamadas durante o modo de interrupção. Eles são implementados somente para Common Language Runtime provedores de símbolo (SP).

|Interface|Implementado por|Descrição|
|---------------|--------------------|-----------------|
|[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)|SP|Representa o endereço de um item.|
|[IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)|SP|Representa o endereço de um item, fornecendo acesso à ID do processo.|
|[IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)|SP|Representa um símbolo de matriz ou tipo de matriz.|
|[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)|SP|Representa um símbolo de classe ou tipo de classe.|
|[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)|SP|Representa um provedor de símbolos COM+ com métodos que são específicos do código gerenciado.|
|[IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)|SP|Representa um provedor de símbolos COM+ com métodos que são específicos do código gerenciado e estende o **IDebugComPlusSymbolProvider**.|
|[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)|SP|Representa um símbolo ou tipo que é um contêiner para outros símbolos ou tipos.|
|[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)|SP|Representa um atributo personalizado que pode ser anexado a um símbolo.|
|[IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)|SP|Representa uma consulta de atributos personalizados em um método ou tipo.|
|[IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)|SP|Fornece acesso a atributos personalizados em um símbolo.|
|[IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md)|SP|A interface base para qualquer tipo que possa ser determinado em tempo de execução.|
|[IDebugDynamicFieldCOMPlus](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus.md)|SP|Representa um campo dinâmico para um objeto [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) .|
|[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)|SP|Representa um tipo de enumeração.|
|[IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)|SP3|Estende os tipos de campos disponíveis para dar suporte a genéricos de código gerenciado.|
|[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)|SP|A classe base para todos os campos; representa uma descrição de um símbolo ou tipo.|
|[IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)|SP|Representa a definição de um campo para um tipo genérico de código gerenciado.|
|[IDebugGenericFieldInstance](../../../extensibility/debugger/reference/idebuggenericfieldinstance.md)|SP|Representa uma instância de um campo para um tipo genérico de código gerenciado.|
|[IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)|SP|Representa um parâmetro para um tipo genérico de código gerenciado.|
|[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)|SP|Representa um método.|
|[IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)|SP|Representa um modificador opcional de depuração.|
|[IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)|SP|Representa um ponteiro.|
|[IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)|SP|Representa um valor de enumeração de tipo primitivo de uma interface [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) .|
|[IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)|SP|Representa uma propriedade de uma classe de código gerenciado que pode ser get ou set.|
|[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)|SP|Representa um provedor de símbolos que fornece símbolos e tipos.|
|[IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)|SP|Representa um provedor de símbolos com acesso direto a metadados e interfaces de símbolo de núcleo.|
|[IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)|SP|Representa a capacidade de criar um campo que representa um tipo.|
|[IDebugTypeFieldBuilder2](../../../extensibility/debugger/reference/idebugtypefieldbuilder2.md)|SP|Estende o **IDebugTypeFieldBuilder** para poder criar tipos de matriz.|
|[IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)|SP|Representa uma coleção de objetos [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) .|
|[IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)|SP|Representa uma coleção de objetos [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md) .|
|[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)|SP|Representa uma coleção de objetos [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) .|

## <a name="see-also"></a>Confira também
- [Referência da API](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
