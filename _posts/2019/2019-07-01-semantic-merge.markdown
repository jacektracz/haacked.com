Initial commit

```csharp
using System.Net;

public interface ISocket
{
    string GetHostName(IPAddress address);
    void Listen();
    void Connect(IPAddress address);
    int Send(byte[] buffer);
    int Receive(byte[] buffer);
}
```

Developer 2 creates branch `separate-client-server` and renames `ISocket` to `ICllientSocket`. Developer also moves methods `Listen` and `Receive` into a new interface, `IServerSocket`.

```csharp
using System.Net;

public interface IClientSocket
{
    string GetHostName(IPAddress address);
    void Connect(IPAddress address);
    int Send(byte[] buffer);
}

public interface IServerSocket
{
    void Listen();
    int Receive(byte[] buffer);
}
```

Meanwhile, back on the `master` branch. The original developer moves `GetHostName` into a new interface, `IDns`

```csharp
using System.Net;

public interface ISocket
{
    void Listen();
    void Connect(IPAddress address);
    int Send(byte[] buffer);
    int Receive(byte[] buffer);
}

public interface IDns
{
    string GetHostName(IPAddress address);
}
```

Now Developer 1 tries to merge the `separate-client-server` branch into master and runs into conflicts. Boo hoo.

```csharp
using System.Net;

public interface IClientSocket
{
<<<<<<< HEAD
    void Listen();
=======
    string GetHostName(IPAddress address);
>>>>>>> separate-client-server
    void Connect(IPAddress address);
    int Send(byte[] buffer);
}

<<<<<<< HEAD
public interface IDns
{
    string GetHostName(IPAddress address);
=======
public interface IServerSocket
{
    void Listen();
    int Receive(byte[] buffer);
>>>>>>> separate-client-server
}
```
