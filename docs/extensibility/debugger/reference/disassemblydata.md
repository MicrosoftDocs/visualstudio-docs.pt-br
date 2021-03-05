---
description: Descreve uma instrução de desmontagem para o ambiente de desenvolvimento integrado (IDE) a ser exibido.
title: DisassemblyData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DisassemblyData
helpviewer_keywords:
- DisassemblyData structure
ms.assetid: 10e70aa7-9381-40d3-bdd1-d2cad78ef16c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b6053647d43563e7369793982c72683002ae0df5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170452"
---
# <a name="disassemblydata"></a>DisassemblyData
Descreve uma instrução de desmontagem para o ambiente de desenvolvimento integrado (IDE) a ser exibido.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct tagDisassemblyData {
    DISASSEMBLY_STREAM_FIELDS dwFields;
    BSTR                      bstrAddress;
    BSTR                      bstrAddressOffset;
    BSTR                      bstrCodeBytes;
    BSTR                      bstrOpcode;
    BSTR                      bstrOperands;
    BSTR                      bstrSymbol;
    UINT64                    uCodeLocationId;
    TEXT_POSITION             posBeg;
    TEXT_POSITION             posEnd;
    BSTR                      bstrDocumentUrl;
    DWORD                     dwByteOffset;
    DISASSEMBLY_FLAGS         dwFlags;
} DisassemblyData;
```

```csharp
public struct DisassemblyData { 
    public uint          dwFields;
    public string        bstrAddress;
    public string        bstrAddressOffset;
    public string        bstrCodeBytes;
    public string        bstrOpcode;
    public string        bstrOperands;
    public string        bstrSymbol;
    public ulong         uCodeLocationId;
    public TEXT_POSITION posBeg;
    public TEXT_POSITION posEnd;
    public string        bstrDocumentUrl;
    public uint          dwByteOffset;
    public uint          dwFlags;
};
```

## <a name="members"></a>Membros
`dwFields`\
A constante [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md) que especifica quais campos são preenchidos.

`bstrAddress`\
O endereço como um deslocamento de um ponto de partida (geralmente o início da função associada).

`bstrCodeBytes`\
Os bytes de código para esta instrução.

`bstrOpcode`\
O opcode desta instrução.

`bstrOperands`\
Os operandos para esta instrução.

`bstrSymbol`\
O nome do símbolo, se houver, associado ao endereço (símbolo público, rótulo e assim por diante).

`uCodeLocationId`\
O identificador de local de código para esta linha desmontada. Se o endereço de contexto de código de uma linha for maior do que o endereço de contexto de outro, o identificador de local de código desmontado da primeira também será maior que o identificador de local de código do segundo.

`posBeg`\
O [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) que corresponde à posição em um documento onde os dados de desmontagem são iniciados.

`posEnd`\
O [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) que corresponde à posição em um documento onde os dados de desmontagem são encerrados.

`bstrDocumentUrl`\
Para documentos de texto que podem ser representados como nomes de arquivo, o `bstrDocumentUrl` campo é preenchido com o nome do arquivo no qual a origem pode ser encontrada, usando o formato `file://file name` .

Para documentos de texto que não podem ser representados como nomes de arquivo, `bstrDocumentUrl` é um identificador exclusivo para o documento e o mecanismo de depuração deve implementar o método [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md) .

Esse campo também pode conter informações adicionais sobre somas de verificação. Consulte Comentários para obter detalhes.

`dwByteOffset`\
O número de bytes que a instrução é do início da linha de código.

`dwFlags`\
A constante [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md) que especifica quais sinalizadores estão ativos.

## <a name="remarks"></a>Comentários
Cada `DisassemblyData` estrutura descreve uma instrução de desmontagem. Uma matriz dessas estruturas é retornada do método [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) .

A estrutura de [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) é usada somente para documentos baseados em texto. O intervalo de código-fonte para essa instrução é preenchido apenas para a primeira instrução gerada a partir de uma instrução ou linha, por exemplo, quando `dwByteOffset == 0` .

Para documentos que não são textuais, um contexto de documento pode ser obtido do código e o `bstrDocumentUrl` campo deve ser um valor nulo. Se o `bstrDocumentUrl` campo for o mesmo que o `bstrDocumentUrl` campo no elemento da `DisassemblyData` matriz anterior, defina `bstrDocumentUrl` como um valor nulo.

