---
author: stevewhims
description: In diesem Thema verwendet eine vollständige Codebeispiel Direct2D um zu veranschaulichen, wie C + verwenden / WinRT COM-Klassen und Schnittstellen verwenden.
title: Nutzen von DirectX und andere COM-APIs mit C + / WinRT
ms.author: stwhi
ms.date: 07/23/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, Uwp, Standard, c ++, Cpp, Winrt, COM, Komponente, Klasse, Schnittstelle
ms.localizationpriority: medium
ms.openlocfilehash: b87eb90ed5ecf731cc851e81e81ad016956e5fea
ms.sourcegitcommit: f2f4820dd2026f1b47a2b1bf2bc89d7220a79c1a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2018
ms.locfileid: "2800071"
---
# <a name="consume-directx-and-other-com-apis-with-cwinrtwindowsuwpcpp-and-winrt-apisintro-to-using-cpp-with-winrt"></a>Nutzen von DirectX und andere COM-APIs mit [C + / WinRT](/windows/uwp/cpp-and-winrt-apis/intro-to-using-cpp-with-winrt)

Sie können die Funktionen von C + / WinRT-Bibliothek mit COM-Komponenten, beispielsweise die leistungsfähige 2D-Diagramme und 3-d-Grafiken der DirectX-APIs nutzen. C + / WinRT ist die einfachste Möglichkeit zum DirectX verwenden, ohne dass die Leistung beeinträchtigt. In diesem Thema wird ein Codebeispiel Direct2D um zu veranschaulichen, wie C + verwenden / WinRT COM-Klassen und Schnittstellen verwenden. Sie können natürlich COM und Windows-Runtime-Programmierung innerhalb der gleichen C + mischen / WinRT-Projekt.

Am Ende dieses Themas finden Sie eine vollständige Quelle Codebeispiel einer minimalen Direct2D-Anwendung. Wir heben Sie Auszüge aus Anleitung zu dieser Code und deren Verwendung zum Veranschaulichen der COM-Komponenten, die mit C + nutzen / WinRT mithilfe verschiedener Funktionen der C + / WinRT-Bibliothek.

## <a name="com-smart-pointers-winrtcomptruwpcpp-ref-for-winrtcom-ptr"></a>Com-intelligenten Zeigern ([**winrt::com_ptr**](/uwp/cpp-ref-for-winrt/com-ptr))

Beim Programmieren mit COM, arbeiten Sie direkt mit Schnittstellen und nicht mit Objekten (das auch im Hintergrund für Windows-Runtime-APIs, die eine Weiterentwicklung von COM sind true). Um eine Funktion für eine COM-Klasse aufrufen, beispielsweise Sie aktivieren die Klasse eine Schnittstelle zurück, und rufen Sie dann Sie Funktionen über diese Schnittstelle. Um den Zustand eines Objekts zuzugreifen, zugreifen nicht Sie Datenelemente direkt. Rufen Sie stattdessen Accessor und Mutator Funktionen auf einer Schnittstelle.

Um bestimmte sein, sprechen wir zur Interaktion mit Schnittstelle *Zeiger*. Und, wir das Vorhandensein des Typs COM intelligenten Zeiger in C + Kommunikationsmittel / WinRT&mdash;der [**winrt::com_ptr**](/uwp/cpp-ref-for-winrt/com-ptr) -Typ.

```cppwinrt
winrt::com_ptr<ID2D1Factory1> factory;
```

