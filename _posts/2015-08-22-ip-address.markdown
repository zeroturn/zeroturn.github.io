---
layout: post
title:  "IP Address"
date:   2015-08-22
categories: 
---

##### IPv4 - Dotted Decimal Notation
Computer-to-computer communication (i.e., networking) requires two very basic things:

* each computer must communicate using the same "language" (otherwise known as a *protocol*) and
* each computer must have an address

By far the dominant language or protocol is TCP/IP.  TCP/IP is actually comprised of two separate protocols, TCP ("Transmission Control Protocol") and IP ("Internet Protocol"), but they are so intimately intertwined that they are commonly spoken of as TCP/IP.

Just like houses and buildings have numerical addresses (e.g., 123 Downing Street), the IP protocol requires that each computer have a numerical address.  The address is expressed as a [**32 bit number**](/binary-numbers "a discussion of binary numbers").  See also this [wikipedia](https://en.wikipedia.org/wiki/Binary_number) article.  For example, one computer may have the address of say `11000000101010000000000000000001` and another computer may have the address `11000000101010000000000000100000`.  Since these are hard to remember and talk about, one could try to remember the decimal equivalent of these numbers, namely, 3,232,235,521 and 3,232,235,552.  But that's not much better.  Because of this difficulty, the "dotted decimal" notation was devised.  The binary number is broken into 4 chunks (8 bits each) separated by a dot and each 8 bit chunk is expressed as a decimal number.  Thus, 

`11000000101010000000000000000001`

becomes 

`11000000.10101000.00000000.00000001` 

and that number becomes 

`192.168.0.1` 

which is **much** easier to read and talk about!  And, by the way, that dotted decimal number can be reconverted to decimal if you choose:

**192** x 256^3 + **168** x 256^2 + **0** x 256 + **1** = 3,232,235,521

Because each decimal number is based on 8 bits, the largest decimal number that can appear in dotted decimal notation is 255 (2^8 = 256; so the range of addresses is 0 to 255).  It is simply impossible to have an address such as 192.**302**.0.1.  

##### IP Address Classes and Reserved Addresses
Until about 1993, internet addresses were divided into five different [classes](https://en.wikipedia.org/wiki/Classful_network "more information on "classful" addressing) (denominated Class A - E) intended for different uses and sizes of network.  Since that time an addressing scheme *without classes* has been used, appropriately named *Classless* Inter-Domain Routing or CIDR.

###### Private Addresses
Parts of the address space have been reserved for private networks.  Some of these reserved addresses are

* 10.0.0.0 - 10.255.255.255 (16,777,216 addresses available)
* 172.16.0.0 - 172.31.255.255 (1,048,576 addresses available)
* 192.168.0.0 - 192.168.255.255 (65,536 addresses available)
* 127.0.0.0 - 127.255.255.255 (loopback address)
* 169.254.1.0 - 169.254.254.255 (link-local autoconfiguration when DHCP is not available)

These addresses are *non-routable* meaning that internet routers will not route packets with a destination address in any of these ranges.  These addresses are used strictly within private networks.

The *base* address, wherein the host address consists of all zeros, is the *network address*, meaning it is the address of the entire network, not the address of an individual host computer on that network.  Similarly, the *high* address, wherein the host address consists of all ones, is the *broadcast address* meaning that it is the address that is used when a computer needs to send a message to *all* computers on the network.  For example, in the Class C 192.168.0.0 network, 192.168.0.0 is the network address and 192.168.0.255 is the broadcast address.  Individual hosts on that network will have addresses within the range of 1 - 254.

###### Subnetting
As more and more computers "talk" on the same network, the signals from each interfere more and more with the signals of the other computers on the network.  This interference, or collision, of one signal with another can slow network performance to a crawl.

But, the number of signal "collisions" that occur can be reduced by [subnetting](https://en.wikipedia.org/wiki/Subnetwork "a detailed discussion of subnetting") or network segmentation.  Suppose, for example, we had 50 computers that we wanted to be able to communicate with each other, 25 in the accounting department, 15 in the sales department, and 10 in the human resources department.  All 50 could easily be assigned an address within the 192.168.0.0 network, which can support 254 hosts.  However, the "noise" on the network could be reduced considerably if each department was placed on its own network.  So, for example, the accounting department could be placed in the 192.168.0.0 network; the sales department placed in the 192.168.1.0 network; and the human resources department placed in the 192.168.2.0 network, with *bridges* or *switches* used to route traffic from one network to another as needed.

The same subnetting or segmentation could be accomplished with a CIDR scheme.  For example, the accounting department could be placed on the 192.168.0.0/27 network with host addresses ranging from 192.168.0.1 to 192.168.0.30.  The "/27" indicates that the 27 most significant bits of the address define the network and the remaining 5 bits designate the individual hosts within the network.  Five bits can represent 32 unique addresses (2^5 = 32), but the first is reserved as the network address and the last is reserved as the broadcast address.  That leaves 30 addresses available for the 25 hosts in the accounting department.  Thus, in this example, 192.168.0.0 is the network address, 192.168.0.31 is the broadcast address, and every address in between is available for use as a host address.  The net mask is 255.255.255.224.  Similarly, the sales department could be placed on the 192.168.0.32/27 network with host addresses ranging from 192.168.0.33 to 192.168.0.62.  Finally, the human resources department could be placed on the 192.168.0.64/28 network with host addresses ranging from 192.168.0.65 to 192.168.0.78 (using a net mask of 255.255.255.240).

A CIDR subnet can easily be calculated using Wolfram Alpha.  Try it here using address [192.168.0.56/27](http://www.wolframalpha.com/input/?i=192.168.0.56%2F27).  It tells you that 192.168.0.56 is a host address on the 192.168.0.32 network; that 30 host addresses are available in the range of 192.168.0.33 to 192.168.0.62; that the broadcast address is 192.168.0.63; and that the net mask is 255.255.255.224.

##### IPv6 - the new addressing scheme
Compared to IPv4, the new IPv6 ("IP version 6") addresses are hideously ugly.  But, the IPv4 addressing scheme will *only* accomodate 4,294,967,296 unique addresses.  That seemed like a sufficiently large number to last quite a long time when the scheme was developed, but it has proven to be too small an address space.  The problem has been mitigated somewhat by the introduction of CIDR and also by the extensive use of *NAT* (Network Address Translation) in which many computers on a local area network (LAN) can appear to the internet to be located at a single *external* (i.e., internet facing) address.  But a new scheme is needed and the IPv6 addressing scheme has been developed to solve the problem of insufficient unique addresses.

IPv6 uses 128 bit addresses and therefore permits 3.4 x 10^38 unique addresses.  This is roughly equal to half of the estimated number of atoms in the observable universe.  That should last us for a while.

Rather than "dotted decimal" notation, the IPv6 addresses use what I call "colon hex" notation.  The number is expressed in 8 groups of four [hexadecimal numbers](https://en.wikipedia.org/wiki/Hexadecimal "a detailed discussion of hexadecimal numbers"), separated by colons.  The following is an example of a properly formatted IPv6 address:

`2001:0db8:85a3:0000:0000:8a2e:0370:7334`

Several methods can be used to simplify the address.  Leading zeros may be omitted.  Thus the address above could be simplified to

`2001:0db8:85a3:0:0:8a2e:0370:7334`

Also, *two or more* successive groups of zeros can be replaced with empty space between colons:

`2001:0db8:85a3::8a2e:0370:7334`

Because the address is comprised of 8 groups of numbers and there are only 6 groups in the above number, one can conclude that there are two groups of 0's represented by the double colon.  A single group of zeros is never replaced with a double colon.  The double colon may only be used once in an address.  To allow otherwise would introduce irresolvable ambiguity.

The scheme anticipates that IPv6 addresses will generally be assigned automatically using [DHCPv6](https://en.wikipedia.org/wiki/DHCPv6) based upon the devices' [MAC address](https://en.wikipedia.org/wiki/MAC_address "a discussion of 'media access control' addresses").

During the transition phase from IPv4 to IPv6, IPv4 addresses can be mapped to IPv6 addresses on *some* systems by using the IPv4 address as the last 32 bits of the 128 bit IPv6 address *and* representing those 32 bits in dotted decimal notation.  To accomplish this, IPv6 recognizes a special "transition class" address consisting of an 80 bit prefix of zeros, followed by 16 bits set to 1.  The remaining 32 bits are written in dotted decimal notation.  Thus, the IPv4 address `192.168.0.32` mapped to IPv6 would be represented as `::ffff:192.168.0.32`.

More information on the subject can be found [here](https://en.wikipedia.org/wiki/Private_network) and [here](https://en.wikipedia.org/wiki/IPv6).

[Home Page](/home)
