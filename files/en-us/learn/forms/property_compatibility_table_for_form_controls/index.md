---
title: CSS property compatibility table for form controls
slug: Learn/Forms/Property_compatibility_table_for_form_controls
tags:
  - Advanced
  - CSS
  - Forms
  - Guide
  - HTML
  - Junk
  - NeedsUpdate
  - Web
---
<div>{{learnsidebar}}</div>

<p>The following compatibility tables try to summarize the state of CSS support for HTML forms. Due to the complexity of CSS and HTML forms, these tables can't be considered a perfect reference. However, they will give you good insight into what can and can't be done, which will help you learn how to do things.</p>

<h2 id="How_to_read_the_tables">How to read the tables</h2>

<h3 id="Values">Values</h3>

<p>For each property, there are four possible values:</p>

<dl>
 <dt>Yes</dt>
 <dd>There's reasonably consistent support for the property across browsers. You may still face strange side effects in certain edge cases.</dd>
 <dt>Partial</dt>
 <dd>While the property works, you may frequently face strange side effects or inconsistencies. You should probably avoid these properties unless you master those side effects first.</dd>
 <dt>No</dt>
 <dd>The property doesn't work or is so inconsistent that it's not reliable.</dd>
 <dt>n.a.</dt>
 <dd>The property has no meaning for this type of widget.</dd>
</dl>

<h3 id="Rendering">Rendering</h3>

<p>For each property there are two possible renderings:</p>

<dl>
 <dt>N (Normal)</dt>
 <dd>Indicates that the property is applied as it is</dd>
 <dt>T (Tweaked)</dt>
 <dd>Indicates that the property is applied with the extra rule below:</dd>
</dl>

<pre class="brush: css">* {
  /* Turn off the native look and feel */
  -webkit-appearance: none;
  appearance: none;

/* for Internet Explorer */
  background: none;
}</pre>

<h2 id="Compatibility_tables">Compatibility tables</h2>

<h3 id="Global_behaviors">Global behaviors</h3>

<p>Some behaviors are common to many browsers at a global level:</p>

<dl>
 <dt>{{cssxref("border")}}, {{cssxref("background")}}, {{cssxref("border-radius")}}, {{cssxref("height")}}</dt>
 <dd>Using one of these properties can partially or fully turn off the native look &amp; feel of widgets on some browsers. Be careful when you use them.</dd>
 <dt>{{cssxref("line-height")}}</dt>
 <dd>This property is supported inconsistently across browsers and you should avoid it.</dd>
 <dt>{{cssxref("text-decoration")}}</dt>
 <dd>This property is not supported by Opera on form widgets.</dd>
 <dt>{{cssxref("text-overflow")}}</dt>
 <dd>Opera, Safari, and IE9 do not support this property on form widgets.</dd>
 <dt>{{cssxref("text-shadow")}}</dt>
 <dd>Opera does not support {{cssxref("text-shadow")}} on form widgets and IE9 does not support it at all.</dd>
</dl>

<h3 id="Text_fields">Text fields</h3>

<p>See the <code>{{htmlelement("input/text", "text")}}</code>, <code>{{htmlelement("input/search", "search")}}</code>, and <code>{{htmlelement("input/password", "password")}}</code> input types.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1][2]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>WebKit browsers (mostly on Mac OSX and iOS) use the native look &amp; feel for the search fields. Therefore, it's required to use <code>-webkit-appearance:none</code> to be able to apply this property to search fields.</li>
     <li>On Windows 7, Internet Explorer 9 does not apply the border unless <code>background:none</code> is applied.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1][2]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>WebKit browsers (mostly on Mac OSX and iOS) use the native look &amp; feel for the search fields. Therefore, it's required to use <code>-webkit-appearance:none</code> to be able to apply this property to search fields.</li>
     <li>On Windows 7, Internet Explorer 9 does not apply the border unless <code>background:none</code> is applied.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1][2]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>WebKit browsers (mostly on Mac OSX and iOS) use the native look &amp; feel for the search fields. Therefore, it's required to use <code>-webkit-appearance:none</code> to be able to apply this property to search fields.</li>
     <li>On Windows 7, Internet Explorer 9 does not apply the border unless <code>background:none</code> is applied.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}<sup>[1]</sup></th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>If the {{cssxref("border-color")}} property is not set, some WebKit based browsers will apply the {{cssxref("color")}} property to the border as well as the font on <code>{{htmlelement("textarea")}}</code>s.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>See the note about {{cssxref("line-height")}}</td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td>See the note about Opera</td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 supports this property only on <code>{{htmlelement("textarea")}}</code>s, whereas Opera only supports it on single line text fields.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>WebKit browsers (mostly on Mac OSX and iOS) use the native look &amp; feel for the search fields. Therefore, it's required to use <code>-webkit-appearance:none</code> to be able to apply this property to search fields. On Windows 7, Internet Explorer 9 does not apply the border unless <code>background:none</code> is applied.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1][2]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>WebKit browsers (mostly on Mac OSX and iOS) use the native look &amp; feel for the search fields. Therefore, it's required to use <code>-webkit-appearance:none</code> to be able to apply this property to search fields. On Windows 7, Internet Explorer 9 does not apply the border unless <code>background:none</code> is applied.</li>
     <li>On Opera the {{cssxref("border-radius")}} property is applied only if an explicit border is set.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 does not support this property.</li>
    </ol>
   </td>
  </tr>
 </tbody>
