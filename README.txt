THE PHANTOM WEIGHT FINDER — free giveaway from "Build It With AI" (Episode 28)

What it is
----------
A Google Sheet with one extra menu. It reads your own USPS package log and works out what
each package is billed at under the dimensional-weight rule in force since July 12, 2026,
flags every package billed above its real weight ("phantom weight"), prices the difference
from YOUR rate card, and tells you which of your box sizes trigger the rule. It sends
nothing, buys nothing and talks to nothing outside your spreadsheet.

The rule it applies (USPS Postal Bulletin 22705, effective July 12, 2026)
-----------------------------------------------------------------------
- Round each side UP to the next whole inch (12.25 becomes 13; 12 stays 12).
- Multiply the three. If the result is MORE than 1,728 cubic inches, divide by 139 and round
  up to the next whole pound: that is the dimensional weight.
- Round the real weight up to the next whole pound. You are billed the bigger of the two.
- Priority Mail Express, Priority Mail, Ground Advantage and Parcel Select.
- Cubic-priced services use their own tiers: the sheet sets them aside and says so.

How to set it up (about five minutes)
-------------------------------------
1. Make a new Google Sheet with four tabs named exactly:
     Packages : Order | Service | Length | Width | Height | Weight     (inches, pounds)
     Boxes    : Box | Length | Width | Height | Box cost (optional)   (your box sizes; cost per box)
     Rates    : Service | Pounds | Price                              (your own rate card, one zone)
     Settings : Setting | Value   (optional: divisor 139, threshold 1728)
   Headers on row 1, any column order, extra columns are ignored. To try it first,
   File > Import the three sample CSVs from the bundle into those tabs.
2. Extensions > Apps Script. Delete what is there, paste in phantom.gs, save.
3. Reload the sheet. A "Phantom Weight" menu appears. Click Find phantom weight.
   (The first run asks you to authorize the script to read and write THIS spreadsheet.)
4. Read the "Phantom Weight" tab it writes.

If the top line of the report says DO NOT TRUST THESE WEIGHTS, believe it: a header row was
unreadable, the counts did not add up, the money did not re-add, more than 10% of rows were
refused, your rate card had no usable rows, a box cost was unreadable, or the box savings
did not re-add. The reason is printed beside it.

In the bundle (Phantom_Weight_Finder_BUNDLE.zip)
------------------------------------------------
- phantom.gs                 the tool (paste into Apps Script)
- sample_packages.csv, sample_boxes.csv, sample_rates.csv
                             Hollow Pine Candle Company: a made-up shop, a made-up month,
                             a made-up rate card and made-up box costs. Replace them with your own.
- checker.py                 independent Python checker, written from the rules alone —
                             run: python3 checker.py sample_packages.csv sample_boxes.csv sample_rates.csv
- phantom_v1_FIRST_BUILD_NOT_THE_TOOL.gs   the first build from the episode — WRONG
- phantom_v2_SECOND_BUILD_NOT_THE_TOOL.gs  the second build — closer, still wrong three ways
- PROMPTS.txt                the three prompts, word for word, in the order they were sent
- SPEC.md                    the written rules both the sheet and the checker follow

v1.1 changelog (November 14, 2026)
----------------------------------
Added after a viewer pointed out that a smaller box isn't free: the postage a box swap saves
can be eaten by what the new box (and its fill) costs.
- Boxes takes an optional "Box cost" column: what one box costs you, with its fill.
- For every package the sheet suggests a smaller box for, the report now also shows the box
  cost change and the NET saving (postage saved minus the extra box cost). A swap whose net is
  zero or less is marked SWAP NOT WORTH IT. If a cost is missing it says "add box costs to see
  the net" and leaves the net blank — it never guesses.
- A BOX SWAPS line totals the postage saved, the box cost change and the net, over the swaps
  where every number is known, and the self-audit re-adds that net to the cent.
- In the sample, moving a Bulk 3 package (HP-4132, Ground Advantage) into the Gift set box
  saves $9.45 of postage but the gift box costs $9.85 more: net -$0.40, SWAP NOT WORTH IT.
- Without a Box cost column the sheet behaves exactly like v1.0. Every number in Episode 28
  comes from the same three sample files; the only change to them is the new Box cost column
  in sample_boxes.csv (the sizes are unchanged).
- PROMPTS.txt is unchanged: it is the record of what was actually sent in the episode.

Honest limits
-------------
It knows this one USPS rule. It does not know other carriers' rules, it does not check
cubic-priced services, and it does not know your zones: the money is only as good as the
rate card you paste. Its box suggestion is the largest of YOUR boxes that is smaller than the
one you used and would not be billed above that package's weight; it cannot know whether
your product fits, and it treats a package's current box as the first box in your list with
the same rounded sides. Box costs are only as good as the numbers you type. Check anything that
matters against your carrier invoices.
Sample data is fictional. Not shipping or accounting advice.
