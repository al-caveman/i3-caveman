i like [i3](https://github.com/i3/i3), but its maintainers are drama queens
that baselessly rejected a patch of mine, and even banned me, all due to
some irc drama.  if you want to read _more_ about this drama, checkout the
[appendix](#appendix) section.

anyway, i'll keep my patches here.  for me to use, and others who like it.
all while maintaining the taste of liberty, the taste of gplv3!

# patches (so far just one)

## 1. i3 _surface_ `focus`ing mode

*synopsis—* this patch, in the file `i3-surface-focus-mode.patch`, is a
simple solution to solve `i3`'s vertical and horizontal focusing swamps
problem.  tested and works great with `x11-wm/i3-4.18.2`, and it keeps
working perfectly with later releases of `i3`.  currently i am using
`x11-wm/i3-4.19.1` with no problem at all.  i have setup my `gentoo` to
apply this patch automatically every time `i3` gets updated, and i forgot
about it thanks to it working perfectly every time.

### usage

```
bindsym KEYS focus DIRECTION surface
```

where:
- `KEYS` is any upstream key binding as per `i3`'s `bindsym` syntax.
- `DIRECTION` is any upstream direction.


### `i3` has swamps?

without this patch, `i3` has a major usability problem, by which moving
around with the focus command will _also_ shuffle your tabs or stacks.  for
example, stacks are vertical, and when you want to move the focus upwards
and fall in a stack, you will get stuck there (i call it a _vertical
swamp_), and keep moving up/down in the vertical direction really slowly as
you shuffle the stacks.

`i3`'s official solution to this annoying _vertical swamp_ problem is to
put `i3` is to do `mod+a` for selection all elements in the stack swamp, so
that you jump there.  but this approach is not `o(1)` as it requires the
user to be aware of swamps ahead of him as he navigates across tabs.
realistically, we often discover that we are stuck in a vertical swamp only
after we've fell into it and wasted a few `mod+direction` key hits already,
only then we put `i3` in manual 4l gear (i.e. `mod+a`) then do another
`mod+direction` to finally get out the swamp!

a similar problem happens with tabs, except that tabs are _horizontal
swamps_.  this is an identical problem to the horizontal swamps above,
except for having a vertical polarity.

therefore, a neat solution is to introduce the `surface` focusing mode
(which this patch does).  this way, we can navigate around with `focus
direction surface` as we want, without causing any stacks or tabs to
re-shuffle.  this way, you won't _need_ to keep scouting ahead of your
steps to watch out for vertical/horizontal swamps, nor need to put `i3` in
manual 4l gear (`mod+a`)!

finally, in order to shuffle the stacks or tabs, you can simply use the
`sibling` focusing mode (which is already in upstream).

a neat side effect of this is that stacks and tabs can now be treated just
like tabs, except that stacks are tabs that are visually looking different
than tabs.

### example config

here is how my i3 uses the `focus` mode.  of course you can use other
bindings, this is just how i like to use it:

```
bindsym $mod+h focus left surface
bindsym $mod+j focus down surface
bindsym $mod+k focus up surface
bindsym $mod+l focus right surface
bindsym $mod+Mod1+h focus left
bindsym $mod+Mod1+j focus down
bindsym $mod+Mod1+k focus up
bindsym $mod+Mod1+l focus right
bindsym $mod+p focus prev sibling
bindsym $mod+n focus next sibling
```
As you see above, I personally like it this way:

- `mod+DIRECTION` to be in `focus` mode, so that i move around _freely_
  without any fear of any swamps as i gloriously hover over them like
  magic!
- `mod+p` and `mod+n` to shuffle previous/next in `sibling` mode (already
  in upstream i3).
- `mod+Mod1+DIRECTION` to move around in manual L4 gear, for surgical
  situations, which also shuffles stacks/tabs (which is the default option
  in upstream `i3` yuck!).


# appendix


*i3 drama synopsis—* a blind person that lurks in dark the corners of the
`freenode` irc network, whom goes by the nick `squigz`, confused me against
another person that apparently wasn't pleasant to `squigz`.  so, this
`squigz` started banning me in channels where he is an op, spread railing
accusations about me with other ops of other channels.  `squigz` even kept
pushing ops of `#weechat-offtopic` to ban me (they refused since i didn't
do anything wrong, of course `squigz` quit the channel, at least
momentarily, since he is apparently a drama queen).  but the drama queens
of `i3` (aka i3's maintainers) fell for it and went full twilight-mode.
more info is below.

- historical description about the stack/tab swamp problem:
  https://github.com/i3/i3/issues/3738
- historical reference about the original PR in `i3` (and the drama queen
  `i3` maintainers): https://github.com/i3/i3/pull/3859
- an `i3` maintainer actually [liked this `focus` idea a
  lot](https://github.com/i3/i3/issues/3738#issuecomment-550185288) (in his
  own words), and also [approved the simplicity of the
  patch](https://github.com/i3/i3/pull/3859#issuecomment-593023090).
  could've easily ended up in upstream `i3` to the benefit of humanity.
  but they rejected it simply because of the psycho `squigz` and the drama
  queen `i3` maintainers who can't act professional for 1 second.  i mean,
  look at [how an i3 maintainer is
  talking](https://www.youtube.com/watch?v=qbtr_a7vBXw&feature=youtu.be&t=382)?
  can't stand straight either.