</table>

<h3 id="Buttons">Buttons</h3>

<p>See the <code>{{htmlelement("input/button", "button")}}</code>,  <code>{{htmlelement("input/submit", "submit")}}</code>, and <code>{{htmlelement("input/reset", "reset")}}</code> input types and the <code>{{htmlelement("button")}}</code> element.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>This property is not applied on WebKit based browsers on Mac OSX or iOS.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>This property is not applied on WebKit based browsers on Mac OSX or iOS.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>See the note about {{cssxref("line-height")}}.</td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes<sup>[1]</sup></td>
   <td>
    <ol>
     <li>On Opera the {{cssxref("border-radius")}} property is applied only if an explicit border is set.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 does not support this property.</li>
    </ol>
   </td>
  </tr>
 </tbody>
</table>

<h3 id="Number">Number</h3>

<p>See the  <code>{{htmlelement("input/number", "number")}}</code> input type. There is no standard way to change the style of spinners used to change the value of the field, with the spinners on Safari being outside the field.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>On Opera, the spinners are zoomed in, which can hide the content of the field.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>On Opera, the spinners are zoomed in, which can hide the content of the field.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>See the note about {{cssxref("line-height")}}.</td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td rowspan="3">
    <p>Supported but there is too much inconsistency between browsers to be reliable.</p>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
  </tr>
 </tbody>
</table>

<h3 id="Check_boxes_and_radio_buttons">Check boxes and radio buttons</h3>

<p>See the <code>{{htmlelement("input/checkbox", "checkbox")}}</code> and <code>{{htmlelement("input/radio", "radio")}}</code> input types.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Some browsers add extra margins and others stretch the widget.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Some browsers add extra margins and others stretch the widget.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
</table>

<h3 id="Select_boxes_single_line">Select boxes (single line)</h3>

<p>See the <code>{{htmlelement("select")}}</code>,  <code>{{htmlelement("optgroup")}}</code> and  <code>{{htmlelement("option")}}</code> elements.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>This property is okay on the <code>{{htmlelement("select")}}</code> element, but it cannot be the case on the <code>{{htmlelement("option")}}</code> or <code>{{htmlelement("optgroup")}}</code> elements.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[2]</sup></td>
   <td>
    <ol>
     <li>The property is applied, but in an inconsistent way between browsers on Mac OSX.</li>
     <li>The property is well applied on the <code>{{htmlelement("select")}}</code> element, but is inconsistently handled on <code>{{htmlelement("option")}}</code> and <code>{{htmlelement("optgroup")}}</code> elements.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>On Mac OSX, WebKit based browsers do not support this property on native widgets and they, along with Opera, do not support it at all on <code>{{htmlelement("option")}}</code> and <code>{{htmlelement("optgroup")}}</code> elements.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>On Mac OSX, WebKit based browsers do not support this property on native widgets and they, along with Opera, do not support it at all on <code>{{htmlelement("option")}}</code> and <code>{{htmlelement("optgroup")}}</code> elements.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 does not support this property on <code>{{htmlelement("select")}}</code>, <code>{{htmlelement("option")}}</code>, and <code>{{htmlelement("optgroup")}}</code> elements; WebKit based browsers on Mac OSX do not support this property on <code>{{htmlelement("option")}}</code> and <code>{{htmlelement("optgroup")}}</code> elements.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 on Windows 7 and WebKit based browsers on Mac OSX do not support this property on this widget.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Only Firefox provides full support for this property. Opera does not support this property at all and other browsers only support it on the <code>{{htmlelement("select")}}</code> element.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1][2]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1][2]</sup></td>
   <td>
    <ol>
     <li>Most of the browsers only support this property on the <code>{{htmlelement("select")}}</code> element.</li>
     <li>IE9 does not support this property.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1][2]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1][2]</sup></td>
   <td>
    <ol>
     <li>Most of the browsers only support this property on the <code>{{htmlelement("select")}}</code> element.</li>
     <li>IE9 does not support this property.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Most of the browsers only support this property on the <code>{{htmlelement("select")}}</code> element.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td rowspan="3">
    <ol>
     <li>Most of the browsers only support this property on the <code>{{htmlelement("select")}}</code> element.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
  </tr>
 </tbody>
