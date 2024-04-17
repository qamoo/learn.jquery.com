<script>{
	"title": "Finding & Evaluating Plugins",
	"level": "intermediate",
	"source": "http://jqfundamentals.com/legacy",
	"attribution": [ "jQuery Fundamentals" ]
}</script>

One of the most celebrated aspects of jQuery is its extensive plugin ecosystem. From table sorting to form validation to autocompletion – if there's a need for it, chances are good that someone has written a plugin for it.

jQuery에서 가장 칭찬받는 측면 중 하나는 다양한 플러그인 생태계입니다. 테이블 정렬부터 폼 유효성 검사, 자동 완성까지 - 필요한 것이 있다면 누군가가 해당 기능을 위한 플러그인을 작성한 가능성이 높습니다.

The quality of jQuery plugins varies widely. Many plugins are extensively tested and well-maintained, but others are hastily created and then ignored. More than a few fail to follow best practices. Some plugins, mainly [jQuery UI](http://jqueryui.com/), are maintained by the jQuery team. The quality of these plugins is as good as jQuery itself.

jQuery 플러그인의 품질은 매우 다양합니다. 많은 플러그인은 철저하게 테스트되고 잘 유지되지만, 다른 일부는 서둘러 작성된 뒤에는 무시됩니다. 몇몇은 최선의 방법을 따르지 않습니다. 일부 플러그인, 주로 [jQuery UI](http://jqueryui.com/)와 같은 것들은 jQuery 팀에 의해 유지됩니다. 이러한 플러그인의 품질은 jQuery 자체만큼 좋습니다.

The easiest way to find plugins is to search Google or the [jQuery Plugins Registry](http://plugins.jquery.com/). Once you've identified some options, you may want to consult the [jQuery forums](http://forum.jquery.com/) or the `#jquery` IRC channel to get input from others.

플러그인을 찾는 가장 쉬운 방법은 Google 또는 jQuery 플러그인 레지스트리를 검색하는 것입니다. 몇 가지 옵션을 식별한 후에는 jQuery 포럼이나 #jquery IRC 채널에서 다른 사람들의 의견을 듣는 것이 좋습니다.

When looking for a plugin to fill a need, do your homework. Ensure that the plugin is well-documented, and look for the author to provide lots of examples of its use. Be wary of plugins that do far more than you need; they can end up adding substantial overhead to your page. For more tips on spotting a sub-par plugin, read [Signs of a poorly written jQuery plugin](https://remysharp.com/2010/06/03/signs-of-a-poorly-written-jquery-plugin/) by Remy Sharp.

특정 필요를 충족시키기 위해 플러그인을 찾을 때 공들이세요. 플러그인이 잘 문서화되었는지 확인하고, 작성자가 해당 플러그인의 사용 예제를 많이 제공하는지 확인하세요. 필요 이상으로 많은 기능을 갖춘 플러그인에 대해 조심하세요. 이러한 플러그인은 페이지에 상당한 오버헤드를 추가할 수 있습니다. 저품질 플러그인을 발견하는 더 많은 팁을 원한다면 Remy Sharp의 [Signs of a poorly written jQuery plugin](https://remysharp.com/2010/06/03/signs-of-a-poorly-written-jquery-plugin/)을 참고하세요.

Once you choose a plugin, you'll need to add it to your page. Download the plugin, unzip it if necessary, place it within your application's directory structure, then include the plugin in your page using a script tag (after you include jQuery).

플러그인을 선택하면 페이지에 추가해야 합니다. 플러그인을 다운로드한 후 필요하다면 압축 해제하고, 응용 프로그램의 디렉토리 구조 내에 배치한 다음 스크립트 태그를 사용하여 페이지에 플러그인을 포함시킵니다 (jQuery를 포함한 후에 포함해야 합니다).
