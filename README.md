# MetaMask.Blazor
Use MetaMask with Blazor WebAssembly

This library provides an easy helper to use MetaMask with Blazor WebAssembly.

**[Live Demo](https://michielpost.github.io/MetaMask.Blazor/)**

Real world implementation, login with MetaMask: [SkyDocs](https://github.com/michielpost/SkyDocs/)

## How to use
See included Blazor sample app.

Install: [MetaMask.Blazor on NuGet](https://www.nuget.org/packages/MetaMask.Blazor/)

Register in `Program.cs`:
```cs
builder.Services.AddMetaMaskBlazor();
```

Inject the `MetaMaskService` in your Razor page
```cs
@using MetaMask.Blazor
@inject IMetaMaskService MetaMaskService
```

or class when using a .razor.cs file:
```cs
[Inject]
public IMetaMaskService MetaMaskService { get; set; } = default!;
```

Use the `MetaMaskService`:

Check if the user has MetaMask installed:
```cs
bool hasMetaMask = await MetaMaskService.HasMetaMask();
```

Check if the user has previously connected to your site.
```cs
bool isSiteConnected = await MetaMaskService.IsSiteConnected();
```

Initialize a new connection with MetaMask
```cs
try
{
    await MetaMaskService.ConnectMetaMask();
}
catch (UserDeniedException)
{
   //Handle "User Denied" case;
}
```
This can throw exceptions if the user decides to not allow the connection.

Once there is a connection, you can use other method calls like:
- `GetSelectedAddress`
- `GetTransactionCount`
- `SignTypedData`
- `SendTransaction`
- or use the generic RPC method: `GenericRpc`

### Events
Listen to events:
 `await MetaMaskService.ListenToEvents();`

You can subscribe to two events:
- `IMetaMaskService.AccountChangedEvent`
- `IMetaMaskService.NetworkChangedEvent`


## Reference
- https://docs.metamask.io
- https://metamask.io
- [Logging in with MetaMask in a Blazor WebAssembly app](https://www.michielpost.nl/posts/logging-in-with-metamask-in-a-blazor-webassembly-app)

## Acknowledgements
Development of MetaMask.Blazor has been made possible with a grant from [The Graph](https://thegraph.com/blog/wave-one-funding).
