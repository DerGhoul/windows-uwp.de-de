---
title: Kopieren in und aus Bytearrays
description: Dieser Beispielcode zeigt, wie Sie in und aus Bytearrays in einer UWP (Universelle Windows-Plattform)-App kopieren können.
ms.assetid: C343B08C-1FA1-40FD-8CA5-7FC9B707C5E3
author: msatranjr
ms.author: misatran
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, Uwp, Sicherheit
ms.localizationpriority: medium
ms.openlocfilehash: cc7119ba2d97bfc6e1fb3f1a519b6d650027b1a3
ms.sourcegitcommit: f2f4820dd2026f1b47a2b1bf2bc89d7220a79c1a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2018
ms.locfileid: "2786712"
---
# <a name="copy-to-and-from-byte-arrays"></a>Kopieren in und aus Bytearrays



Dieser Beispielcode zeigt, wie Sie in und aus Bytearrays in einer UWP (Universelle Windows-Plattform)-App kopieren können.

```cs
public void ByteArrayCopy()
{
    // Initialize a byte array.
    byte[] bytes = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    // Create a buffer from the byte array.
    IBuffer buffer = CryptographicBuffer.CreateFromByteArray(bytes);

    // Encode the buffer into a hexadecimal string (for display);
    string hex = CryptographicBuffer.EncodeToHexString(buffer);

    // Copy the buffer back into a new byte array.
    byte[] newByteArray;
    CryptographicBuffer.CopyToByteArray(buffer, out newByteArray);
}
```