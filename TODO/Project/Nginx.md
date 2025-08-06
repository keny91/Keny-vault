

NormalLy web servers create a thread for every arriving requests.


Nginx is structured as a Master Process and multiple workers, along with some cache memory.

Workers have a queue for a socket for new incomming connections. I

Event loop, a non blocking (no mutex on thread)