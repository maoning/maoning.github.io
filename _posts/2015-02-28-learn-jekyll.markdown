---
title:  "Notes for Creating Pages Using jekyll"
date:   2015-02-27 23:26:59
categories: jekyll 
---
### Serve
`jekyll serve`

### Hightlighting
Short Name for code highlighting using Pygments [lookup][Pygments]
Extra Args for Highlighting: `linenos` => line numbers

### Build
Set default source and destination dirs inside `_config.yml`

{% highlight bash %}
$ jekyll build --source <source> --destination <destination>
# => The <source> folder will be generated into <destination>
{% endhighlight %}

[Pygments]:    http://pygments.org/docs/lexers/
