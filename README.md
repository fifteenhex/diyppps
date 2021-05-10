# diyppps
Making a DIY usb hub with per-port-power-switching using an existing hub.

So you want to use [uhubctl](https://github.com/mvp/uhubctl) to do power
control for USB devices but like everyone else you found that hubs with PPPS
wired up are rare.

If you can find a USB hub with buttons like the [RSH-516-4](https://www.amazon.co.jp/gp/product/B07R227J1S/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1)
then the chances are that the buttons drive transistors/mosfets to control
VBUS. If the hub chip inside exposes all of the PPPS control signals like
the RTS5411 in the RSH-516-4 does then you can remove the buttons and
wire the PPPS control signals to the VBUS transistor/mosfets instead and
have a PPPS capable USB hub.

For the RSH-516-4 this wasn't so easy. There are pads in the footprint
for the signals but the PCB is apparently made of toilet paper.
One hub died during this experiment because all of the pads including
the usb signal pads came off the board when trying to attach wires to
the PPPS signals.

It is much easier to grind off the corner of the chip where the PPPS
signals are and solder directly to the lead frame instead. See the photos
to see what I did but the basic idea is to slowly use a file
on the corner of the RTS5411 to expose the 4 PPPS signals. Go slow
to avoid going right through the lead frame. Once some metal is exposed
you can tin the metal and have some pads to solder on to. The soldering
process is difficult but not impossible. Once you have good connections
use some 5 minute epoxy to make everything solid and then you can
attach your PPPS signals to the pads from the buttons.

Maybe a small flex pcb could make this process easier.

## Hubs that are good

- RSH-516-4 - Realtek RTS5411 - can be done, need good soldering skills
- "Atolla USB 3.0 HUB " - Renesas UPD720210 - Much easier, PPPS pins are
   brought out onto resistors so you can very easily tack wires on.
   PPPS signals are 3.3v and push-pull and can't directly drive the p-channel
   mosfets used to control the VBUS lines. You need a 3.3V -> 5v logic
   doodad or make some transistors to drive the mosfet gates.
   See [here](/atolla/).

## Hubs that are no good

- Sabrent 4 port (HB-UM43): GL3510 hub doesn't have per port port control pins
  switches directly connect and disconnect VBUS from the ports.
