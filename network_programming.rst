===================
Network Programming
===================

-----------
Advanced IO
-----------

``recv`` and ``send`` are similar to ``read`` and ``write`` functions, but one
additional parameter is required to specify arguments regarding to networking
operation ::
    
    ssize_t recv(int sockfd, void *buf, size_t len, int flags);
    ssize_t send(int sockfd, const void *buf, size_t len, int flags);

``MSG_NOSIGNAL`` flag requests that the implementation does not send a
``SIGPIPE`` signal on errors on stream oriented sockets when the other end
breaks the connection. The ``EPIPE`` error is still returned as normal. A socket
option ``SO_NOSIGPIPE`` have the same effect.


------
Signal
------

The basic rule that applies to signal is when a process is blocked in a slow
system call and the process catches a signal and the signal handler returns, the
system can return an ``EINTR`` error. Some kernel automatically restart `some`
interrupted system calls. 


