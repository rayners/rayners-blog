---
---
I use [OrgMode][orgmode] to manage my task list and I am trying to make it into my main calendar.  One of the things I keep in mind as I work my way through the various configuration options and customizations is that I want to use [OrgMode][orgmode] as little as possible; do what I need to do with it and get back to what I am actually doing.

One of the big problems in that realm that I have run into is that it takes effort for me to view my agenda and to-do list.  Yes, it's a _small_ effort to type `C-c a a` when I'm in emacs, but I still have to remember to do that so I can check it.  Enter [GeekTool][geektool].

With [GeekTool][geektool], among other things, I can stick the output of any shell command onto my desktop.  And [OrgMode][orgmode] has some handy functionality to [extract agenda information](http://orgmode.org/manual/Extracting-agenda-information.html), so I set up a custom agenda to use for [GeekTool][geektool]:

From [`~/.emacs.d/rayners/org.el`](http://github.com/rayners/emacs.d/blob/master/rayners/org.el):

<!--
<style type="text/css">
.highlight .hll { background-color: #ffffcc }
.highlight  { background: #ffffff; }
.highlight .c { color: #808080 } /* Comment */
.highlight .err { color: #F00000; background-color: #F0A0A0 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #303030 } /* Operator */
.highlight .cm { color: #808080 } /* Comment.Multiline */
.highlight .cp { color: #507090 } /* Comment.Preproc */
.highlight .c1 { color: #808080 } /* Comment.Single */
.highlight .cs { color: #cc0000; font-weight: bold } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #808080 } /* Generic.Output */
.highlight .gp { color: #c65d09; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0040D0 } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #003080; font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #303090; font-weight: bold } /* Keyword.Type */
.highlight .m { color: #6000E0; font-weight: bold } /* Literal.Number */
.highlight .s { background-color: #fff0f0 } /* Literal.String */
.highlight .na { color: #0000C0 } /* Name.Attribute */
.highlight .nb { color: #007020 } /* Name.Builtin */
.highlight .nc { color: #B00060; font-weight: bold } /* Name.Class */
.highlight .no { color: #003060; font-weight: bold } /* Name.Constant */
.highlight .nd { color: #505050; font-weight: bold } /* Name.Decorator */
.highlight .ni { color: #800000; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #F00000; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0060B0; font-weight: bold } /* Name.Function */
.highlight .nl { color: #907000; font-weight: bold } /* Name.Label */
.highlight .nn { color: #0e84b5; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #007000 } /* Name.Tag */
.highlight .nv { color: #906030 } /* Name.Variable */
.highlight .ow { color: #000000; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mf { color: #6000E0; font-weight: bold } /* Literal.Number.Float */
.highlight .mh { color: #005080; font-weight: bold } /* Literal.Number.Hex */
.highlight .mi { color: #0000D0; font-weight: bold } /* Literal.Number.Integer */
.highlight .mo { color: #4000E0; font-weight: bold } /* Literal.Number.Oct */
.highlight .sb { background-color: #fff0f0 } /* Literal.String.Backtick */
.highlight .sc { color: #0040D0 } /* Literal.String.Char */
.highlight .sd { color: #D04020 } /* Literal.String.Doc */
.highlight .s2 { background-color: #fff0f0 } /* Literal.String.Double */
.highlight .se { color: #606060; font-weight: bold; background-color: #fff0f0 } /* Literal.String.Escape */
.highlight .sh { background-color: #fff0f0 } /* Literal.String.Heredoc */
.highlight .si { background-color: #e0e0e0 } /* Literal.String.Interpol */
.highlight .sx { color: #D02000; background-color: #fff0f0 } /* Literal.String.Other */
.highlight .sr { color: #000000; background-color: #fff0ff } /* Literal.String.Regex */
.highlight .s1 { background-color: #fff0f0 } /* Literal.String.Single */
.highlight .ss { color: #A06000 } /* Literal.String.Symbol */
.highlight .bp { color: #007020 } /* Name.Builtin.Pseudo */
.highlight .vc { color: #306090 } /* Name.Variable.Class */
.highlight .vg { color: #d07000; font-weight: bold } /* Name.Variable.Global */
.highlight .vi { color: #3030B0 } /* Name.Variable.Instance */
.highlight .il { color: #0000D0; font-weight: bold } /* Literal.Number.Integer.Long */
</style>
-->
<style type="text/css">
.highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #008800; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #AA22FF; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .cm { color: #008800; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #008800 } /* Comment.Preproc */
.highlight .c1 { color: #008800; font-style: italic } /* Comment.Single */
.highlight .cs { color: #008800; font-weight: bold } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #808080 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0040D0 } /* Generic.Traceback */
.highlight .kc { color: #AA22FF; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #AA22FF; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #AA22FF; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #AA22FF } /* Keyword.Pseudo */
.highlight .kr { color: #AA22FF; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #00BB00; font-weight: bold } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BB4444 } /* Literal.String */
.highlight .na { color: #BB4444 } /* Name.Attribute */
.highlight .nb { color: #AA22FF } /* Name.Builtin */
.highlight .nc { color: #0000FF } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #00A000 } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #B8860B } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sb { color: #BB4444 } /* Literal.String.Backtick */
.highlight .sc { color: #BB4444 } /* Literal.String.Char */
.highlight .sd { color: #BB4444; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BB4444 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BB4444 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BB4444 } /* Literal.String.Single */
.highlight .ss { color: #B8860B } /* Literal.String.Symbol */
.highlight .bp { color: #AA22FF } /* Name.Builtin.Pseudo */
.highlight .vc { color: #B8860B } /* Name.Variable.Class */
.highlight .vg { color: #B8860B } /* Name.Variable.Global */
.highlight .vi { color: #B8860B } /* Name.Variable.Instance */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
</style>

{% highlight cl %}
    (setq org-agenda-custom-commands
          '(
            ;; ...
            ("G" "Geektool agenda"
             ((agenda "")
              (alltodo))
             ((org-agenda-ndays 1)
              (org-deadline-warning-days 7))
             ("~/agenda.txt"))
            ))
{% endhighlight %}

Which translates to roughly: today's agenda, all my to-do items and warnings for any deadlines in the next week.

<a href="http://rayners.org/assets_c/2010/10/GeekTool-20101024-011514-20.html" onclick="window.open('http://rayners.org/assets_c/2010/10/GeekTool-20101024-011514-20.html','popup','width=624,height=410,scrollbars=no,resizable=no,toolbar=no,directories=no,location=no,menubar=no,status=no,left=0,top=0'); return false"><img src="http://rayners.org/assets_c/2010/10/GeekTool-20101024-011514-thumb-200x131-20.jpg" width="200" height="131" alt="GeekTool-20101024-011514.jpg" class="mt-image-right" style="float: right; margin: 0 0 20px 20px;" /></a>

Next, I added a geeklet in [GeekTool][geektool] that runs the following command: 

{% highlight sh %}
    /path/to/emacs --batch \
        -l ~/.emacs.d/init.el \
        -eval '(org-batch-agenda "G")'
{% endhighlight %}

 `--batch` nixes the use of my personal emacs customization files, so that's what the `-l ~/.emacs.d/init.el` part is for.

[OrgMode][orgmode] also has a CSV agenda export function that might warrant some exploring in the not too distant future.  If nothing else, it might be a useful link the tool-chain to connect all my various calendars.

  [orgmode]: http://orgmode.org/
  [geektool]: http://projects.tynsoe.org/en/geektool/
