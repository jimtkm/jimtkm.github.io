---
layout: post
title: "Ghost on FreeBSD"
excerpt: "Get Ghost working under FreeBSD."
---
Couple of months back, I switched to [FreeBSD][fbsd] and started everything fresh. I just prefer [FreeBSD][fbsd].

I didn't want to run [WordPress][wp], I want something light and simple, like [Jekyll][jrb]. But I also want to be able to blog with my iPad or even my mobile phone. So, I ended up with [Ghost][gh-pg], and I'm liking it.

## Installing

Installing `node` and `npm` are pretty straightforward.

{% highlight text %}
cd /usr/ports/www/node
sudo make install clean
{% endhighlight %}


{% highlight text %}
cd /usr/ports/www/npm
sudo make install clean
{% endhighlight %}

Once done, I tried to install [Ghost][gh-pg] but got a `sqlite3` error due to `g++`. After some googling, the solution is very simple.

We will need to install `sqlite3`.

{% highlight text %}
cd /usr/ports/databases/sqlite3
sudo make install clean
{% endhighlight %}

Now we can start installing [Ghost][gh-pg].

{% highlight text %}
cd /usr/local/www/ghost
setenv CXX c++ ; npm install sqlite3 --sqlite=/usr/local
{% endhighlight %}

Now [Ghost][gh-pg] is installed, just follow [Ghost][gh-pg] document to complete your configuration.

## Running Ghost

I prefer to run [Ghost][gh-pg] as a service using `forever` module.

{% highlight text %}
npm install forever -g
{% endhighlight %}

Copy this script.

<script src="https://gist.github.com/jimtkm/c2134edbf9ccdec4555b.js"></script>

Now, just start [Ghost][gh-pg] like any [FreeBSD][fbsd] services.

**PS**: This my script, I have it inside `/usr/local/etc/rc.d/`. Also, my log file is inside `/var/log/ghost/ghost.log`. This is a sh script, you will need to `+x` to run it, duh. And never run as `root`, create a `ghost` user or something.


[fbsd]: http://freebsd.org/
[wp]: http://wordpress.org/
[jrb]: http://jekyllrb.com/
[gh-pg]: http://ghost.org/