</table>

<p>Note Firefox does not provide any way to change the down arrow on the <code>{{htmlelement("select")}}</code> element.</p>

<h3 id="Select_boxes_multiline">Select boxes (multiline)</h3>

<p>See the <code>{{htmlelement("select")}}</code>, <code>{{htmlelement("optgroup")}}</code> and  <code>{{htmlelement("option")}}</code> elements and the <a href="/en-US/docs/Web/HTML/Attributes/size"><code>size</code> attribute</a>.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Opera does not support {{cssxref("padding-top")}} and {{cssxref("padding-bottom")}} on the <code>{{htmlelement("select")}}</code> element.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>See the note about {{cssxref("line-height")}}.</td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 does not support this property on <code>{{htmlelement("select")}}</code>, <code>{{htmlelement("option")}}</code>, and <code>{{htmlelement("optgroup")}}</code> elements; WebKit based browsers on Mac OSX do not support this property on <code>{{htmlelement("option")}}</code> and <code>{{htmlelement("optgroup")}}</code> elements.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 on Windows 7 and WebKit based browser on Mac OSX do not support this property on this widget.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Only supported by Firefox and IE9+.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Most of the browsers only support this property on the <code>{{htmlelement("select")}}</code> element.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes<sup>[1]</sup></td>
   <td>
    <ol>
     <li>On Opera the {{cssxref("border-radius")}} property is applied only if an explicit border is set.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 does not support this property.</li>
    </ol>
   </td>
  </tr>
 </tbody>
</table>

<h3 id="Datalist">Datalist</h3>

<p>See the <code>{{htmlelement("datalist")}}</code> and <code>{{htmlelement("input")}}</code> elements and the <a href="/en-US/docs/Web/HTML/Attributes/list"><code>list</code> attribute</a>.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
</table>

<h3 id="File_picker">File picker</h3>

<p>See the <code>{{htmlelement("input/file", "file")}}</code> input type.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Supported, but there is too much inconsistency between browsers to be reliable.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Many browsers apply this property to the select button.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>It acts more or less like an extra left margin outside the widget.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Supported, but there is too much inconsistency between browsers to be reliable.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 does not support this property.</li>
    </ol>
   </td>
  </tr>
 </tbody>
</table>

<h3 id="Date_pickers">Date pickers</h3>

<p>See the <code>{{htmlelement("input/date", "date")}}</code> and <code>{{htmlelement("input/time", "time")}}</code> input types. Many properties are supported, but there is too much inconsistency between browsers to be reliable.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td></td>
  </tr>
 </tbody>
</table>

<h3 id="Color_pickers">Color pickers</h3>

<p>See the <code>{{htmlelement("input/color", "color")}}</code> input type:</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>Opera handles this like a select widget with the same restriction.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>Opera handles this like a select widget with the same restriction.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td rowspan="3">
    <ol>
     <li>Supported, but there is too much inconsistency between browsers to be reliable.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
  </tr>
 </tbody>
</table>

<h3 id="Meters_and_progress">Meters and progress</h3>

<p>See the <code>{{htmlelement("meter")}}</code> and <code>{{htmlelement("progress")}}</code> elements:</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Chrome hides the <code>{{htmlelement("progress")}}</code> and <code>{{htmlelement("meter")}}</code> element when the {{cssxref("padding")}} property is applied on a tweaked element.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td rowspan="3">
    <ol>
     <li>Supported, but there is too much inconsistency between browsers to be reliable.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
  </tr>
 </tbody>
