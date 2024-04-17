<script>{
	"title": "Plugins",
	"level": "intermediate",
	"customFields": [
		{
			"key": "icon",
			"value": "bolt"
		}
	]
}</script>

A jQuery plugin is simply a new method that we use to extend jQuery's prototype object. By extending the prototype object you enable all jQuery objects to inherit any methods that you add. As established, whenever you call `jQuery()` you're creating a new jQuery object, with all of jQuery's methods inherited.

jQuery 플러그인은 간단히 말해 jQuery의 prototype 객체를 확장하는 새로운 방법입니다. 프로토타입 객체를 확장함으로써 추가한 메서드를 모든 jQuery 객체가 상속받을 수 있습니다. 앞에서 설명한 대로 `jQuery()`를 호출할 때마다 모든 jQuery 메서드가 상속된 새로운 jQuery 객체가 생성됩니다.

The idea of a plugin is to do something with a collection of elements. You could consider each method that comes with the jQuery core a plugin, like `.fadeOut()` or `.addClass()`.

플러그인의 아이디어는 요소 컬렉션을 처리하는 것입니다. jQuery 코어와 함께 제공되는 각 메서드를 플러그인으로 간주할 수 있습니다. `.fadeOut()`나 `.addClass()`와 같이요.

You can make your own plugins and use them privately in your code or you can release them into the wild. There are thousands of jQuery plugins available online. The barrier to creating a plugin of your own is so low that you'll want to do it straight away!

자신만의 플러그인을 만들어서 코드 내에서 비공개로 사용할 수도 있고, 공개할 수도 있습니다. 온라인에서 수천 개의 jQuery 플러그인이 제공됩니다. 자신의 플러그인을 만드는 장벽은 매우 낮기 때문에 즉시 시작하고 싶을 것입니다!
