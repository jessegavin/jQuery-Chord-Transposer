# jQuery Chord Transpose Plugin

This jQuery plugin will add a toolbar to any plain text guitar chord music chart allowing the user to transpose the chords of the song with a single click.

Demo [https://jquery-chord-transposer.now.sh/](https://jquery-chord-transposer.now.sh/)

## Example Usage
Suppose you have HTML markup like the following.

    <pre data-key="C">
           C              G                 Am          F
    When I find myself in times of trouble, Mother Mary comes to me
    C                 G              F   C/E   Dm   C
    Speaking words of wisdom, let it be

        C             G                Am                F
    And in my hour of darkness, She is standing right in front of me
    C                 G              F   C/E   Dm   C
    Speaking words of wisdom, let it be

           Am         G          F          C
    Let it be, let it be, let it be, let it be
                     G              F   C/E   Dm   C
    Whisper words of wisdom, let it be
    </pre>

You would simply use the plugin like this.

    <script type="text/javascript" src="jquery.transposer.js"></script>
    <script type="text/javascript">
      $(function() {
        $("pre").transpose();
      });
    </script>

By default, the script will try to determine the starting key of the song by looking for a data-key attribute on the containing element. However, you have the option of specifying the starting key with a settings object like the following example.

    <script type="text/javascript">
      $(function() {
        $("pre").transpose({ key : 'C' });
      });
    </script>

## Plugin Requirements
The element you're targeting is either a `<pre>` tag or uses the `white-space: pre` CSS declaration.
The font is monospaced. It really won't be useful otherwise since the chords are position over the correct text using white space.
Lines with chords contain chords only. The script will examine each bit of text on the line to see if it matches a regular expression which is meant to find chords. If any chunk of text in that line does not match, it will be skipped. The only non-alphanumeric character that is allowed on chord lines (beside `#`) is / when it is used to show a chord with a bass note like `G/B`.

### Regarding chord spacing
Always make sure that chords (that don't have a sharp `#` or flat `b` after them) are followed by at least two spaces otherwise the chords might get 'smushed' together when transposed. In the following example, if the song were transposed from `G` to `F#`, the white space which follows the G chord will be taken up by the `#` character (same is true with D chord).

    G C    D G    >>>   F#B    C#F#
    I love music  >>>   I love music
    
If you have at least two spaces after each chord, this will not happen. Here's a suggested change for the previous example.

    G  C    D  G    >>>   F# B    C# F#
    I  love mu-sic  >>>   I  love mu-sic
    
Chords like G/B should have at least three spaces following them because if the song were transposed to `F#` the chord would take a total of five characters `F#/A#` instead of the original three.
