<script>{
	"title": "Key Concepts",
	"level": "beginner",
	"source": "http://jqfundamentals.com/legacy",
	"attribution": [ "jQuery Fundamentals" ]
}</script>

Proper use of Ajax-related jQuery methods requires understanding some key concepts first.   
Ajax 관련 jQuery 메서드를 올바르게 사용하기 위해서는 먼저 몇 가지 핵심 개념을 이해해야 합니다.  

### GET vs. POST

The two most common "methods" for sending a request to a server are GET and POST. It's important to understand the proper application of each.

서버로 요청을 보내는 가장 일반적인 두 가지 "메서드"는 GET과 POST입니다. 각각의 올바른 적용을 이해하는 것이 중요합니다.

The GET method should be used for non-destructive operations — that is, operations where you are only "getting" data from the server, not changing data on the server. For example, a query to a search service might be a GET request. GET requests may be cached by the browser, which can lead to unpredictable behavior if you are not expecting it. GET requests generally send all of their data in a query string.

GET 메서드는 비파괴적 작업에 사용되어야 합니다. 즉, 서버의 데이터를 변경하지 않고 단순히 데이터를 "가져오는" 작업에 사용됩니다. 예를 들어, 검색 서비스에 대한 쿼리는 GET 요청일 수 있습니다. GET 요청은 브라우저에 의해 캐시될 수 있으며, 이는 예상하지 않은 동작을 유발할 수 있습니다. GET 요청은 일반적으로 쿼리 문자열에 모든 데이터를 보냅니다.

The POST method should be used for destructive operations — that is, operations where you are changing data on the server. For example, a user saving a blog post should be a POST request. POST requests are generally not cached by the browser; a query string can be part of the URL, but the data tends to be sent separately as post data.

POST 메서드는 파괴적 작업에 사용되어야 합니다. 즉, 서버의 데이터를 변경하는 작업에 사용됩니다. 예를 들어, 사용자가 블로그 글을 저장하는 경우 POST 요청이어야 합니다. POST 요청은 일반적으로 브라우저에 의해 캐시되지 않습니다. 쿼리 문자열은 URL의 일부가 될 수 있지만, 데이터는 일반적으로 별도의 POST 데이터로 전송됩니다.

### Data Types

jQuery generally requires some instruction as to the type of data you expect to get back from an Ajax request; in some cases the data type is specified by the method name, and in other cases it is provided as part of a configuration object. There are several options:

jQuery에서 Ajax 요청으로부터 기대하는 데이터 유형에 대한 명시적인 지시가 필요합니다. 때로는 데이터 유형이 메서드 이름으로 지정되며, 다른 경우에는 구성 객체의 일부로 제공됩니다. 여러 옵션이 있습니다:

#### text

For transporting simple strings.   
단순 문자열을 전송하는 데 사용합니다.

#### html

For transporting blocks of HTML to be placed on the page.   
페이지에 배치될 HTML 블록을 전송하는 데 사용합니다.

#### script

For adding a new script to the page.   
페이지에 새 스크립트를 추가하는 데 사용됩니다.

#### json

For transporting JSON-formatted data, which can include strings, arrays, and objects.   
문자열, 배열, 그리고 객체를 포함할 수 있는 JSON 형식의 데이터를 전송하는 데 사용됩니다.

**Note:** As of jQuery 1.4, if the JSON data sent by your server isn't properly formatted, the request may fail silently. See [http://json.org](http://json.org) for details on properly formatting JSON, but as a general rule, use built-in language methods for generating JSON on the server to avoid syntax issues.

**참고:** jQuery 1.4부터 서버에서 전송한 JSON 데이터가 올바르게 형식화되지 않으면 요청이 조용히 실패할 수 있습니다. JSON의 올바른 형식에 대한 자세한 내용은 [http://json.org](http://json.org)를 참조하십시오. 그러나 일반적으로 서버에서 JSON을 생성할 때 내장된 언어 메서드를 사용하여 구문 오류를 피하십시오.

#### jsonp

For transporting JSON data from another domain.   
다른 도메인에서 JSON 데이터를 전송하기 위해 사용됩니다.

#### xml

For transporting data in a custom XML schema.   
사용자 정의 XML 스키마로 데이터를 전송하는 데 사용됩니다.

Consider using the JSON format in most cases, as it provides the most flexibility. It is especially useful for sending both HTML and data at the same time.   
대부분의 경우 JSON 형식을 사용하는 것이 가장 유연합니다. 특히 HTML과 데이터를 동시에 전송해야 할 때 유용합니다.

### A is for Asynchronous / A는 비동기(Asynchronous)를 나타냅니다.

The asynchronicity of Ajax catches many new jQuery users off guard. Because Ajax calls are asynchronous by default, the response is not immediately available. Responses can only be handled using a callback. So, for example, the following code will not work:

Ajax의 비동기성은 많은 새로운 jQuery 사용자들을 놀라게 합니다. Ajax 호출은 기본적으로 비동기적이기 때문에 응답이 즉시 사용할 수 없습니다. 응답은 콜백을 사용해서만 처리할 수 있습니다. 예를 들어, 다음 코드는 작동하지 않습니다:

```
var response;

$.get( "foo.php", function( r ) {
	response = r;
});

console.log( response ); // undefined
```

Instead, we need to pass a callback function to our request; this callback will run when the request succeeds, at which point we can access the data that it returned, if any.

대신, 요청에 콜백 함수를 전달해야 합니다. 이 콜백은 요청이 성공한 경우에 실행되며, 그때 반환된 데이터에 접근할 수 있습니다.
```
$.get( "foo.php", function( response ) {
	console.log( response ); // server response
});
```

### Same-Origin Policy and JSONP

In general, Ajax requests are limited to the same protocol (http or https), the same port, and the same domain as the page making the request. This limitation does not apply to scripts that are loaded via jQuery's Ajax methods. 

Note: Versions of Internet Explorer less than 10 do not support cross-domain AJAX requests. 

The other exception is requests targeted at a JSONP service on another domain. In the case of JSONP, the provider of the service has agreed to respond to your request with a script that can be loaded into the page using a `<script>` tag, thus avoiding the same-origin limitation; that script will include the data you requested, wrapped in a callback function you provide.

### Ajax and Firebug

Firebug (or the Webkit Inspector in Chrome or Safari) is an invaluable tool for working with Ajax requests. You can see Ajax requests as they happen in the Console tab of Firebug (and in the Resources > XHR panel of Webkit Inspector), and you can click on a request to expand it and see details such as the request headers, response headers, response content, and more. If something isn't going as expected with an Ajax request, this is the first place to look to track down what's wrong.