Der oben angegebenen Code veranschaulicht, wie einen nicht initialisierten intelligenten Zeiger auf eine [**ID2D1Factory1**](https://msdn.microsoft.com/library/Hh404596) COM-Schnittstelle deklariert. Der intelligente Zeiger ist nicht initialisiert, sodass es noch nicht auf eine **ID2D1Factory1** -Schnittstelle, die kein tatsächliche Objekt weist (es ist nicht auf eine Schnittstelle in allen verweisen) gehören. Es besitzt die potenzielle Möglichkeit dazu jedoch. und (wird ein intelligente Zeiger) die Möglichkeit, über den COM-Verweis zur Verwaltung der Lebensdauer der das übergeordnete Objekt der Schnittstelle, die darauf verweist, und das Medium mit dem Sie die Funktionen für diese Schnittstelle aufrufen zählen hat.

## <a name="com-functions-that-return-an-interface-pointer-as-void"></a>COM-Funktionen, die einen Schnittstellenzeiger als zurückgeben **Void\ * \ ***

Sie können die Funktion [**com_ptr::put_void**](/uwp/cpp-ref-for-winrt/com-ptr#comptrputvoid-function) zum Schreiben in eines nicht initialisierten intelligenten Zeigers zugrunde liegende unformatierten Zeiger aufrufen.

```cppwinrt
D2D1CreateFactory(
    D2D1_FACTORY_TYPE_SINGLE_THREADED,
    __uuidof(factory),
    &options,
    factory.put_void()
);
```

Der oben angegebenen Code Ruft die [**D2D1CreateFactory**](/windows/desktop/api/d2d1/nf-d2d1-d2d1createfactory) -Funktion, die einen **ID2D1Factory1** Schnittstellenzeiger über den letzten Parameter zurückgibt hat **Void\ * \ *** Typ. Viele COM-Funktionen zurückgeben einer **Void\ * \ ***. Verwenden Sie für solche Funktionen [**com_ptr::put_void**](/uwp/cpp-ref-for-winrt/com-ptr#comptrputvoid-function) wie dargestellt.

## <a name="com-functions-that-return-a-specific-interface-pointer"></a>COM-Funktionen, die einen bestimmten Schnittstellenzeiger zurückgeben

Die [**D3D11CreateDevice**](/windows/desktop/api/dwrite/nf-dwrite-dwritecreatefactory) -Funktion gibt einen [**ID3D11Device**](https://msdn.microsoft.com/library/Hh404596) Schnittstelle-Zeiger über seinen antepenultimate Parameter, der hat **ID3D11Device\ * \ *** Typ. Verwenden Sie für Funktionen, die einen bestimmten Schnittstellenzeiger wie zurückzugeben [**com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#comptrput-function).

```cppwinrt
winrt::com_ptr<ID3D11Device> device;
D3D11CreateDevice(
    ...
    device.put(),
    ...);
```

Im Codebeispiel im Abschnitt vor dieser zeigt, wie die Rohdaten **D2D1CreateFactory** -Funktion aufgerufen. Jedoch können Sie sogar wenn im Codebeispiel zu diesem Thema **D2D1CreateFactory**aufruft, Hilfsprogramm-Funktionsvorlage, die umbrochen die unformatierte API wird verwendet, und daher im Codebeispiel [**com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#comptrput-function)tatsächlich verwendet.

```cppwinrt
winrt::com_ptr<ID2D1Factory1> factory;
D2D1CreateFactory(
    D2D1_FACTORY_TYPE_SINGLE_THREADED,
    options,
    factory.put());
```

## <a name="com-functions-that-return-an-interface-pointer-as-iunknown"></a>COM-Funktionen, die einen Schnittstellenzeiger als zurückgeben **IUnknown\ * \ ***

Die [**DWriteCreateFactory**](/windows/desktop/api/dwrite/nf-dwrite-dwritecreatefactory) -Funktion gibt einen DirectWrite Factory Schnittstelle-Zeiger über seinen letzten Parameter, der hat **IUnknown\ * \ *** Typ. Verwenden Sie für eine Funktion, [**com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#comptrput-function), aber Neuinterpretation umgewandelt, um **IUnknown\ * \ ***.

```cppwinrt
DWriteCreateFactory(
    DWRITE_FACTORY_TYPE_SHARED,
    __uuidof(dwriteFactory2),
    reinterpret_cast<IUnknown**>(dwriteFactory2.put()));
```

## <a name="re-seat-a-winrtcomptr"></a>Setzen Sie erneut eine **winrt::com_ptr**

> [!IMPORTANT]
> Wenn Sie über eine [**winrt::com_ptr**](/uwp/cpp-ref-for-winrt/com-ptr) verfügen, die bereits sitzt (seine interne unformatierte Zeiger hat bereits eine Ziel) Sie es so zeigen Sie auf ein anderes Objekt erneut setzen möchten, und Sie müssen zuerst zuweisen `nullptr` darauf&mdash;wie im folgenden Codebeispiel gezeigt. Wenn dies nicht der Fall, klicken Sie dann zeichnet ein bereits angeschlossene **Com_ptr** das Problem an Ihre Aufmerksamkeit (Wenn Sie [**com_ptr::put**](/uwp/cpp-ref-for-winrt/com-ptr#comptrput-function) oder [**com_ptr::put_void**](/uwp/cpp-ref-for-winrt/com-ptr#comptrputvoid-function)aufrufen) durch die Assertion, dass seine interne Zeiger nicht null ist.

```cppwinrt
winrt::com_ptr<ID2D1SolidColorBrush> brush;
...
    brush.put()
...
brush = nullptr; // Important because we're about to re-seat
target->CreateSolidColorBrush(
    color_orange,
    D2D1::BrushProperties(0.8f),
    brush.put()));
```

## <a name="handle-hresult-error-codes"></a>Behandeln von HRESULT-Fehlercodes

Um zu überprüfen, dass der Wert der ein HRESULT von einer COM-Funktion zurückgegeben und löst eine Ausnahme aus, wenn es sich um ein Fehlercode darstellt, rufen Sie [**winrt::check_hresult**](/uwp/cpp-ref-for-winrt/error-handling/check-hresult).

```cppwinrt
winrt::check_hresult(D2D1CreateFactory(
    D2D1_FACTORY_TYPE_SINGLE_THREADED,
    __uuidof(factory),
    options,
    factory.put_void()));
```

## <a name="com-functions-that-take-a-specific-interface-pointer"></a>COM-Funktionen, die einen bestimmten Schnittstellenzeiger verwenden

Sie können die [**com_ptr::get**](/uwp/cpp-ref-for-winrt/com-ptr#comptrget-function) -Funktion, um Ihre **Com_ptr** auf eine Funktion zu übergeben, die einen bestimmten Schnittstellenzeiger des gleichen Typs akzeptiert aufrufen.

```cppwinrt
... ExampleFunction(
    winrt::com_ptr<ID2D1Factory1> const& factory,
    winrt::com_ptr<IDXGIDevice> const& dxdevice)
{
    ...
    winrt::check_hresult(factory->CreateDevice(dxdevice.get(), ...));
    ...
}
```

## <a name="com-functions-that-take-an-iunknown-interface-pointer"></a>COM-Funktionen, die einen **IUnknown** -Schnittstellenzeiger verwenden

Sie können die kostenlose [**winrt::get_unknown**](/uwp/cpp-ref-for-winrt/windows-foundation-iunknown#getunknown-function) -Funktion, um Ihre **Com_ptr** auf eine Funktion zu übergeben, die einen **IUnknown** -Schnittstellenzeiger akzeptiert aufrufen.

```cppwinrt
winrt::check_hresult(factory->CreateSwapChainForCoreWindow(
    ...
    winrt::get_unknown(CoreWindow::GetForCurrentThread()),
    ...));
```

## <a name="passing-and-returning-com-smart-pointers"></a>Übergeben und Zurückgeben von COM intelligente Zeiger

Eine Funktion, die einen COM-intelligenten Zeiger in Form einer **winrt::com_ptr** sollten von Konstanten Verweis oder per Verweis tun.

```cppwinrt
... GetDxgiFactory(winrt::com_ptr<ID3D11Device> const& device) ...

... CreateDevice(..., winrt::com_ptr<ID3D11Device>& device) ...
```

Eine Funktion, die ein **winrt::com_ptr** gibt sollte vom Wert dazu.

```cppwinrt
winrt::com_ptr<ID2D1Factory1> CreateFactory() ...
```

## <a name="query-a-com-smart-pointer-for-a-different-interface"></a>Abfrage einer COM intelligenten Zeiger für eine andere Schnittstelle

Die [**com_ptr::as**](/uwp/cpp-ref-for-winrt/com-ptr#comptras-function) -Funktion können Sie einen COM-intelligenten Zeiger für eine andere Schnittstelle Abfragen. Die Funktion löst eine Ausnahme aus, wenn die Abfrage nicht erfolgreich.

```cppwinrt
void ExampleFunction(winrt::com_ptr<ID3D11Device> const& device)
{
    ...
    winrt::com_ptr<IDXGIDevice> const dxdevice{ device.as<IDXGIDevice>() };
    ...
}
```

Verwenden Sie alternativ [**com_ptr::try_as**](/uwp/cpp-ref-for-winrt/com-ptr#comptrtryas-function), die einen Wert, die Sie können zurückgibt, gegen überprüfen `nullptr` um festzustellen, ob die Abfrage erfolgreich war.

## <a name="full-source-code-listing-of-a-minimal-direct2d-application"></a>Vollständige Quelle Codebeispiel einer minimalen Direct2D-Anwendung

Wenn Sie erstellen und dieser Quelle Codebeispiel wird anschließend die erste, in Visual Studio ausführen möchten, erstellen Sie ein neues **Kern (C + / WinRT)**. `Direct2D` ein kürzeren Namen für das Projekt ist, aber Sie können nennen Sie sie nichts anderes. Open `App.cpp`, löschen Sie den gesamten Inhalt, und fügen Sie in der Liste unten.

```cppwinrt
#include "pch.h"

using namespace winrt;

using namespace Windows;
using namespace Windows::ApplicationModel::Core;
using namespace Windows::UI;
using namespace Windows::UI::Core;
using namespace Windows::Graphics::Display;

namespace
{
    winrt::com_ptr<ID2D1Factory1> CreateFactory()
    {
        D2D1_FACTORY_OPTIONS options{};

#ifdef _DEBUG
        options.debugLevel = D2D1_DEBUG_LEVEL_INFORMATION;
#endif

        winrt::com_ptr<ID2D1Factory1> factory;

        winrt::check_hresult(D2D1CreateFactory(
            D2D1_FACTORY_TYPE_SINGLE_THREADED,
            options,
            factory.put()));

        return factory;
    }

    HRESULT CreateDevice(D3D_DRIVER_TYPE const type, winrt::com_ptr<ID3D11Device>& device)
    {
        WINRT_ASSERT(!device);

        return D3D11CreateDevice(
            nullptr,
            type,
            nullptr,
            D3D11_CREATE_DEVICE_BGRA_SUPPORT,
            nullptr, 0,
            D3D11_SDK_VERSION,
            device.put(),
            nullptr,
            nullptr);
    }

    winrt::com_ptr<ID3D11Device> CreateDevice()
    {
        winrt::com_ptr<ID3D11Device> device;
        HRESULT hr{ CreateDevice(D3D_DRIVER_TYPE_HARDWARE, device) };

        if (DXGI_ERROR_UNSUPPORTED == hr)
        {
            hr = CreateDevice(D3D_DRIVER_TYPE_WARP, device);
        }

        winrt::check_hresult(hr);
        return device;
    }

    winrt::com_ptr<ID2D1DeviceContext> CreateRenderTarget(
        winrt::com_ptr<ID2D1Factory1> const& factory,
        winrt::com_ptr<ID3D11Device> const& device)
    {
        WINRT_ASSERT(factory);
        WINRT_ASSERT(device);

        winrt::com_ptr<IDXGIDevice> const dxdevice{ device.as<IDXGIDevice>() };

        winrt::com_ptr<ID2D1Device> d2device;
        winrt::check_hresult(factory->CreateDevice(dxdevice.get(), d2device.put()));

        winrt::com_ptr<ID2D1DeviceContext> target;
        winrt::check_hresult(d2device->CreateDeviceContext(D2D1_DEVICE_CONTEXT_OPTIONS_NONE, target.put()));
        return target;
    }

    winrt::com_ptr<IDXGIFactory2> GetDxgiFactory(winrt::com_ptr<ID3D11Device> const& device)
    {
        WINRT_ASSERT(device);

        winrt::com_ptr<IDXGIDevice> const dxdevice{ device.as<IDXGIDevice>() };

        winrt::com_ptr<IDXGIAdapter> adapter;
        winrt::check_hresult(dxdevice->GetAdapter(adapter.put()));

        winrt::com_ptr<IDXGIFactory2> factory;
        winrt::check_hresult(adapter->GetParent(__uuidof(factory), factory.put_void()));
        return factory;
    }

    void CreateDeviceSwapChainBitmap(
        winrt::com_ptr<IDXGISwapChain1> const& swapchain,
        winrt::com_ptr<ID2D1DeviceContext> const& target)
    {
        WINRT_ASSERT(swapchain);
        WINRT_ASSERT(target);

        winrt::com_ptr<IDXGISurface> surface;
        winrt::check_hresult(swapchain->GetBuffer(0, __uuidof(surface), surface.put_void()));

        D2D1_BITMAP_PROPERTIES1 const props{ D2D1::BitmapProperties1(
            D2D1_BITMAP_OPTIONS_TARGET | D2D1_BITMAP_OPTIONS_CANNOT_DRAW,
            D2D1::PixelFormat(DXGI_FORMAT_B8G8R8A8_UNORM, D2D1_ALPHA_MODE_IGNORE)) };

        winrt::com_ptr<ID2D1Bitmap1> bitmap;

        winrt::check_hresult(target->CreateBitmapFromDxgiSurface(surface.get(),
            props,
            bitmap.put()));

        target->SetTarget(bitmap.get());
    }

    winrt::com_ptr<IDXGISwapChain1> CreateSwapChainForCoreWindow(winrt::com_ptr<ID3D11Device> const& device)
    {
        WINRT_ASSERT(device);

        winrt::com_ptr<IDXGIFactory2> const factory{ GetDxgiFactory(device) };

        DXGI_SWAP_CHAIN_DESC1 props{};
        props.Format = DXGI_FORMAT_B8G8R8A8_UNORM;
        props.SampleDesc.Count = 1;
        props.BufferUsage = DXGI_USAGE_RENDER_TARGET_OUTPUT;
        props.BufferCount = 2;
        props.SwapEffect = DXGI_SWAP_EFFECT_FLIP_SEQUENTIAL;

        winrt::com_ptr<IDXGISwapChain1> swapChain;

        winrt::check_hresult(factory->CreateSwapChainForCoreWindow(
            device.get(),
            winrt::get_unknown(CoreWindow::GetForCurrentThread()),
            &props,
            nullptr, // all or nothing
            swapChain.put()));

        return swapChain;
    }

    constexpr D2D1_COLOR_F color_white{ 1.0f,  1.0f,  1.0f,  1.0f };
    constexpr D2D1_COLOR_F color_orange{ 0.92f,  0.38f,  0.208f,  1.0f };
}

struct App : implements<App, IFrameworkViewSource, IFrameworkView>
{
    winrt::com_ptr<ID2D1Factory1> m_factory;
    winrt::com_ptr<ID2D1DeviceContext> m_target;
    winrt::com_ptr<IDXGISwapChain1> m_swapChain;
    winrt::com_ptr<ID2D1SolidColorBrush> m_brush;
    float m_dpi{};

    IFrameworkView CreateView()
    {
        return *this;
    }

    void Initialize(CoreApplicationView const&)
    {
    }

    void Load(hstring const&)
    {
        CoreWindow const window{ CoreWindow::GetForCurrentThread() };

        window.SizeChanged([&](auto&&...)
        {
            if (m_target)
            {
                ResizeSwapChainBitmap();
                Render();
            }
        });

        DisplayInformation const display{ DisplayInformation::GetForCurrentView() };
        m_dpi = display.LogicalDpi();

        display.DpiChanged([&](DisplayInformation const& display, IInspectable const&)
        {
            if (m_target)
            {
                m_dpi = display.LogicalDpi();
                m_target->SetDpi(m_dpi, m_dpi);
                CreateDeviceSizeResources();
                Render();
            }
        });

        m_factory = CreateFactory();
        CreateDeviceIndependentResources();
    }

    void Uninitialize()
    {
    }

    void Run()
    {
        CoreWindow const window{ CoreWindow::GetForCurrentThread() };
        window.Activate();

        Render();
        CoreDispatcher const dispatcher{ window.Dispatcher() };
        dispatcher.ProcessEvents(CoreProcessEventsOption::ProcessUntilQuit);
    }

    void SetWindow(CoreWindow const&) {}

    void Draw()
    {
        m_target->Clear(color_white);

        D2D1_SIZE_F const size{ m_target->GetSize() };
        D2D1_RECT_F const rect{ 100.0f, 100.0f, size.width - 100.0f, size.height - 100.0f };
        m_target->DrawRectangle(rect, m_brush.get(), 100.0f);

        WINRT_TRACE("Draw %.2f x %.2f @ %.2f\n", size.width, size.height, m_dpi);
    }

    void Render()
    {
        if (!m_target)
        {
            winrt::com_ptr<ID3D11Device> const device{ CreateDevice() };
            m_target = CreateRenderTarget(m_factory, device);
            m_swapChain = CreateSwapChainForCoreWindow(device);

            CreateDeviceSwapChainBitmap(m_swapChain, m_target);

            m_target->SetDpi(m_dpi, m_dpi);

            CreateDeviceResources();
            CreateDeviceSizeResources();
        }

        m_target->BeginDraw();
        Draw();
        m_target->EndDraw();

        HRESULT const hr{ m_swapChain->Present(1, 0) };

        if (S_OK != hr && DXGI_STATUS_OCCLUDED != hr)
        {
            ReleaseDevice();
        }
    }

    void ReleaseDevice()
    {
        m_target = nullptr;
        m_swapChain = nullptr;

        ReleaseDeviceResources();
    }

    void ResizeSwapChainBitmap()
    {
        WINRT_ASSERT(m_target);
        WINRT_ASSERT(m_swapChain);

        m_target->SetTarget(nullptr);

        if (S_OK == m_swapChain->ResizeBuffers(0, // all buffers
            0, 0, // client area
            DXGI_FORMAT_UNKNOWN, // preserve format
            0)) // flags
        {
            CreateDeviceSwapChainBitmap(m_swapChain, m_target);
            CreateDeviceSizeResources();
        }
        else
        {
            ReleaseDevice();
        }
    }

    void CreateDeviceIndependentResources()
    {
    }

    void CreateDeviceResources()
    {
        winrt::check_hresult(m_target->CreateSolidColorBrush(
            color_orange,
            D2D1::BrushProperties(0.8f),
            m_brush.put()));
    }

    void CreateDeviceSizeResources()
    {
    }

    void ReleaseDeviceResources()
    {
        m_brush = nullptr;
    }
};

int __stdcall wWinMain(HINSTANCE, HINSTANCE, PWSTR, int)
{
    CoreApplication::Run(App());
}
```

## <a name="important-apis"></a>Wichtige APIs
* [WinRT::check_hresult](/uwp/cpp-ref-for-winrt/error-handling/check-hresult)
* [winrt::com_ptr](/uwp/cpp-ref-for-winrt/com-ptr)
* [winrt::Windows::Foundation::IUnknown-Struktur](/uwp/cpp-ref-for-winrt/windows-foundation-iunknown)