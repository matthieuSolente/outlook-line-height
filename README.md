# The line-height property and Outlook (Windows)
A brief summary of knowledge about the line-height property in Outlook



## For percentage values, Outlook renders them as is.

Example:

`line-height: 200%`

Becomes:

`line-height: 200%`

For percentage values with decimal, for example, 117.5%, Outlook ignores decimals and rounds down (e.g., 117.5%->117% and 117.9%->117%) similarly (Math.floor js function).

➤ You can use percentage value only, as long as it is not with decimal.

## For values in em format, Outlook completely ignores them.

Example :

`font-size: 24px; line-height: 1.5em`

becomes

`font-size: 24px;`

➤ Don't rely only en em value.

## The `mso-line-height-alt` properties become a simple `line-height` in Outlook.

Example:

`line-height:1.5; mso-line-height-alt:131.25%`

becomes

`line-height:131%`

## mso-line-height-rule only applies to pixel units.

➤ if you use percentage or unitless values (em values do not apply since Outlook ignores them) the mso-line-height-rule property is useless because it is not interpreted by Outlook

## Values without units are interpreted as percentages.

Example:

`line-height:2`

becomes

`line-height:200%`

## For values without units and with decimals, Outlook converts them to percentages by rounding down.

Example:

`line-height: 2.6 or line-height: 2.1`

becomes

`line-height: 200%`

➤ You can rely only on unitless value without adding a specific rule for Outlook, as long as it is without decimal

## When a value without units is mixed with a percentage, it will favor the percentage.

Example:

`line-height:2; mso-line-height-alt:175% or line-height:1.5; mso-line-height-alt:120%`

becomes

`line-height:175% or line-height:120%`

➤ Unless you need to have a different line-height on Outlook, it seems useless to combine unitless value (without decimal) with mso specific percentage.You might as well use either the rounded value without unit or the percentage only.

## When specifying a value in pixels, Outlook translates it into points.

Example:

`line-height:24px`

becomes

`line-height:18pt`

➤ No need to do the pixel-to-point calculation, Outlook does it all by itself

## When specifying a value in both em and pixels, Outlook favors the pixel (which it changes to points. A pixel value is present, so it maintains the mso-line-height-rule rule).

Example:

`line-height: 1.5em; mso-line-height-alt: 21px; mso-line-height-rule: exactly;`

becomes

`line-height:15.75pt; mso-line-height-rule:exactly;`

## When specifying a value in both pixel and percentage, Outlook favors percentage.

Example

`line-height: 21px; mso-line-height-alt:190%; mso-line-height-rule: exactly;`

becomes

`line-height:190%;`

Here we see that unlike the previous example mixing em and pixel, Outlook by favoring the percentage, ignores the mso-line-height-rule rule

➤This scenario seems inappropriate. For a more accurate rendering, use only the pixel value.

## Whatever combination you make, if you use the keyword "normal" or a number (eg1.1) in the mso-line-height-alt declaration, that will completely erase all line-height declaration

Example

`line-height: 21px; mso-line-height-alt:1.4; mso-line-height-rule: exactly;`

becomes

'' (nothing)

## Things to consider
In this article :
[text_guidance](https://www.inclusivedesigntoolkit.com/text_guidance/#sufficientspacing:~:text=Ensuring%20sufficient%20line%20spacing)

we can read :

"* *A good rule of thumb is to set the gap between successive lines of text should usually be about 1.5 times the x-height (or more). In Microsoft Office products, with Arial text, this effect is achieved with a line spacing of 1.1, but with Times New Roman, the same effect is achieved with a line spacing of 1.0.* *"

It's pointless to seek strict rendering equivalence between different mailboxes. The final line height varies from one font to another, and from one mailbox to another.

Example: If you use a web font in your email and set the line height (e.g. to 1/2 or 1.5em or 2em, or 21px or 150%) on Outlook, it will be rendered with a web-safe font (Arial, Verdana, Helvetica, etc.) on which this value will produce a completely different result.

Conclusion
- Em is simply ignored
- Value without unit are accepted but without decimal.
- Percentage are accepted but without decimal
- If you use value with decimal,eg 1.5/1.5em/ combine it with percentage without decimal, or with pixel or point value
- Pixel is converted to point
- mso-line-height-rule works only with pixel (or point, but anyway Outlook convert it in point), so no need to add it if you use unitless value or percentage
- If you use unitless value and percentage, Outlook will only take the percentage.
- If you use em value and percentage, Outlook will only take the percentage.
- If you use em value and pixel, Outlook will only take the pixel (converted to point).
- If you use pixel value and percentage, Outlook will only take the percentage.
