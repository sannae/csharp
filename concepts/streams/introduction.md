# Introduction

C# includes following standard IO (Input/Output) classes to read/write from different sources like files, memory, network, isolated storage, etc.

`System.IO.Stream` is an abstract class that provides standard methods to transfer bytes (read, write, etc.) to the source. Classes that need to read/write bytes from a particular source must implement the `Stream` class: some of the more commonly used streams that inherit from `Stream` are `FileStream` and `MemoryStream`.

Any stream must be disposed once used. It is recommended to use the `using` keyword:

```csharp
using (MemoryStream memory = new MemoryStream())
{
   // do stuff here...
}
```

## Stream Reader and Writer

Streams involve two fundamental operations:

* You can read from streams, by converting bytes into a specific data structure, using an appropriate encoding. This is done with the `StreamReader` object.

* You can write to streams, by converting a specific data structure into bytes via an appropriate encoding. This is done with the `StreamWriter` object.

```csharp
using (MemoryStream memoryStream = new MemoryStream())
{
    // Open writing buffer
    StreamWriter streamWriter = new StreamWriter(memoryStream);
    // Write data to buffer
    streamWriter.Write(123);
    // Clear the buffer, write buffered data to stream
    streamWriter.Flush();
    
    // We need to set the position to 0 in order to read from the beginning
    memoryStream.Position = 0;

    // Open reading buffer
    StreamReader streamReader = new StreamReader(ms);
    // Read buffer and save into variable
    var readString = streamReader.ReadToEnd();
}
// dispose stream
```