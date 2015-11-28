# Concordion Markdown Configuration

## Saving Source HTML
For debug purposes, you may wish to save a copy of the interim HTML that is generated by the Markdown extension, and used as the input specification to Concordion.

To save a copy, call the method [withSourceHtmlSavedTo(Target target)](http://concordion.github.io/concordion-markdown-extension/api/org/concordion/ext/MarkdownExtension.html#withSourceHtmlSavedTo-org.concordion.api.Target-), for example:

    @Extension
    public MarkdownExtension extension = new MarkdownExtension().withSourceHtmlSavedTo(new FileTarget(new File("/tmp/concordion")));

## Markdown Syntax Extensions
The underlying Markdown parser is [Pegdown](https://github.com/sirthias/pegdown), which allows for an [extended Markdown syntax](https://github.com/sirthias/pegdown/blob/master/README.markdown#introduction).

The extension is already adding the TABLES and STRIKETHRU extensions to enable its syntax.

Should you wish to add further Pegdown extensions, call the method [withPegdownExtensions(int options)](http://concordion.github.io/concordion-markdown-extension/api/org/concordion/ext/MarkdownExtension.html#withPegdownExtensions-int-) where `options` is a bitmask of the required [extensions](http://www.decodified.com/pegdown/api/org/pegdown/Extensions.html), for example:

    @Extension
    public MarkdownExtension extension = new MarkdownExtension().withPegdownExtensions(Extensions.WIKILINKS | Extensions.QUOTES);

### [No extra extensions](- "no-extra-extensions")

Without additional extensions, the following are translated as-is.

<div class="example">
  <h3>Example</h3>
  <table concordion:execute="#html=translate(#md)">
    <tr>
      <th concordion:set="#md">Markdown</th>
      <th concordion:assertEquals="#html">Resulting HTML</th>
    </tr>
    <tr>
      <td>[[not a wikilink]]</td>
      <td>[[not a wikilink]]</td>
    </tr>
    <tr>
      <td>"pretty quotes"</td>
      <td>"pretty quotes"</td>
    </tr>
  </table>
</div>
 
### [With WIKILINKS and QUOTES extensions](- "extra-extensions")

Given the method `withPegdownExtensions(int options)` has been [called](- "withWikilinkAndQuotes()") with `options` set to `org.pegdown.Extensions.WIKILINKS | org.pegdown.Extensions.QUOTES`, the following are now translated as shown:

<div class="example">
  <h3>Example</h3>
  <table concordion:execute="#html=translate(#md)">
    <tr>
      <th concordion:set="#md">Markdown</th>
      <th concordion:assertEquals="#html">Resulting HTML</th>
    </tr>
    <tr>
      <td>[[wikilink]]</td>
      <td>&lt;a href="./wikilink.html">wikilink&lt;/a></td>
    </tr>
    <tr>
      <td>"pretty quotes"</td>
      <td>&amp;ldquo;pretty quotes&amp;rdquo;</td>
    </tr>
  </table>
</div>

