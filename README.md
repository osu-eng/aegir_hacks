Aegir Hacks
===========

This contains some hacks we use in the aegir project. Don't be like us. Don't hack Aegir.

~/.drush/provision/http/apache/vhost.tpl.php
--------------------------------------------

The pack module for 6.x-1.x (1.9) doesn't appear to work correctly with SSL. 
Mmy observed problem with pack is that the SSL bits don't seem to be being set correctly. 
This results in the 443 vhost block getting skipped (do to conditionals in the ssl 
vhost.tpl.php template). My guess is this has something to do with the way Aegir maps 
SSL certificates to IPs and the fact that all the slaves in a pack have a different ip.

There's an issue in their queue about this being a problem for 2.x.
http://drupal.org/node/1784108

We only have one SSL cert for our whole aegir cluster so a really, really blissful 
solution would be if we could just disable SSL and override aegir's standard vhost.tpl.php 
template. Unfortunately, we believe it's only possible to inject into an existing vhost.tpl.php.

In 2.x there has apparently been a commit to allow you to override the vhost template.
http://drupal.org/node/709862

However, we're not planning on running 2.x while it's in alpha (currently alpha1).

So the plan is to replace the vhost.tpl.php file in provision with the one here.
When 2.x is stable, we'll switch to a non-hacky way of overriding the template
or use native ssl/pack support as necessary.
