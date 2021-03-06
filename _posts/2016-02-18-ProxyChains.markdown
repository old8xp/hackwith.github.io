---
layout: post
title:  "ProxyChains"
date:   2016-02-18 01:40:00
categories: Proxy
shortnote: "ProxyChains is a UNIX program, that hooks network-related libc functions in dynamically linked programs via a preloaded DLL and redirects the connections through SOCKS4a/5 or HTTP proxies."
---

##Current version: 4.2.0

##Build Status

ProxyChains is a UNIX program, that hooks network-related `libc` functions in dynamically linked programs via a preloaded DLL and redirects the connections through SOCKS4a/5 or HTTP proxies.

###Warning
This program works only on dynamically linked programs. Also both proxychains and the program to call must use the same dynamic linker (i.e. same `libc`)

##Known limitations of the current version
When a process forks, does a DNS lookup in the child, and then uses the IP in the parent, the corresponding ip mapping will not be found. This is because the fork can’t write back into the parents mapping table. IRSSI shows this behaviour, so you have to pass the resolved IP address to it. (You can use the `proxyresolv` script (requires `dig`) to do so)

This means that you can’t currently use tor onion urls for irssi. To solve this issue, an external data store (`file`, `pipe`, …​) has to manage the `dns <→ ip mapping`. Of course there has to be proper locking. `shm_open`, `mkstemp`, are possible candidates for a file based approach, the other option is to spawn some kind of server process that manages the map lookups. since `connect()` etc are hooked, this must not be a TCP server.

#Installation

##Using release version

<b>Proxychains-4.2.0</b> are available with `pkgsrc` to everyone using it on Linux, NetBSD, FreeBSD, OpenBSD, DragonFlyBSD or Mac OS X. You just need to install `pkgsrc-wip` repository and run make install in a `wip/proxychains` directory.

You can find out more about `pkgsrc` on pkgsrc and about `pkgsrc-wip` on Pkgsrc-wip homepage.

##Installing on Mac OS X with homebrew

You can install current proxychains on Mac OS X with an homebrew. You have to download unofficial homebrew formula from to your `BREW_HOME` by default `/usr/local/Library/Formula/` and run

{% highlight bash %}
$ brew install proxychains
{% endhighlight %}

##Running Current Source code version
{% highlight bash %}
# needs a working C compiler, preferably gcc
./configure
make
sudo make install
{% endhighlight %}

##When to use it

- When the only way to get "outside" from your LAN is through proxy server.

- To get out from behind restrictive firewall which filters outgoing ports.

- To use two (or more) proxies in chain:
{% highlight bash %}
   like: your_host <--> proxy1 <--> proxy2 <--> target_host
{% endhighlight %}
- To "proxify" some program with no proxy support built-in (like telnet)

- Access intranet from outside via proxy.

- To use DNS behind proxy.


##To know more about ProxyChains click <a href="https://github.com/haad/proxychains" title="ProxyChains" target="_blank">here</a>

##Useful links:
<footer>
<a href="https://github.com/pietromenna/jekyll-architect-theme/archive/master.zip" target="_blank" class="button">
<small>Download</small>
.zip file
</a>
</footer>