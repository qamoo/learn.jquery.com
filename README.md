# The jQuery Learning Site

This site aims to be an authoritative educational resource for those wishing to learn how to use jQuery. From beginners, to more advanced users. It's being driven by the jQuery community.
이 사이트는 jQuery를 사용하는 방법을 배우고자 하는 사람들을 위한 권위있는 교육 자료로 목표를 하고 있습니다. 초보자부터 더 고급 사용자까지를 대상으로 하며, jQuery 커뮤니티가 주도하고 있습니다.

## About

The goal of this site is twofold:

1. To serve as a central, trustworthy, narrative compendium of information about how to use jQuery and JavaScript.
2. To remain a timely, vibrant, and community-driven reference with a relatively low barrier to contribution.

Much of the initial content - and spirit - comes from [jQuery Fundamentals](http://jqfundamentals.com/legacy), an open-source book about jQuery, originally written by [Rebecca Murphey](http://www.rmurphey.com/) and released in 2010. In 2011, Rebecca [bequeathed the book](http://rmurphey.com/blog/2011/03/17/the-future-of-jquery-fundamentals-and-a-confession/) unto the jQuery Foundation to serve as the basis for this site. The book was split up into individual sections, whch we iterated on and improved over several months. Early on we wanted to ensure we covered as many relevant topics as possible and reached out to writers in the community to give us permission to integrate some of their blog posts as well.


## How This Site Works

This site's core content consists of [Markdown](http://daringfireball.net/projects/markdown/) files. The template that controls the site's appearance is a [child theme](https://github.com/jquery/jquery-wp-content/tree/master/themes/learn.jquery.com) of [jquery-wp-content](https://github.com/jquery/jquery-wp-content), and any issues with the presentation should be directed to [that repository](https://github.com/jquery/jquery-wp-content).


### Site Organization

All of the content lives inside of the subdirectories of the `page` directory. Each of these subdirectories is considered a **chapter**, and contains one or more **articles**, and there is also a top level file that corresponds to each chapter, which contains the chapter's human-readable title and an overview, which will appear on the chapter's landing page.

The [`order.json`](https://github.com/jquery/learn.jquery.com/blob/master/order.json) file controls the order that chapters and articles appear in the site.


### Front Matter

Each of the articles on the site has some JSON "Front Matter" that contains metadata. All articles should include the following:

* `title` - The title of the article as it will appear in the site.

`"title": "jQuery Event Extensions"`

* `level` - The approximate level of jQuery experience required to find the article useful. Options: `beginner`, `intermediate`, or `advanced`.

`"level": "advanced"`


## Building and Deploying

To build and deploy your changes for previewing in a [`jquery-wp-content`](https://github.com/jquery/jquery-wp-content) instance, follow the [workflow instructions](http://contribute.jquery.org/web-sites/#workflow) from our documentation on [contributing to jQuery Foundation web sites](http://contribute.jquery.org/web-sites/).


## How Can I Help?

We encourage contribution from anyone. For more comprehensive documentation on how to get involved, please read our [contributing guide](http://learn.jquery.com/contributing).
