---
title: Java InputStream
date: 2023-10-27 15:08:36
toc: true  
categories:  
- java  

---

# Java InputStream

`InputStream` is an important class in the Java programming language used for reading data. It is an abstract class representing the superclass of all classes that read bytes from a stream. `InputStream` is located in the `java.io` package and provides fundamental methods to read byte streams.

### Key Features

1. **Abstract Class**: `InputStream` is an abstract class and cannot be instantiated directly. It needs to be implemented by its subclasses.
2. **Byte Stream**: It is used to read bytes (8-bit data), making it suitable for reading all types of data (text, images, audio, etc.).
3. **Blocking Methods**: Its read operations may block until input data is available, end of the file is detected, or an exception is thrown.

### Main Methods

#### 1. `int read()`

- **Usage**: Reads the next byte of data from the input stream.
- **Returns**: The byte read (0 to 255) or `-1` if the end of the stream is reached.

  ```java
  InputStream is = new FileInputStream("example.txt");
  int singleByte = is.read();
  is.close();
  ```

#### 2. `int read(byte[] b)`

- **Usage**: Reads some bytes from the input stream and stores them into the array `b`.
- **Parameters**: `b` - the buffer into which the data is read.
- **Returns**: The number of bytes read, or `-1` if the end of the stream is reached.

  ```java
  InputStream is = new FileInputStream("example.txt");
  byte[] byteArray = new byte[100];
  int numOfBytesRead = is.read(byteArray);
  is.close();
  ```

#### 3. `int read(byte[] b, int off, int len)`

- **Usage**: Reads up to `len` bytes of data from the input stream into an array of bytes.
- **Parameters**:
  - `b` - the buffer into which the data is read.
  - `off` - the start offset in the destination array `b`.
  - `len` - the maximum number of bytes read.
- **Returns**: The number of bytes read, or `-1` if the end of the stream is reached.

  ```java
  InputStream is = new FileInputStream("example.txt");
  byte[] byteArray = new byte[100];
  int numOfBytesRead = is.read(byteArray, 0, byteArray.length);
  is.close();
  ```

#### 4. `long skip(long n)`

- **Usage**: Skips over and discards `n` bytes of data from the input stream.
- **Parameters**: `n` - the number of bytes to be skipped.
- **Returns**: The actual number of bytes skipped.

  ```java
  InputStream is = new FileInputStream("example.txt");
  long bytesSkipped = is.skip(50);
  is.close();
  ```

#### 5. `int available()`

- **Usage**: Returns an estimate of the number of bytes that can be read (or skipped over) from this input stream without blocking.
- **Returns**: An estimate of the number of bytes that can be read without blocking.

  ```java
  InputStream is = new FileInputStream("example.txt");
  int availableBytes = is.available();
  is.close();
  ```

#### 6. `void close()`

- **Usage**: Closes this input stream and releases any system resources associated with the stream.

  ```java
  InputStream is = new FileInputStream("example.txt");
  is.close();
  ```

#### 7. `void mark(int readlimit)`

- **Usage**: Marks the current position in this input stream.
- **Parameters**: `readlimit` - the maximum limit of bytes that can be read before the mark position becomes invalid.

  ```java
  InputStream is = new FileInputStream("example.txt");
  if (is.markSupported()) {
      is.mark(100); // Mark the current position
      // ... perform some read operations
      is.reset();   // Reset to the marked position
  }
  is.close();
  ```

#### 8. `void reset()`

- **Usage**: Repositions this stream to the position at the time the `mark` method was last called.
- **Note**: This method is valid only if the input stream supports the `mark/reset` functionality. Otherwise, it may throw an `IOException`.

#### 9. `boolean markSupported()`

- **Usage**: Tests if this input stream supports the `mark` and `reset` methods.
- **Returns**: `true` if this stream instance supports the `mark` and `reset` methods; `false` otherwise.

### Example

Here is a simple example that demonstrates how to use `FileInputStream` (a subclass of `InputStream`) to read the contents of a file.

```java
import java.io.FileInputStream;
import java.io.InputStream;

public class InputStreamExample {
    public static void main(String[] args) {
        try {
            InputStream is = new FileInputStream("example.txt");
            int byteData;

            while ((byteData = is.read()) != -1) {
                // Print each byte as a character
                System.out.print((char) byteData);
            }

            is.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

In this example, `FileInputStream` is used to read data from a file named `example.txt`. The `read()` method reads one byte at a time from the file until the end of the file is reached (indicated by `-1`).

### Best Practices

- Ensure to call the `close()` method after using `InputStream` to release resources.
- Handle exceptions properly using try-catch blocks.
- For efficiency, consider using `BufferedInputStream` in combination with `InputStream`.

By understanding and utilizing these methods and best practices, you can effectively manage and read byte streams in Java applications.