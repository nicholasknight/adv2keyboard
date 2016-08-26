I received my Advantage 2 today. There's no full manual yet, even though keyboards are apparently arriving (hint, hint, Kinesis). The quick start guide leaves out the "power user mode", and there are some other quirks.

Update: A manual has been posted at http://www.kinesis-ergo.com/advantage2-resources/

It includes a dictionary for the key maps, but I know it leaves at least one possible key undocumented: it does not list `f14`, but I have successfully mapped my scrollock to `f14` regardless.

It also mentions a firmware version (1.0.18) that doesn't seem to be available yet, with a new feature (status report playback speed).

# The on-board drive.
To get at the on-board drive, you need to enter power user mode, and then "mount" the drive.

Power user mode: `Program+Shift+Esc` (lights will flash a couple times)

Mount drive: `Program+Shift+F1`

This presents a 2MB FAT12 (!) filesystem, so pretty much any OS that supports USB drives will be read/write capable on it.

At least on a Mac, if you try to safely eject the drive, it will, curiously, remount. As far as I can tell, to do it "safely", you have to eject and then quickly hit Program+Shift+F1. If you just hit the key combo, MacOS whines about unsafe removal. This all makes me a bit nervous about possible filesystem corruption down the line.

# Layouts

Keyboard layouts are stored in the folder called "active". You'll find "dvorak.txt" and "qwerty.txt". You can create additional layouts by naming them `X_dvorak.txt` or `X_qwerty.txt` where "X" is any number or letter. You then switch between the layouts with `Program+X`. So, if you create a `2_dvorak.txt`, you can switch to it with `Program+2`. To switch to the "base" layout (that is, dvorak.txt or qwerty.txt), you just hit `Program+F3` (qwerty) or `Program+F4` (dvorak), just like you were switching to that mode to begin with.

NOTE: You have to hit the original, *physical* key corresponding to the letter or number. So if you name a file `g_dvorak.txt`, You have to hit the original QWERTY "g" key -- Dvorak "i", even if you're already in dvorak mode. Probably less confusing to just stick to numbers.

The "language" of the layout files is simple yet arcane. It's `[physicalkey]>[logicalkey]`. The manual provides a list of tokens in the appendix (chapter 13, page 32 of the current version). There appear to be some "hidden" tokens (notably `f14`, which I've been using since I got the keyboard, is not listed). Additional tokens are also apparently coming in future firmware updates.

Below is a sample of what I have in my dvorak layout thus far, mostly created through the on-board remapping mechanism, though `[scroll]>[f14]` was a manual edit (that worked!).

```
[caps]>[rctrl]
[scroll]>[f14]
[intl-\]>[lalt]
[kp=]>[kp=mac]
[hyphen]>[\]
[lalt]>[rwin]
[lctrl]>[lalt]
[kp-lctrl]>[kp-lwin]
[rctrl]>[rwin]
[kp-rctrl]>[kp-rwin]
[\]>[hyphen]
[rwin]>[rctrl]
[kp-rwin]>[kp-rctrl]
```

## Raw HID Codes

Turns out, [you can specify decimal HID keycodes in the layout files](https://twitter.com/kinesisergo/status/768891441594503168)!

I'm not sure of the exact rules, but I've been able to do, for example:

```
[A]>[047]
```

And "A" then types `[`. An initial attempt to just use `[47]` failed, I suspect it either must be at least 3 digits or zero-prefixed.

A list of specified USB HID codes is available in [a PDF on usb.org](http://www.usb.org/developers/hidpage/Hut1_12v2.pdf). Chapter 10, starting on page 53.

# Other files

`state.txt` appears to contain various settings, HOWEVER, I have not yet been able to get manual changes to this file to take effect, even by unplugging the keyboard and plugging it back in, so it appears that it may be effectively read-only.

The curiously-named `do_not_edit.txt` is empty and has an unknown function.

`version.txt` displays the model name and firmware version. I'm guessing this is effectively read-only like state.txt.

# Quirk with remapping Mac modifier keys.

I do some unusual things with my modifier keys. First of all, I've always (long before I used an Advantage) remapped capslock to ctrl. I'm also not a fan of the default Mac modifier key layout on Advantage keyboards. So, I remap them (the `"\|"/"insert"` key (bottom left ring finger key) becomes an `alt/option`, then going left-to-right on the thumb modifiers, I do `alt/option`, `cmd`, `ctrl`, `cmd`).

However, trying to remap them can give surprising results. Specifically, you may find that when you thought you mapped a key to `ctrl`, you actually mapped it to `cmd`, or vice-versa (I haven't documented exactly what happens, mostly I was happy to finally get it right).

I believe this just has to do with the default layout that's active in remapping mode. It's actually the windows or PC modifier key layout, and you have to transpose. Someday I may have the patience to actually stop and think about what's happening. I recall having the same difficulty when I got my Advantage Pro.

---

Adv2Notes © 2016 by Nicholas Knight (https://github.com/nicholasknight/adv2keyboard)

This work is licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.

You should have received a copy of the license along with this work.  If not, see <http://creativecommons.org/licenses/by-sa/4.0/>.
