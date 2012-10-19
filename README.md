# NAME

AnyEvent::HTTP::LWP::UserAgent::Determined - a virtual browser that retries errors with AnyEvent

# SYNOPSIS

    use strict;
    use AnyEvent::HTTP::LWP::UserAgent::Determined;
    my $browser = LWP::UserAgent::Determined->new;
    my $response = $browser->get($url, headers... );
    $browser->get_async($url, headers... )->cb(sub {
      my $response = shift->recv;
    });

# DESCRIPTION

[LWP::UserAgent::Determined](http://search.cpan.org/perldoc?LWP::UserAgent::Determined) works just like [LWP::UserAgent](http://search.cpan.org/perldoc?LWP::UserAgent) (and is based on it, by
being a subclass of it), except that when you use it to get a web page
but run into a possibly-temporary error (like a DNS lookup timeout),
it'll wait a few seconds and retry a few times.

It also adds some methods for controlling exactly what errors are
considered retry-worthy and how many times to wait and for how many
seconds, but normally you needn't bother about these, as the default
settings are relatively sane.

This class not only works like [LWP::UserAgent::Determined](http://search.cpan.org/perldoc?LWP::UserAgent::Determined) but also [AnyEvent::HTTP::LWP::UserAgent](http://search.cpan.org/perldoc?AnyEvent::HTTP::LWP::UserAgent)
 (and is based on them, by being a subclass of them),

# METHODS

This module inherits all of [LWP::UserAgent::Determined](http://search.cpan.org/perldoc?LWP::UserAgent::Determined)'s methods and 
[AnyEvent::HTTP::LWP::UserAgent](http://search.cpan.org/perldoc?AnyEvent::HTTP::LWP::UserAgent)'s methods.

# IMPLEMENTATION

This class works by overriding [AnyEvent::HTTP::LWP::UserAgent](http://search.cpan.org/perldoc?AnyEvent::HTTP::LWP::UserAgent)'s `simple_request` method
with its own around-method that just loops.  See the source of this
module; it's straightforward with caution of asynchronous nature.



# SEE ALSO

[LWP](http://search.cpan.org/perldoc?LWP), [LWP::UserAgent](http://search.cpan.org/perldoc?LWP::UserAgent), [LWP::UserAgent::Determined](http://search.cpan.org/perldoc?LWP::UserAgent::Determined), [AnyEvent::HTTP](http://search.cpan.org/perldoc?AnyEvent::HTTP), [AnyEvent::HTTP::LWP::UserAgent](http://search.cpan.org/perldoc?AnyEvent::HTTP::LWP::UserAgent)



# COPYRIGHT AND DISCLAIMER

Original copyright for LWP::UserAgent::Determined:

Copyright 2004, Sean M. Burke, all rights
reserved.  This program is free software; you can redistribute it
and/or modify it under the same terms as Perl itself.

This program is distributed in the hope that it will be useful,
but without any warranty; without even the implied warranty of
merchantability or fitness for a particular purpose.



# AUTHOR

Yasutaka ATARASHI `yakex@cpan.org`

Original authors of LWP::UserAgent::Determined are as follows:

Originally created by Sean M. Burke, `sburke@cpan.org`

Currently maintained by Jesse Vincent `jesse@fsck.com`