Se o `dwFlags` campo tiver o `DF_DOCUMENT_CHECKSUM` sinalizador definido, as informações adicionais de soma de verificação seguirão a cadeia de caracteres apontada pelo `bstrDocumentUrl` campo. Especificamente, após o terminador de cadeia de caracteres nulo, segue um GUID que identifica o algoritmo de soma de verificação, que, por sua vez, é seguido por um valor de 4 bytes indicando o número de bytes na soma de verificação e que, por sua vez, é seguido pelos bytes de soma de verificação. Consulte o exemplo neste tópico sobre como codificar e decodificar esse campo no [!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)] .

## <a name="example"></a>Exemplo
O `bstrDocumentUrl` campo pode conter informações adicionais que não sejam uma cadeia de caracteres se o `DF_DOCUMENT_CHECKSUM` sinalizador for definido. O processo de criação e leitura dessa cadeia de caracteres codificada é simples no [!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)] . No entanto, no [!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)] , é outra questão. Para aqueles que são curiosos, o exemplo a seguir mostra uma maneira de criar a cadeia de caracteres codificada de [!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)] e uma maneira de decodificar a cadeia de caracteres codificada [!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)] .

```csharp
using System;
using System.Runtime.InteropServices;

namespace MyNamespace
{
    class MyClass
    {
        string EncodeData(string documentString,
                          Guid checksumGuid,
                          byte[] checksumData)
        {
            string returnString = documentString;

            if (checksumGuid == null || checksumData == null)
            {
                // Nothing more to do. Just return the string.
                return returnString;
            }

            returnString += '\0'; // separating null value

            // Add checksum GUID to string.
            byte[] guidDataArray  = checksumGuid.ToByteArray();
            int    guidDataLength = guidDataArray.Length;
            IntPtr pBuffer        = Marshal.AllocCoTaskMem(guidDataLength);
            for (int i = 0; i < guidDataLength; i++)
            {
                Marshal.WriteByte(pBuffer, i, guidDataArray[i]);
            }
            // Copy guid data bytes to string as wide characters.
            // Assumption: sizeof(char) == 2.
            for (int i = 0; i < guidDataLength / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }

            // Add checksum count (a 32-bit value).
            Int32 checksumCount = checksumData.Length;
            Marshal.StructureToPtr(checksumCount, pBuffer, true);
            for (int i = 0; i < sizeof(Int32) / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }

            // Add checksum data.
            pBuffer = Marshal.AllocCoTaskMem(checksumCount);
            for (int i = 0; i < checksumCount; i++)
            {
                Marshal.WriteByte(pBuffer, i, checksumData[i]);
            }
            for (int i = 0; i < checksumCount / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }
            Marshal.FreeCoTaskMem(pBuffer);

            return returnString;
        }

        void DecodeData(    string encodedString,
                        out string documentString,
                        out Guid   checksumGuid,
                        out byte[] checksumData)
        {
            documentString = String.Empty;
            checksumGuid = Guid.Empty;
            checksumData = null;

            IntPtr pBuffer = Marshal.StringToBSTR(encodedString);
            if (null != pBuffer)
            {
                int bufferOffset = 0;

                // Parse string out. String is assumed to be Unicode.
                documentString = Marshal.PtrToStringUni(pBuffer);
                bufferOffset += (documentString.Length + 1) * sizeof(char);

                // Parse Guid out.
                // Read guid bytes from buffer and store in temporary
                // buffer that contains only the guid bytes. Then the
                // Marshal.PtrToStructure() can work properly.
                byte[] guidDataArray  = checksumGuid.ToByteArray();
                int    guidDataLength = guidDataArray.Length;
                IntPtr pGuidBuffer    = Marshal.AllocCoTaskMem(guidDataLength);
                for (int i = 0; i < guidDataLength; i++)
                {
                    Marshal.WriteByte(pGuidBuffer, i,
                                      Marshal.ReadByte(pBuffer, bufferOffset + i));
                }
                bufferOffset += guidDataLength;
                checksumGuid = (Guid)Marshal.PtrToStructure(pGuidBuffer, typeof(Guid));
                Marshal.FreeCoTaskMem(pGuidBuffer);

                // Parse out the number of checksum data bytes (always 32-bit value).
                int dataCount = Marshal.ReadInt32(pBuffer, bufferOffset);
                bufferOffset += sizeof(Int32);

                // Parse out the checksum data.
                checksumData = new byte[dataCount];
                for (int i = 0; i < dataCount; i++)
                {
                    checksumData[i] = Marshal.ReadByte(pBuffer, bufferOffset + i);
                }
            }
        }
    }
}
```

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [Ler](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
