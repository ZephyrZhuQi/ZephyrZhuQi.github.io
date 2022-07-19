---
layout: page
permalink: /publications/
title: Publications
pubs:

    - title:   "Simple is not Easy: A Simple Strong Baseline for TextVQA and TextCaps"
      author:  "**Qi Zhu**, Chenyu Gao, Peng Wang, Qi Wu"
      journal: "Association for the Advancement of Artificial Intelligence"
      note:    "AAAI"
      year:    "2021"
      url:     "https://arxiv.org/abs/2012.05153"
      # doi:     "http://dx.doi.org"
      image:   "/images/ssbaseline.png"
      # media:
        # - name: "IMDB"
          # url:  "http://www.imdb.com/title/tt0133093/"

    - title:   "Chop Chop BERT: Visual Question Answering by Chopping VisualBERT’s Heads"
      author:  "Chenyu Gao, **Qi Zhu**, Peng Wang, Qi Wu"
      journal: "International Joint Conferences on Artificial Intelligence"
      note:    "IJCAI"
      year:    "2021"
      url:     "https://arxiv.org/abs/2104.14741"
      # doi:     "http://dx.doi.org"
      image:   "/images/chop.png"
      # media:
        # - name: "IMDB"
          # url:  "http://www.imdb.com/title/tt0133093/"

    - title:   "Structured Multimodal Attentions for TextVQA"
      author:  "Chenyu Gao, **Qi Zhu**, Peng Wang
, Hui Li, Yuliang Liu, Anton van den Hengel, Qi Wu"
      journal: "IEEE Transactions on Pattern Analysis and Machine Intelligence"
      # note:    "(presented at Oz)"
      year:    "2020"
      url:     "https://arxiv.org/abs/2006.00753"
      # doi:     "http://dx.doi.org"
      image:   "/images/sma.png"
      # media:
        # - name: "IMDB"
          # url:  "http://www.imdb.com/title/tt0133093/"

    # - title:   "Paper title in 3-7 words that sound like Clingon"
    #   author:  "M. McFly, D. Kirk, L. Skywalker, H.J. Potter, I. Jones, H. Houdini"
    #   journal: "Transactions on Black Magic"
    #   note:    "(presented at Oz)"
    #   year:    "2014"
    #   url:     "http://publish-more-stuff.org"
    #   doi:     "http://dx.doi.org"
    #   image:   "https://images.duckduckgo.com/iu/?u=http%3A%2F%2Fimages.moviepostershop.com%2Fthe-matrix-movie-poster-1999-1020518087.jpg&f=1"
    #   media:
    #     - name: "IMDB"
    #       url:  "http://www.imdb.com/title/tt0133093/"

    # - title:   "Paper title in 3-7 words that sound like Clingon"
    #   author:  "M. McFly, D. Kirk, L. Skywalker, H.J. Potter, I. Jones, H. Houdini"
    #   journal: "Transactions on Black Magic"
    #   note:    "(presented at Oz)"
    #   year:    "2013"
    #   url:     "http://publish-more-stuff.org"
    #   doi:     "http://dx.doi.org"
    #   image:   "https://images.duckduckgo.com/iu/?u=http%3A%2F%2Fimages.moviepostershop.com%2Fthe-matrix-movie-poster-1999-1020518087.jpg&f=1"
    #   media:
    #     - name: "IMDB"
    #       url:  "http://www.imdb.com/title/tt0133093/"

    # - title:   "Paper title in 3-7 words that sound like Clingon"
    #   author:  "M. McFly, D. Kirk, L. Skywalker, H.J. Potter, I. Jones, H. Houdini"
    #   journal: "Transactions on Black Magic"
    #   note:    "(presented at Oz)"
    #   year:    "2012"
    #   url:     "http://publish-more-stuff.org"
    #   doi:     "http://dx.doi.org"
    #   image:   "https://images.duckduckgo.com/iu/?u=http%3A%2F%2Fimages.moviepostershop.com%2Fthe-matrix-movie-poster-1999-1020518087.jpg&f=1"
    #   media:
    #     - name: "IMDB"
    #       url:  "http://www.imdb.com/title/tt0133093/"

---




{% assign thumbnail="left" %}

{% for pub in page.pubs %}
{% if pub.image %}
{% include image.html url=pub.image caption="" height="80px" align=thumbnail %}
{% endif %}
[**{{pub.title}}**]({% if pub.internal %}{{pub.url | prepend: site.baseurl}}{% else %}{{pub.url}}{% endif %})<br />
{{pub.author}}<br />
*{{pub.journal}}*
{% if pub.note %} *({{pub.note}})*
{% endif %} *{{pub.year}}* {% if pub.doi %}[[doi]({{pub.doi}})]{% endif %}
{% if pub.media %}<br />Media: {% for article in pub.media %}[[{{article.name}}]({{article.url}})]{% endfor %}{% endif %}

{% endfor %}
