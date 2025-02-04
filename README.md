# ESP32Ping
Let the ESP32Ping ping a remote machine.

This fork adds an ping with ms options in a compatible way. The original method is the same,
but an PingMs() is added.
tw: I did a fork of the original ESP32Ping lib at version 1.7. I renamed this to ESP32PingMs which is fully compatible (drop in replacement).
The new functionality is available with the PingMs() call, see below.

#Note that this is a port from https://github.com/dancol90/ESP8266Ping
With this library an ESP32Ping can ping a remote machine and know if it's reachable.
It provide some basic measurements on ping messages (avg response time).

## Usage

First, include the library in your sketch along with WiFi library:

```Arduino
#include <WiFi.h>
#include <ESP32Ping.h>
```

Next, simply call the `Ping.ping()` function

```Arduino
IPAddress ip (192, 168, 0, 1); // The remote ip to ping
bool ret = Ping.ping(ip);
```

`ret` will be true if the remote responded to pings, false if not reachable.
The library supports hostname too, just pass a string instead of the ip address:

```Arduino
bool ret = Ping.ping("www.google.com");
```

Additionally, the function accept a second integer parameter `count` that specify how many pings has to be sent:

```Arduino
bool ret = Ping.ping(ip_or_host, 10);
```

After `Ping.ping()` has been called, the average response time (in milliseconds) can be retrieved with

```Arduino
float avg_time_ms = Ping.averageTime();
```

These is the "old" compatibility layer with defaults (timeout 1 second, interval 1 second, count 3, size 32)

## Update for ESP32PingMs:

The new method for doing pings with millisecond timing is:

```Arduino
bool PingClass::pingMs(IPAddress dest, byte count, int timeout_ms, int size, int interval_ms);
```

So for doing a single ping with 50 ms timeout you can do:

```Arduino
bool ret = Ping.pingMs(ip_or_host, 1, 50);
```
