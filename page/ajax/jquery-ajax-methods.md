<script>{
	"title": "jQuery's Ajax-Related Methods",
	"level": "beginner",
	"source": "http://jqfundamentals.com/legacy",
	"attribution": [ "jQuery Fundamentals" ]
}</script>

While jQuery does offer many Ajax-related convenience methods, the core `$.ajax()` method is at the heart of all of them, and understanding it is imperative. We'll review it first, and then touch briefly on the convenience methods.

jQuery는 많은 Ajax 관련 편의 메서드를 제공하지만, 핵심인 `$.ajax()` 메서드는 그 모든 것의 핵심입니다. 이를 이해하는 것이 매우 중요합니다. 먼저 이를 자세히 살펴보고, 간단히 편의 메서드에 대해 짚어보겠습니다.

It's often considered good practice to use the `$.ajax()` method over the jQuery provided [convenience methods](#convenience-methods). As you'll see, it offers features that the convenience methods do not, and its syntax allows for the ease of readability.

편의 메서드 대신 `$.ajax()` 메서드를 사용하는 것이 좋은 관행으로 여겨집니다. 보다시피 편의 메서드에는 없는 기능을 제공하며, 문법은 가독성을 향상시킵니다.

### `$.ajax()`

jQuery’s core `$.ajax()` method is a powerful and straightforward way of creating Ajax requests. It takes a configuration object that contains all the instructions jQuery requires to complete the request. The `$.ajax()` method is particularly valuable because it offers the ability to specify both success and failure callbacks. Also, its ability to take a configuration object that can be defined separately makes it easier to write reusable code. For complete documentation of the configuration options, visit [http://api.jquery.com/jQuery.ajax/](http://api.jquery.com/jQuery.ajax/).

jQuery의 핵심 `$.ajax()` 메서드는 Ajax 요청을 만드는 강력하고 직관적인 방법입니다. 이 메서드는 요청을 완료하기 위해 jQuery가 필요로 하는 모든 지시사항을 포함하는 구성 객체를 가져옵니다. `$.ajax()` 메서드는 성공 및 실패 콜백을 지정할 수 있는 능력 때문에 특히 유용합니다. 또한, 구성 객체를 따로 정의할 수 있는 능력은 재사용 가능한 코드를 작성하기 쉽게 만듭니다. 구성 옵션에 대한 완전한 문서는 [http://api.jquery.com/jQuery.ajax/](http://api.jquery.com/jQuery.ajax/) 를 참조하십시오.

```
// Using the core $.ajax() method
// 핵심 $.ajax() 메서드 사용
$.ajax({

	// The URL for the request
	// 요청을 위한 URL
	url: "post.php",

	// The data to send (will be converted to a query string)
	// 전송할 데이터 (쿼리 문자열로 변환될 것임)
	data: {
		id: 123
	},

	// Whether this is a POST or GET request
	// 이것이 POST인지 GET인지 여부
	type: "GET",

	// The type of data we expect back
	// 우리가 응답받기 기대하는 데이터의 유형
	dataType : "json",
})
  // Code to run if the request succeeds (is done);
  // 요청이 성공했을 때 실행할 코드(완료);
  // The response is passed to the function
  // 응답이 함수에 전달됩니다.
  .done(function( json ) {
     $( "<h1>" ).text( json.title ).appendTo( "body" );
     $( "<div class=\"content\">").html( json.html ).appendTo( "body" );
  })
  // Code to run if the request fails; the raw request and
  // status codes are passed to the function
  // 요청이 실패한 경우 실행할 코드; 원본 요청과 상태 코드가 함수에 전달됩니다.
  .fail(function( xhr, status, errorThrown ) {
    alert( "Sorry, there was a problem!" );
    console.log( "Error: " + errorThrown );
    console.log( "Status: " + status );
    console.dir( xhr );
  })
  // Code to run regardless of success or failure;
  // 성공 또는 실패 여부에 관계없이 실행할 코드;
  .always(function( xhr, status ) {
    alert( "The request is complete!" );
  });

```

**Note:** Regarding the `dataType` setting, if the server sends back data that is in a different format than you specify, your code may fail, and the reason will not always be clear, because the HTTP response code will not show an error. When working with Ajax requests, make sure your server is sending back the data type you're asking for, and verify that the `Content-type` header is accurate for the data type. For example, for JSON data, the `Content-type` header should be `application/json`.

**참고:** `dataType` 설정에 관련하여, 서버가 지정한 형식과 다른 형식의 데이터를 보내면 코드가 실패할 수 있으며, 그 이유가 항상 명확하지 않을 수 있습니다. 왜냐하면 HTTP 응답 코드에 오류가 표시되지 않을 수 있기 때문입니다. Ajax 요청을 처리할 때 서버가 요청한 데이터 유형을 보내는지 확인하고, `Content-type` 헤더가 데이터 유형에 대해 정확한지 확인하세요. 예를 들어, JSON 데이터의 경우 `Content-type` 헤더는 `application/json`이어야 합니다.

### `$.ajax()` Options

There are many, many options for the `$.ajax()` method, which is part of its power. For a complete list of options, visit [http://api.jquery.com/jQuery.ajax/](http://api.jquery.com/jQuery.ajax/); here are several that you will use frequently:

$.ajax() 메서드에는 많은 옵션이 있으며, 이것이 그것의 강력함의 일부입니다. 옵션의 완전한 목록은 http://api.jquery.com/jQuery.ajax/를 참조하십시오. 다음은 자주 사용하는 옵션 몇 가지입니다:

#### async

Set to `false` if the request should be sent synchronously. Defaults to `true`. Note that if you set this option to `false`, your request will block execution of other code until the response is received.

옵션을 `false`로 설정하면 요청이 동기적으로 전송되어야 함을 나타냅니다. 기본값은 `true`입니다. 이 옵션을 `false`로 설정하면 요청이 완료될 때까지 다른 코드의 실행이 차단됩니다. 주의하세요.

#### cache

Whether to use a cached response if available. Defaults to `true` for all `dataType`s except "script" and "jsonp". When set to `false`, the URL will simply have a cachebusting parameter appended to it.

응답이 캐시되어 있는 경우 캐시된 응답을 사용할지 여부를 나타냅니다. "script" 및 "jsonp"를 제외한 모든 `dataType`에 대해 기본값은 `true`입니다. `false`로 설정하면 URL에 캐시 버스트 파라미터가 추가됩니다.

#### done

A callback function to run if the request succeeds. The function receives the response data (converted to a JavaScript object if the `dataType` was JSON), as well as the text status of the request and the raw request object.

요청이 성공한 경우 실행할 콜백 함수입니다. 이 함수는 응답 데이터를 받고 (`dataType`이 JSON이었을 경우 JavaScript 객체로 변환됨), 요청의 텍스트 상태 및 원시 요청 객체도 받습니다.

#### fail

A callback function to run if the request results in an error. The function receives the raw request object and the text status of the request.

요청이 오류로 인해 실패한 경우 실행할 콜백 함수입니다. 이 함수는 원시 요청 객체와 요청의 텍스트 상태를 받습니다.

#### always 

A callback function to run when the request is complete, regardless of success or failure. The function receives the raw request object and the text status of the request.

요청이 성공 또는 실패 여부에 관계없이 완료된 후 실행할 콜백 함수입니다. 이 함수는 원시 요청 객체와 요청의 텍스트 상태를 받습니다.

#### context

The scope in which the callback function(s) should run (i.e. what `this` will mean inside the callback function(s)). By default, `this` inside the callback function(s) refers to the object originally passed to `$.ajax()`.

콜백 함수가 실행되는 범위(즉, 콜백 함수 내에서 `this`가 무엇을 의미하는지)입니다. 기본적으로 콜백 함수 내에서 `this`는 원래 `$.ajax()`에 전달된 객체를 가리킵니다.

#### data

The data to be sent to the server. This can either be an object or a query string, such as   
서버로 보낼 데이터입니다. 이는 객체 또는 쿼리 문자열일 수 있습니다.
`foo=bar&amp;baz=bim`.

#### dataType

The type of data you expect back from the server. By default, jQuery will look at the MIME type of the response if no `dataType` is specified.

서버에서 기대하는 데이터의 유형입니다. 기본적으로 `dataType`이 지정되지 않은 경우 jQuery는 응답의 MIME 유형을 확인합니다.

#### jsonp

The callback name to send in a query string when making a JSONP request. Defaults to "callback".   
JSONP 요청 시 쿼리 문자열에 보낼 콜백 이름입니다. 기본값은 "callback"입니다.

#### timeout

The time in milliseconds to wait before considering the request a failure.   
요청이 실패로 간주되기 전에 기다리는 시간(밀리초 단위)입니다.


#### traditional

Set to `true` to use the param serialization style in use prior to jQuery 1.4. For details, see [http://api.jquery.com/jQuery.param/](http://api.jquery.com/jQuery.param/).

jQuery 1.4 이전에 사용된 매개변수 직렬화 스타일을 사용하려면 `true`로 설정하세요. 자세한 내용은 [http://api.jquery.com/jQuery.param/](http://api.jquery.com/jQuery.param/) 를 참조하세요.

#### type

The type of the request, "POST" or "GET". Defaults to "GET". Other request types, such as "PUT" and "DELETE" can be used, but they may not be supported by all browsers.

요청의 유형, "POST" 또는 "GET"입니다. 기본값은 "GET"입니다. "PUT" 및 "DELETE"와 같은 다른 요청 유형을 사용할 수도 있지만, 모든 브라우저에서 지원되지 않을 수 있습니다.

#### url

The URL for the request.   
요청을 보낼 URL입니다.

The `url` option is the only required property of the `$.ajax()` configuration object; all other properties are optional. This can also be passed as the first argument to `$.ajax()`, and the options object as the second argument.

`url` 옵션은 `$.ajax()` 구성 객체의 유일한 필수 속성입니다. 다른 모든 속성은 선택 사항입니다. 이것은 또한 `$.ajax()`의 첫 번째 인수로 전달될 수 있으며, 옵션 객체는 두 번째 인수로 전달될 수 있습니다.

### Convenience Methods

If you don't need the extensive configurability of `$.ajax()`, and you don't care about handling errors, the Ajax convenience functions provided by jQuery can be useful, terse ways to accomplish Ajax requests. These methods are just "wrappers" around the core `$.ajax()` method, and simply pre-set some of the options on the `$.ajax()` method.

`$.ajax()`의 폭넓은 구성 가능성이 필요하지 않고 오류 처리에 관심이 없다면, jQuery에서 제공하는 Ajax 편의 함수들은 Ajax 요청을 수행하는 간단하고 간결한 방법으로 유용할 수 있습니다. 이러한 메서드들은 핵심 `$.ajax()` 메서드 주위의 "래퍼"일 뿐이며, 단순히 `$.ajax()` 메서드의 일부 옵션을 미리 설정합니다.

The convenience methods provided by jQuery are:   
jQuery에서 제공하는 편의 메서드는 다음과 같습니다:

#### $.get

Perform a GET request to the provided URL.   
제공된 URL로 GET 요청을 수행합니다.

#### $.post

Perform a POST request to the provided URL.   
제공된 URL로 POST 요청을 수행합니다.

#### $.getScript

Add a script to the page.   
페이지에 스크립트를 추가합니다.

#### $.getJSON

Perform a GET request, and expect JSON to be returned.   
GET 요청을 수행하고, JSON이 반환될 것으로 예상합니다.

In each case, the methods take the following arguments, in order:   
각 경우에 메서드는 순서대로 다음과 같은 인수를 받습니다:

#### url

The URL for the request. Required.   
요청을 위한 URL입니다. 필수 항목입니다.

#### data

The data to be sent to the server. Optional. This can either be an object or a query string, such as   
서버로 전송할 데이터입니다. 선택 사항입니다. 이는 객체 또는 쿼리 문자열일 수 있습니다.   
`foo=bar&amp;baz=bim`.

**Note:** This option is not valid for `$.getScript`.   
**참고:** 이 옵션은 `$.getScript`에 대해 유효하지 않습니다.

#### success callback

A callback function to run if the request succeeds. Optional. The function receives the response data (converted to a JavaScript object if the data type was JSON), as well as the text status of the request and the raw request object.

요청이 성공한 경우 실행할 콜백 함수입니다. 선택 사항입니다. 이 함수는 응답 데이터를 받으며 (`dataType`이 JSON이었을 경우 JavaScript 객체로 변환됨), 요청의 텍스트 상태와 원시 요청 객체도 받습니다.

#### data type

The type of data you expect back from the server. Optional.   
서버에서 예상되는 데이터 유형입니다. 선택 사항입니다.

**Note:** This option is only applicable for methods that don't already specify the data type in their name.
**참고:** 이 옵션은 이미 이름에 데이터 유형을 지정하지 않는 메서드에만 적용됩니다.

```
// Using jQuery's Ajax convenience methods
// jQuery의 Ajax 편의 메서드 사용

// Get plain text or HTML
// 일반 텍스트 또는 HTML 가져오기
$.get( "/users.php", {
	userId: 1234
}, function( resp ) {
	console.log( resp ); // server response
});

// Add a script to the page, then run a function defined in it   
// 페이지에 스크립트 추가한 다음, 해당 스크립트에 정의된 함수 실행
$.getScript( "/static/js/myScript.js", function() {
	functionFromMyScript();
});

// Get JSON-formatted data from the server
$.getJSON( "/details.php", function( resp ) {

	// Log each key in the response data
	$.each( resp, function( key, value ) {
		console.log( key + " : " + value );
	});
});
```

### `$.fn.load`

The `.load()` method is unique among jQuery’s Ajax methods in that it is called on a selection. The `.load()` method fetches HTML from a URL, and uses the returned HTML to populate the selected element(s). In addition to providing a URL to the method, you can optionally provide a selector; jQuery will fetch only the matching content from the returned HTML.

```
// Using .load() to populate an element
$( "#newContent" ).load( "/foo.html" );
```

```
// Using .load() to populate an element based on a selector
$( "#newContent" ).load( "/foo.html #myDiv h1:first", function( html ) {
	alert( "Content updated!" );
});
```