</table>

<h3 id="Range">Range</h3>

<p>See the <code>{{htmlelement("input/range", "range")}}</code> input type. There is no standard way to change the style of the range grip and Opera has no way to tweak the default rendering of the range widget.</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>Chrome and Opera add some extra space around the widget, whereas Opera on Windows 7 stretches the range grip.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td>
    <ol>
     <li>The {{cssxref("padding")}} is applied, but has no visual effect.</li>
    </ol>
   </td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td rowspan="3">
    <ol>
     <li>Supported, but there is too much inconsistency between browsers to be reliable.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 153, 153); vertical-align: top;">No<sup>[1]</sup></td>
  </tr>
 </tbody>
</table>

<h3 id="Image_buttons">Image buttons</h3>

<p>See the <code>{{htmlelement("input/image", "image")}}</code> input type:</p>

<table>
 <thead>
  <tr>
   <th scope="col">Property</th>
   <th scope="col" style="text-align: center;">N</th>
   <th scope="col" style="text-align: center;">T</th>
   <th scope="col">Note</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>CSS box model</em></th>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("width")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("height")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("border")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("margin")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="vertical-align: top;">{{cssxref("padding")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Text and font</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("color")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("font")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("letter-spacing")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-align")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-decoration")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-indent")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-overflow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-shadow")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("text-transform")}}</th>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td style="text-align: center; vertical-align: top;">N.A.</td>
   <td></td>
  </tr>
 </tbody>
 <tbody>
  <tr>
   <th colspan="4" scope="col"><em>Border and background</em></th>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("background")}}</th>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td style="text-align: center; background-color: rgb(204, 255, 102); vertical-align: top;">Yes</td>
   <td></td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("border-radius")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 does not support this property.</li>
    </ol>
   </td>
  </tr>
  <tr>
   <th scope="row" style="white-space: nowrap; vertical-align: top;">{{cssxref("box-shadow")}}</th>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td style="text-align: center; background-color: rgb(255, 255, 102); vertical-align: top;">Partial<sup>[1]</sup></td>
   <td>
    <ol>
     <li>IE9 does not support this property.</li>
    </ol>
   </td>
  </tr>
 </tbody>
</table>

<h2 id="See_also">See also</h2>

<h3 id="Learning_path">Learning path</h3>

<ul>
 <li><a href="/en-US/docs/Learn/Forms/Your_first_form">Your first HTML form</a></li>
 <li><a href="/en-US/docs/Learn/Forms/How_to_structure_a_web_form">How to structure an HTML form</a></li>
 <li><a href="/en-US/docs/Learn/Forms/Basic_native_form_controls">The native form widgets</a></li>
 <li><a href="/en-US/docs/Learn/Forms/HTML5_input_types">HTML5 input types</a></li>
 <li><a href="/en-US/docs/Learn/Forms/Other_form_controls">Additional form controls</a></li>
 <li><a href="/en-US/docs/Learn/Forms/UI_pseudo-classes">UI pseudo-classes</a></li>
 <li><a href="/en-US/docs/Learn/Forms/Styling_web_forms">Styling HTML forms</a></li>
 <li><a href="/en-US/docs/Learn/Forms/Form_validation">Form data validation</a></li>
 <li><a href="/en-US/docs/Learn/Forms/Sending_and_retrieving_form_data">Sending form data</a></li>
</ul>

<h3 id="Advanced_Topics">Advanced Topics</h3>

<ul>
 <li><a href="/en-US/docs/Learn/Forms/Sending_forms_through_JavaScript">Sending forms through JavaScript</a></li>
 <li><a href="/en-US/docs/Learn/Forms/How_to_build_custom_form_controls">How to build custom form widgets</a></li>
 <li><a href="/en-US/docs/Learn/Forms/HTML_forms_in_legacy_browsers">HTML forms in legacy browsers</a></li>
 <li><a href="/en-US/docs/Learn/Forms/Advanced_form_styling">Advanced styling for HTML forms</a></li>
 <li><a href="/en-US/docs/Learn/Forms/Property_compatibility_table_for_form_controls">Property compatibility table for form widgets</a></li>
</ul>