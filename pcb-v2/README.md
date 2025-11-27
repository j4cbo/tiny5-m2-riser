# Ordering Boards

The riser can be assembled by any PCB manufacturing contractor. I used [JLCPCB](https://jlcpcb.com/) and have optimized the parts list for their process. To order your own batch:

- Log in to your account (or create a new one, if you don't already have one).
- Upload `riser-v2.zip` with the "Add gerber file" box on the home page.
- Some properties of the PCB (4 layers, outside dimensions) will be auto-detected, but you will need to change several options:
  - Surface Finish: **ENIG**
  - Layer Stackup: **JLC04161H-7628** (this is critical for the PCIe bus to work!)
  - Impedance Control: **Yes**
    - Select +-10% option (Excel template is included in Gerber zip)
  - Mark on PCB: **Order Number (Specify Position)**
  - Gold Fingers: **Yes**
  - 30° finger chamfered: **No** 
- Check the "PCB Assembly" box and make sure these options are selected:
  - PCBA Type: **Standard** (Economic not available)
  - Assembly Side: **Top Side**
  - Edge Rails/Fiducials: **Added by JLCPCB**
  - Parts Selection: **By Customer**
  - PCBA Qty: although JLC will manufacture PCBs only in multiples of 5, you can choose to have them solder parts onto as few as 2 of them - but doing so usually doesn't save much money.
- Click "Next". Make sure the top side of the PCB is selected, and click "Next" again.
- Upload `riser-v2_top_bom.csv` and `riser-v2_top_cpl.csv`.
- At this point you should see a parts list showing which parts are in stock and which are out of stock. Most likely, the `SI53152-A01AGMR` clock buffer chip and `MDT350M01001VT` right-angle M.2 connector will be out of stock, so you'll need to use JLCPCB's global sourcing tool to order them. If any other parts are out of stock, note those as well.
- If parts are out of stock, you can click "next", choose "Do not place", and "next" again to see what the cost would be excluding the missing parts. Don't actually check out with missing parts, unless you're willing to buy and solder them yourself. If you're just getting an estimate, don't worry about the component placements being just right.
- Go to the [JLCPCB Parts Manager](https://jlcpcb.com/user-center/smtPrivateLibrary/myPartsLib) and click "Global Sourcing Parts".
  - For the clock buffer, search for either `SI53152-A01AGM` or `SI53152-A01AGMR` (these are equivalent parts). Find a supplier with an MOQ (minumum order quantity) less than the number of risers you're making and click "add".
  - Repeat for any other out-of-stock parts.
- Click "Parts Cart" on the left-hand sidebar and make sure "Global Sourcing Parts" near the top is selected. You should see the parts you added. Then check out. What you are doing in this step is paying JLCPCB to source and store those parts for your future order. It usually takes a few weeks for them to arrive, and you'll get an email when that happens.
- Once the parts you ordered are available, repeat the whole process from the top. **Make sure to choose the right Impedance Control and Layer Stackup options if you're starting over.**
- At the "Component Placements" step, click "Select all top parts" and use the arrow keys to move the parts so that they line up with the pads on the board. You can rotate parts 90 degrees at a time with the spacebar.
  - All the R, C, and L parts are symmetric - there's no such thing as the wrong way around.
  - The pins of J4 should be sticking off in space past the end of the board, away from all the other components.
  - Make sure the white circle on IC1 and IC2 is near the corresponding white circle on the PCB.
  - The "out" pin of Y1 should be on the top left side, near the white "Y1" text on the PCB.
  - The + side of D1 should be down towards the PCIe slot.
- Finally, click "save to cart" and check out.

If you use another manufacturer, give them the following PCB specifications:
- Controlled impedance
- Coplanar differential pair (on L1 referenced to L2, and on L4 referenced to L3) of 85 ohms nominal, +/- 10 ohms
- ENIG surface finish with gold fingers
- No chamfer
