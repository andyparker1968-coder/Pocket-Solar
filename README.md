# Pocket Solar

Standalone static calculator. The calculator needs only `index.html`; its logo
and browser favicon are embedded, so the `icons/` folder is not needed. The
package also includes `apple-touch-icon.png` beside `index.html` for an iPhone
or iPad Home Screen shortcut when both files are hosted together. The
calculator uses no backend or external API.

The refreshed default uses a white background, light-grey panels (`#eef0f2`),
dark supporting text, Rounded font, and bold headings. The in-app logo is
embedded in the HTML, and the mobile layout uses narrower safe-area gutters and
fewer card borders.

Solar and battery purchase costs default to £0.00. The total and estimated
payback include the battery cost only while “Include battery in totals” is
checked; unchecking it excludes the battery's energy effects and purchase cost.
Payback is included purchase costs divided by projected annual savings.

Solar panel capacity and average solar output are entered in kW: for example,
800 W is 0.800 kW. In Solar setup, enter average home use during peak windows and
off-peak home use in kWh/h, plus the Morning and Evening peak times. This home
demand profile is used for the solar-only estimate whether or not a battery is
included. During Solar times, the model applies the matching peak or off-peak
home-use rate to estimate direct solar use and surplus export. Solar energy in
kWh is calculated as kW × hours. Existing browser-saved solar W values are
converted to kW once when the calculator loads the updated version.

The one-day, 30-day, and one-year summaries estimate grid kWh used from modeled
household demand, less solar used at home and battery energy supplied to home
demand outside Charge times, plus grid energy used to charge the battery. The
quick breakdown separately reports total battery charge input from solar and
grid. Solar charging does not import energy from the grid. The energy-impact row
says “Grid kWh saved” when the net effect is positive and “Extra grid kWh used”
when grid charging exceeds the modeled solar and battery import reductions; a
negative effect can still lower the bill if charging happens at a cheaper tariff.

## Home Screen icon

Safari needs a publicly reachable image linked from the page head for a
reliable iPhone or iPad Home Screen icon. The standalone HTML links to the
included 180 × 180 `apple-touch-icon.png`. When embedding Pocket Solar in a
Squarespace code block, the code block cannot set the page's head icon: upload
`apple-touch-icon.png` to Squarespace and either set it as the site's iOS icon
or add this link in Squarespace's head code injection, replacing the URL with
the public URL for the uploaded image:

```html
<link rel="apple-touch-icon" sizes="180x180" href="https://YOUR-PUBLIC-ICON-URL">
```

If you change the icon, remove the existing Home Screen shortcut and add it
again so iOS fetches the updated image.

## Battery estimate

The optional battery section is off by default, can be rolled up, and saves its
inputs in the existing browser-local calculator storage. Capacity is entered in
kWh; charging and discharging power is entered in kW.

The estimate treats “Minimum discharge” as the state-of-charge reserve: the model
assumes the battery starts at this level and does not discharge below it. Solar
serves daytime home demand first. With “Solar first, then grid top-up” selected,
surplus solar charges the battery before export; grid power can top it up during
Charge times if needed. With “Grid only” selected, surplus solar is exported and
the battery charges from grid during Charge times. Solar charging is valued at
the feed-in tariff (export income given up). The £0.07/kWh default grid charging
tariff applies only to grid energy used during Charge times; set it to the actual
rate for that window. The charge cost includes solar export value and any
Charge-times grid spend.

The Morning and Evening peak windows and home-use rates are set in Solar setup;
each time window accepts 24-hour clock times, and an end time earlier than its
start is treated as crossing midnight. The two peak windows must not overlap.
These settings determine modeled daily household demand and solar-only use even
when the battery is off. When included, the battery can supply modeled peak and
off-peak home demand outside Charge times; demand during the Charge window is
excluded from battery discharge. Solar used directly at home reduces the demand
the battery is modeled to cover. The selected charge/discharge power, available
energy above reserve, modeled demand, and eligible hours limit battery supply.
The model allocates battery discharge to the Morning peak, then the Evening peak,
then off-peak home use. The schedule and result text report the off-peak portion
as well as peak supply.

The Solar setup's standard import tariff is used for solar energy used at home
and for battery energy supplied in both peak windows and all off-peak hours
outside Charge times. “Off-peak home use” is the modeled kWh demand outside both
peak windows; it does not mean those household imports receive a cheaper rate.
The separate Charge-times grid tariff values only grid energy used inside the
configured charging window, so the discounted rate does not apply to home use
outside that window. Missing required rates are not silently treated as zero.

Existing saved tariff values from the previous p/kWh format are converted
automatically; saved Peak times are retained as the Evening peak window.

For example, 3.5 kW over a 2-hour Charge-times grid window supplies at most 7 kWh
from the grid. At 95% charging efficiency, that stores up to 6.65 kWh. In solar-first
mode, any charge already stored from solar is subtracted before this grid top-up
limit is applied.

It assumes 95% charge and 95% discharge efficiency (about 90% round trip) and
uses the selected power limit for charging and for supply to home demand. The net
battery adjustment is avoided peak and off-peak import cost less Charge-times
grid charging cost and solar export value forgone. The daily total adds this
battery net adjustment to the separately displayed solar-only benefit. Charge
remaining after modeled home use is not credited as a later saving. The status
text identifies whether the target, available solar, charging window, home demand
or power limit is constraining the estimate. The monthly and annual figures assume
this modeled cycle repeats.

The battery result shows the percentage of capacity added, the source split, and
the projected state-of-charge change. Its charge-cost card combines solar export
value and grid top-up spend when both sources contribute. It estimates Solar-time
and Charge-time use separately and reports any remaining shortfall if the target
cannot be reached.

The Off-peak home use rate models demand outside both peak windows; the battery
can supply that demand only in portions of those hours outside Charge times. Peak
kWh totals use the Home use during peak windows rate, adjusted for Charge-time
overlap and direct solar use. Both demand rates and both peak windows remain
available in Solar setup when the battery is off.

## Daily schedule chart

The chart at the bottom plots Solar, Charge, Morning peak and Evening peak windows
on one 00:00–24:00 timeline. “Off peak home usage” is the time outside both peak
windows; it is not a charging window. Solar charging uses surplus during Solar
times; Charge times mark the grid-only or top-up opportunity. The chart shows
potential battery discharge in each peak and reports the modeled off-peak battery
supply beside off-peak home use, along with estimated remaining capacity after
Morning use and after both peaks. Overnight
windows appear as segments on both sides of 00:00. Peak periods are red. The
Charge-times bar crosshatches the estimated hours actually used for grid charging,
starting at the beginning of the Charge window; this indicates timing, not energy
volume. The off-peak and peak descriptions include modeled kWh totals based on
their respective home-use rates. The Charging strategy selector uses the selected
Background colour. Solar/Charge/peak time inputs, the calculated Solar/Charge and peak-hour
fields, the surplus-output box, and battery charge/result cards use the Background
colour selected in Customise appearance. Text and accents continue to use their
selected appearance colours. The battery roll-up and Include battery controls use
the selected Background colour with accent-coloured text, matching the Setup roll-up.