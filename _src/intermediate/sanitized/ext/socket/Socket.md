# Socket

Class `Socket` provides access to the underlying operating system socket
implementations.  It can be used to provide more operating system specific
functionality than the protocol-specific socket classes.

The constants defined under Socket::Constants are also defined under Socket. 
For example, Socket::AF_INET is usable as well as Socket::Constants::AF_INET. 
See Socket::Constants for the list of constants.

### What's a socket?

Sockets are endpoints of a bidirectional communication channel. Sockets can
communicate within a process, between processes on the same machine or between
different machines.  There are many types of socket: TCPSocket, UDPSocket or
UNIXSocket for example.

Sockets have their own vocabulary:

**domain:** The family of protocols:
*   Socket::PF_INET
*   Socket::PF_INET6
*   Socket::PF_UNIX
*   etc.


**type:** The type of communications between the two endpoints, typically
*   Socket::SOCK_STREAM
*   Socket::SOCK_DGRAM.


**protocol:** Typically *zero*. This may be used to identify a variant of a
protocol.

**hostname:** The identifier of a network interface:
*   a string (hostname, IPv4 or IPv6 address or `broadcast` which specifies a
    broadcast address)

*   a zero-length string which specifies INADDR_ANY
*   an integer (interpreted as binary address in host byte order).


### Quick start

Many of the classes, such as TCPSocket, UDPSocket or UNIXSocket, ease the use
of sockets comparatively to the equivalent C programming interface.

Let's create an internet socket using the IPv4 protocol in a C-like manner:

    require 'socket'

    s = Socket.new Socket::AF_INET, Socket::SOCK_STREAM
    s.connect Socket.pack_sockaddr_in(80, 'example.com')

You could also use the TCPSocket class:

    s = TCPSocket.new 'example.com', 80

A simple server might look like this:

    require 'socket'

    server = TCPServer.new 2000 # Server bound to port 2000

    loop do
      client = server.accept    # Wait for a client to connect
      client.puts "Hello !"
      client.puts "Time is #{Time.now}"
      client.close
    end

A simple client may look like this:

    require 'socket'

    s = TCPSocket.new 'localhost', 2000

    while line = s.gets # Read lines from socket
      puts line         # and print them
    end

    s.close             # close socket when done

### Exception Handling

Ruby's Socket implementation raises exceptions based on the error generated by
the system dependent implementation.  This is why the methods are documented
in a way that isolate Unix-based system exceptions from Windows based
exceptions. If more information on a particular exception is needed, please
refer to the Unix manual pages or the Windows WinSock reference.

### Convenience methods

Although the general way to create socket is Socket.new, there are several
methods of socket creation for most cases.

* TCP client socket: Socket.tcp, TCPSocket.open
* TCP server socket: Socket.tcp_server_loop, TCPServer.open
* UNIX client socket: Socket.unix, UNIXSocket.open
* UNIX server socket: Socket.unix_server_loop, UNIXServer.open


### Documentation by

*   Zach Dennis
*   Sam Roberts
*   *Programming Ruby* from The Pragmatic Bookshelf.


Much material in this documentation is taken with permission from *Programming
Ruby* from The Pragmatic Bookshelf.

[Socket Reference](https://ruby-doc.org/stdlib-2.7.0/libdoc/socket/rdoc/Socket.html)