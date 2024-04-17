<script>{
	"title": "Beware Anonymous Functions",
	"level": "beginner",
	"source": "http://jqfundamentals.com/legacy",
	"attribution": [ "jQuery Fundamentals" ]
}</script>

Anonymous functions bound everywhere are a pain. They're difficult to debug, maintain, test, or reuse. Instead, use an object literal to organize and name your handlers and callbacks.

어디에나 바인딩된 익명 함수는 골칫거리입니다. 디버그, 유지 관리, 테스트 또는 재사용이 어렵습니다. 대신, 핸들러와 콜백을 구성하고 이름을 지정하기 위해 객체 리터럴을 사용하십시오.
```
// BAD
$( document ).ready(function() {

	$( "#magic" ).click(function( event ) {
		$( "#yayeffects" ).slideUp(function() {
			// ...
		});
	});

	$( "#happiness" ).load( url + " #unicorns", function() {
		// ...
	});

});

// BETTER
var PI = {

	onReady: function() {
		$( "#magic" ).click( PI.candyMtn );
		$( "#happiness" ).load( PI.url + " #unicorns", PI.unicornCb );
	},

	candyMtn: function( event ) {
		$( "#yayeffects" ).slideUp( PI.slideCb );
	},

	slideCb: function() { ... },

	unicornCb: function() { ... }

};

$( document ).ready( PI.onReady );
```
