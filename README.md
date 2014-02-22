# irssi-pushover

[Irssi](http://www.irssi.org/) script for sending [Pushover](https://pushover.net/) notifications.

There are a few of these out there, but I really liked the features of [irssi-pushover](https://github.com/henrikbrixandersen/irssi-pushover) so I forked it and adapted it for use with Pushover instead.

## Features

* Notifications on hilights
* Notifications on private messages
* Notifications on private actions (``/me``)
* Setting for always sending notifications, never sending notifications or only sending notifications when Irssi is marked as being away (default)
* Manual notifications using the ``/pushover`` command
* Regular expressions for including/excluding channels/nicks
* Customizable priority levels for Pushover notifications
* Customizable IRC URLs for Pushover notifications (useful for quickly pointing your local iOS IRC client to the right server and channel)
* Customizable event strings for Pushover notifications

## Installation

This script depends on the
[WebService::Pushover](http://search.cpan.org/dist/WebService-Pushover/)
perl module. To install this dependency, run the following command in
your terminal (Hint: You don't need root access to install perl
modules, check out
[local::lib](http://search.cpan.org/dist/local-lib/)):

    cpan WebService::Pushover

Download
[pushover.pl](https://raw.github.com/2bithacker/irssi-pushover/master/pushover.pl)
and place it in ``~/.irssi/scripts/``.

## Usage

To activate the script, run the following commands in Irssi;

    /script load pushover
    /set pushover_userkey 0123456789abcdef0123456789abcdef01234567
    /save

The script will now send out Pushover notifications whenever Irssi is
marked as being away. Pushover notifications can also be sent manually
using the ``/pushover`` command:

    /help pushover
    /pushover Hello, world
    /pushover -url https://github.com/2bithacker/irssi-pushover -priority 2 Check out this cool irssi-pushover script!

## Configuration

### Settings

To change the priority level of the Pushover notifications for private
messages, hilights and the default priority for the ``/pushover``
command, use the following settings:

    /set pushover_priority_msgs 1
    /set pushover_priority_hilight 0
    /set pushover_priority_cmd -1
    /save

By default, Pushover notifications for private messages and hilights are
only sent when Irssi is marked as being away. This can be changed
using the following setting:

    /set pushover_mode ON
    /set pushover_mode OFF
    /set pushover_mode AUTO

``ON`` will always send Pushover notifications, ``OFF`` will turn off all
Pushover notifications except for the ``/pushover`` command and ``AUTO``
will only send Pushover notifications when Irssi is marked as being away.

To limit which channels/nicks will send Pushover notifications, change
the following regular expression settings:

    /set pushover_regex_include ^#
    /set pushover_regex_exclude ^#noise$

To assist in debugging, turn on the ``pushover_debug`` setting:

    /set pushover_debug on

### Theming

To change the Pushover event strings for private messages, hilights and
the ``/pushover`` command, use the following settings:

    /format pushover_event_msgs PM from $0
    /format pushover_event_hilight Mentioned in $0
    /format pushover_event_cmd Remember
    /save

For the first two, ``$0`` will be replaced with the respective channel
and ``$1`` will be replaced with the nick.

The format of the URLs passed to Pushover for private messages and
hilights can be controlled with the following settings:

    /format pushover_url_msgs $0://$1:$3/
    /format pushover_url_hilight $0://$1:$3/$4
    /save

For both of these, ``$0`` will be replaced with either ``irc`` or
``ircs`` depending on whether the respective server uses SSL or
not. ``$1`` will be replaced with the server address, ``$2`` with the
name of the chat network, ``$3`` with the server port number and
``$4`` with the respective nick or channel.

The default URL formats are rather conservative in order to support
the largest number of iOS IRC clients. For
[draft-butcher-irc-url-04](http://tools.ietf.org/html/draft-butcher-irc-url-04)
compliant IRC URLs, one could use the following formats:

    /format pushover_url_msgs $0://$1:$3/$4,isuser,isserver
    /format pushover_url_hilight $0://$2:$3/$4,ischannel,isnetwork
    /save

## Acknowledgements

irssi-pushover is based on [irssi-prowl](https://github.com/henrikbrixandersen/irssi-prowl) by [Henrik Brix Andersen](https://github.com/henrikbrixandersen).

## License

This software is licensed under the 2-clause BSD license. See the
script header for the full license text.
