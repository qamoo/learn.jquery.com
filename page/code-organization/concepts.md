<script>{
	"title": "Code Organization Concepts",
	"level": "beginner",
	"source": "http://jqfundamentals.com/legacy",
	"attribution": [ "jQuery Fundamentals" ]
}</script>

When you move beyond adding simple enhancements to your website with jQuery and start developing full-blown client-side applications, you need to consider how to organize your code. In this chapter, we'll take a look at various code organization patterns you can use in your jQuery application and explore the [RequireJS](http://requirejs.org/) dependency management and build system.

jQuery를 사용하여 웹사이트에 간단한 개선 사항을 추가하는 것을 넘어서면서 완전한 클라이언트 측 애플리케이션을 개발할 때 코드를 구성하는 방법을 고려해야 합니다. 이 장에서는 jQuery 애플리케이션에서 사용할 수 있는 다양한 코드 구성 패턴을 살펴보고 [RequireJS](http://requirejs.org/) 종속성 관리 및 빌드 시스템을 탐구해 보겠습니다.

## Key Concepts

Before we jump into code organization patterns, it's important to understand some concepts that are common to all good code organization patterns.

코드 구성 패턴으로 넘어가기 전에, 모든 좋은 코드 구성 패턴에 공통적으로 존재하는 몇 가지 개념을 이해하는 것이 중요합니다.

* Your code should be divided into units of functionality — modules, services, etc. Avoid the temptation to have all of your code in one huge `$( document ).ready()` block. This concept, loosely, is known as encapsulation.
* 코드는 기능 단위로 분할되어야 합니다. 모듈, 서비스 등으로 나뉘어져야 합니다. 모든 코드를 하나의 거대한 `$( document ).ready()` 블록 안에 두는 유혹을 피해야 합니다. 이 개념은 대략적으로 캡슐화로 알려져 있습니다.
* Don't repeat yourself. Identify similarities among pieces of functionality, and use inheritance techniques to avoid repetitive code.
* * 반복하지 마세요. 기능들 사이의 유사점을 파악하고 반복적인 코드를 피하기 위해 상속 기법을 사용하세요.
* Despite jQuery's DOM-centric nature, JavaScript applications are not all about the DOM. Remember that not all pieces of functionality need to — or should — have a DOM representation.
* jQuery는 DOM 중심적인 성격을 가지고 있지만, JavaScript 애플리케이션은 모두 DOM에 관한 것은 아닙니다. 모든 기능 단위가 DOM 표현을 가져야 하는 것은 아니며, 실제로 그렇게 해야 하는 경우도 아닙니다.
* Units of functionality should be [loosely coupled](http://en.wikipedia.org/wiki/Loose_coupling), that is, a unit of functionality should be able to exist on its own, and communication between units should be handled via a messaging system such as custom events or pub/sub. Stay away from direct communication between units of functionality whenever possible.
* 기능 단위는 [느슨하게 결합]되어야 합니다. 즉, 기능 단위는 독립적으로 존재할 수 있어야 하며, 기능 단위 간의 통신은 사용자 지정 이벤트나 pub/sub와 같은 메시징 시스템을 통해 처리되어야 합니다. 가능한 경우 기능 단위 간의 직접적인 통신을 피하십시오.

The concept of loose coupling can be especially troublesome to developers making their first foray into complex applications, so be mindful of this as you're getting started.

처음 복잡한 애플리케이션을 다루는 개발자들에게는 느슨한 결합의 개념이 특히 문제가 될 수 있으므로, 시작할 때 이에 유의하세요.

## Encapsulation 캡슐화

The first step to code organization is separating pieces of your application into distinct pieces; sometimes, even just this effort is sufficient to improve the structure of your code and its maintainability.

코드 구조화의 첫 번째 단계는 애플리케이션의 각 부분을 구별 가능한 단위로 분리하는 것입니다. 때로는 이 노력만으로도 코드의 구조와 유지 관리성을 개선하는 데 충분할 수 있습니다.

### The Object Literal

An object literal is perhaps the simplest way to encapsulate related code. It doesn't offer any privacy for properties or methods, but it's useful for eliminating anonymous functions from your code, centralizing configuration options, and easing the path to reuse and refactoring.

객체 리터럴은 관련된 코드를 캡슐화하는 가장 간단한 방법일 수 있습니다. 이는 속성이나 메서드에 대한 개인 정보를 제공하지 않지만, 코드에서 익명 함수를 제거하고 구성 옵션을 집중화하며, 재사용과 리팩터링을 쉽게할 수 있습니다.

```
// An object literal
var myFeature = {
	myProperty: "hello",

	myMethod: function() {
		console.log( myFeature.myProperty );
	},

	init: function( settings ) {
		myFeature.settings = settings;
	},

	readSettings: function() {
		console.log( myFeature.settings );
	}
};

myFeature.myProperty === "hello"; // true

myFeature.myMethod(); // "hello"

myFeature.init({
	foo: "bar"
});

myFeature.readSettings(); // { foo: "bar" }
```

The object literal above is simply an object assigned to a variable. The object has one property and several methods. All of the properties and methods are public, so any part of your application can see the properties and call methods on the object. While there is an init method, there's nothing requiring that it be called before the object is functional.

위의 객체 리터럴은 단순히 변수에 할당된 객체입니다. 이 객체에는 한 개의 프로퍼티와 여러 개의 메서드가 있습니다. 모든 프로퍼티와 메서드는 공개되어 있으므로 응용 프로그램의 어떤 부분에서든 프로퍼티를 볼 수 있고 객체의 메서드를 호출할 수 있습니다. 초기화 메서드가 있지만, 해당 메서드를 호출하지 않아도 객체가 동작할 수 있도록 하는 것을 요구하는 것은 없습니다.

How would we apply this pattern to jQuery code? Let's say that we had this code written in the traditional jQuery style:

jQuery 코드에 이 패턴을 적용하려면 다음과 같이 할 수 있습니다. 예를 들어, 전통적인 jQuery 스타일로 작성된 다음 코드가 있다고 가정해봅시다:

```
// Clicking on a list item loads some content using the
// list item's ID, and hides content in sibling list items
// 목록 항목을 클릭하면 해당 항목의 ID를 사용하여 내용을 로드하고,
// 형제 목록 항목의 내용을 숨깁니다.
$( document ).ready(function() {
	$( "#myFeature li" ).append( "<div>" ).click(function() {
		var item = $( this );
		var div = item.find( "div" );
		div.load( "foo.php?item=" + item.attr( "id" ), function() {
			div.show();
			item.siblings().find( "div" ).hide();
		});
	});
});
```

If this were the extent of our application, leaving it as-is would be fine. On the other hand, if this was a piece of a larger application, we'd do well to keep this functionality separate from unrelated functionality. We might also want to move the URL out of the code and into a configuration area. Finally, we might want to break up the chain to make it easier to modify pieces of the functionality later.

이것이 응용 프로그램의 전부라면 그대로 두는 것이 괜찮을 것입니다. 그러나 이것이 더 큰 응용 프로그램의 일부인 경우, 이 기능을 관련 없는 기능과 분리하는 것이 좋습니다. 또한 URL을 코드 밖으로 이동하여 구성 영역으로 만들 수도 있습니다. 마지막으로 기능의 일부를 나중에 수정하기 쉽도록 체인을 분해하는 것이 좋을 수 있습니다.

```
// Using an object literal for a jQuery feature
// jQuery 기능에 대한 객체 리터럴 사용
var myFeature = {
	init: function( settings ) {
		myFeature.config = {
			items: $( "#myFeature li" ),
			container: $( "<div class='container'></div>" ),
			urlBase: "/foo.php?item="
		};

		// Allow overriding the default config
		// 기본 구성을 재정의할 수 있도록 함
		$.extend( myFeature.config, settings );

		myFeature.setup();
	},

	setup: function() {
		myFeature.config.items
			.each( myFeature.createContainer )
			.click( myFeature.showItem );
	},

	createContainer: function() {
		var item = $( this );
		var container = myFeature.config.container
			.clone()
			.appendTo( item );
		item.data( "container", container );
	},

	buildUrl: function() {
		return myFeature.config.urlBase + myFeature.currentItem.attr( "id" );
	},

	showItem: function() {
		myFeature.currentItem = $( this );
		myFeature.getContent( myFeature.showContent );
	},

	getContent: function( callback ) {
		var url = myFeature.buildUrl();
		myFeature.currentItem.data( "container" ).load( url, callback );
	},

	showContent: function() {
		myFeature.currentItem.data( "container" ).show();
		myFeature.hideContent();
	},

	hideContent: function() {
		myFeature.currentItem.siblings().each(function() {
			$( this ).data( "container" ).hide();
		});
	}
};

$( document ).ready( myFeature.init );
```

The first thing you'll notice is that this approach is obviously far longer than the original — again, if this were the extent of our application, using an object literal would likely be overkill. Assuming it's not the extent of our application, though, we've gained several things:

가장 먼저 이 접근 방식이 원래 코드보다 분명히 길다는 것을 알 수 있습니다. 다시 말해서, 이것이 응용 프로그램의 전부라면 객체 리터럴을 사용하는 것은 과도할 수 있습니다. 그러나 응용 프로그램의 전부가 아닌 경우에는 여러 가지 이점을 얻게 됩니다.

* We've broken our feature up into tiny methods. In the future, if we want to change how content is shown, it's clear where to change it. In the original code, this step is much harder to locate.*
* 우리는 기능을 작은 메서드로 분리했습니다. 나중에 내용을 표시하는 방법을 변경하려면 어디를 수정해야 할지 명확합니다. 원본 코드에서는 이 단계를 찾기가 훨씬 어렵습니다.
* We've eliminated the use of anonymous functions.
* 익명 함수의 사용을 없앴습니다.
* We've moved configuration options out of the body of the code and put them in a central location.
* 우리는 설정 옵션을 코드 본문에서 분리하여 중앙 위치에 배치했습니다.
* We've eliminated the constraints of the chain, making the code easier to refactor, remix, and rearrange.
* 우리는 체인의 제약을 제거하여 코드를 리팩토링, 재구성 및 재배치하기 쉽게 만들었습니다.

For non-trivial features, object literals are a clear improvement over a long stretch of code stuffed in a `$( document ).ready()` block, as they get us thinking about the pieces of our functionality. However, they aren't a whole lot more advanced than simply having a bunch of function declarations inside of that `$( document ).ready()` block.

비단순한 기능에 대해서는 객체 리터럴은 기능을 하나의 `$( document ).ready()` 블록에 몰아 넣는 것보다 명확한 개선입니다. 왜냐하면 이를 통해 기능의 부분들을 고려하게 되기 때문입니다. 그러나 이것은 단순히 `$( document ).ready()` 블록 내에 함수 선언을 두는 것보다는 그렇게 많이 발전한 것은 아닙니다.

### The Module Pattern 모듈 패턴

The module pattern overcomes some of the limitations of the object literal, offering privacy for variables and functions while exposing a public API if desired.

모듈 패턴은 객체 리터럴의 일부 제약을 극복하며, 필요에 따라 변수와 함수에 대한 개인 정보를 제공하면서 공개 API를 노출합니다.
```
// The module pattern
var feature = (function() {

	// Private variables and functions
	var privateThing = "secret";
	var publicThing = "not secret";

	var changePrivateThing = function() {
		privateThing = "super secret";
	};

	var sayPrivateThing = function() {
		console.log( privateThing );
		changePrivateThing();
	};

	// Public API
	return {
		publicThing: publicThing,
		sayPrivateThing: sayPrivateThing
	};
})();

feature.publicThing; // "not secret"

// Logs "secret" and changes the value of privateThing
feature.sayPrivateThing();
```

In the example above, we self-execute an anonymous function that returns an object. Inside of the function, we define some variables. Because the variables are defined inside of the function, we don't have access to them outside of the function unless we put them in the return object. This means that no code outside of the function has access to the `privateThing` variable or to the `changePrivateThing` function. However, `sayPrivateThing` does have access to `privateThing` and `changePrivateThing`, because both were defined in the same scope as `sayPrivateThing`.

위의 예에서 익명 함수를 자체 실행하여 객체를 반환합니다. 함수 내부에서 몇 가지 변수를 정의합니다. 이러한 변수들은 함수 내에서 정의되었으므로, 함수 외부에서는 해당 변수에 액세스할 수 없습니다. 이 변수들을 반환 객체에 넣지 않는 한. 이는 함수 외부의 코드가 `privateThing` 변수나 `changePrivateThing` 함수에 액세스할 수 없음을 의미합니다. 그러나 `sayPrivateThing` 함수는 `privateThing` 및 `changePrivateThing`에 액세스할 수 있습니다. 왜냐하면 둘 다 `sayPrivateThing`와 동일한 스코프에서 정의되었기 때문입니다.

This pattern is powerful because, as you can gather from the variable names, it can give you private variables and functions while exposing a limited API consisting of the returned object's properties and methods.

이 패턴은 강력합니다. 변수 이름에서 알 수 있듯이, 이 패턴은 반환된 객체의 속성과 메서드로 구성된 제한된 API를 노출함으로써 개인 변수와 함수를 제공할 수 있습니다.

Below is a revised version of the previous example, showing how we could create the same feature using the module pattern while only exposing one public method of the module, `showItemByIndex()`.

이전 예제의 수정된 버전은 모듈 패턴을 사용하여 동일한 기능을 만들 수 있는 방법을 보여줍니다. 모듈의 단일 공개 메서드인 `showItemByIndex()`만 노출됩니다.

```
// Using the module pattern for a jQuery feature
$( document ).ready(function() {
	var feature = (function() {
		var items = $( "#myFeature li" );
		var container = $( "<div class='container'></div>" );
		var currentItem = null;
		var urlBase = "/foo.php?item=";

		var createContainer = function() {
			var item = $( this );
			var _container = container.clone().appendTo( item );
			item.data( "container", _container );
		};

		var buildUrl = function() {
			return urlBase + currentItem.attr( "id" );
		};

		var showItem = function() {
			currentItem = $( this );
			getContent( showContent );
		};

		var showItemByIndex = function( idx ) {
			$.proxy( showItem, items.get( idx ) )();
		};

		var getContent = function( callback ) {
			currentItem.data( "container" ).load( buildUrl(), callback );
		};

		var showContent = function() {
			currentItem.data( "container" ).show();
			hideContent();
		};

		var hideContent = function() {
			currentItem.siblings().each(function() {
				$( this ).data( "container" ).hide();
			});
		};

		items.each( createContainer ).click( showItem );

		return {
			showItemByIndex: showItemByIndex
		};
	})();

	feature.showItemByIndex( 0 );
});
```
