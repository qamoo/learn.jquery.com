<script>{
	"title": "Ajax",
	"level": "beginner",
	"customFields": [
		{
			"key": "icon",
			"value": "refresh"
		}
	]
}</script>

Traditionally webpages required reloading to update their content. For web-based email this meant that users had to manually reload their inbox to check and see if they had new mail. This had huge drawbacks: it was slow and it required user input. When the user reloaded their inbox, the server had to reconstruct the entire web page and resend all of the HTML, CSS, JavaScript, as well as the user's email. This was hugely inefficient. Ideally, the server should only have to send the user's new messages, not the entire page. By 2003, all the major browsers solved this issue by adopting the XMLHttpRequest (XHR) object, allowing browsers to communicate with the server without requiring a page reload.

전통적으로 웹 페이지는 콘텐츠를 업데이트하려면 다시 로드해야 했습니다. 웹 기반 이메일의 경우 사용자는 새로운 메일을 확인하려면 수동으로 받은 편지함을 다시 로드해야 했습니다. 이에는 큰 단점이 있었습니다: 속도가 느리고 사용자 입력이 필요했습니다. 사용자가 받은 편지함을 다시 로드하면 서버가 전체 웹 페이지를 재구성하고 모든 HTML, CSS, JavaScript 및 사용자의 이메일을 다시 전송해야 했습니다. 이는 매우 비효율적이었습니다. 이상적으로는 서버가 사용자의 새 메시지만 보내야 합니다. 2003년까지 모든 주요 브라우저는 XMLHttpRequest (XHR) 객체를 채택하여 페이지를 다시 로드하지 않고도 브라우저가 서버와 통신할 수 있도록 이 문제를 해결했습니다.

The XMLHttpRequest object is part of a technology called Ajax (Asynchronous JavaScript and XML). Using Ajax, data could then be passed between the browser and the server, using the XMLHttpRequest API, without having to reload the web page. With the widespread adoption of the XMLHttpRequest object it quickly became possible to build web applications like Google Maps, and Gmail that used XMLHttpRequest to get new map tiles, or new email without having to reload the entire page.

XMLHttpRequest 객체는 Ajax(비동기 JavaScript와 XML)라는 기술의 일부입니다. Ajax를 사용하면 XMLHttpRequest API를 사용하여 웹 페이지를 다시 로드하지 않고도 브라우저와 서버 간에 데이터를 전송할 수 있습니다. XMLHttpRequest 객체의 널리 사용으로 Google 지도 및 Gmail과 같은 웹 애플리케이션을 만드는 것이 가능해졌습니다. 이러한 애플리케이션은 전체 페이지를 다시 로드하지 않고도 새 지도 타일이나 새 이메일을 가져오기 위해 XMLHttpRequest를 사용합니다.

Ajax requests are triggered by JavaScript code; your code sends a request to a URL, and when it receives a response, a callback function can be triggered to handle the response. Because the request is asynchronous, the rest of your code continues to execute while the request is being processed, so it's imperative that a callback be used to handle the response.

Ajax 요청은 JavaScript 코드에 의해 트리거됩니다. 코드가 URL로 요청을 보내고 응답을 받으면 콜백 함수가 트리거되어 응답을 처리할 수 있습니다. 요청이 비동기적이기 때문에 요청이 처리되는 동안 나머지 코드가 계속 실행되므로 응답을 처리하기 위해 콜백을 사용하는 것이 중요합니다.

Unfortunately, different browsers implement the Ajax API differently. Typically this meant that developers would have to account for all the different browsers to ensure that Ajax would work universally. Fortunately, jQuery provides Ajax support that abstracts away painful browser differences. It offers both a full-featured `$.ajax()` method, and simple convenience methods such as `$.get()`, `$.getScript()`, `$.getJSON()`, `$.post()`, and `$().load()`.

불행하게도, 각각의 브라우저는 Ajax API를 다르게 구현합니다. 일반적으로 이것은 개발자들이 모든 다른 브라우저를 고려하여 Ajax가 모든 곳에서 작동하도록 보장해야 한다는 것을 의미합니다. 다행히도, jQuery는 고통스러운 브라우저 간의 차이점을 추상화하여 Ajax 지원을 제공합니다. jQuery는 `$.ajax()`와 같은 다양한 기능을 갖춘 메서드뿐만 아니라 `$.get()`, `$.getScript()`, `$.getJSON()`, `$.post()`, `$().load()`와 같은 간편한 편의 메서드도 제공합니다.

Most jQuery applications don't in fact use XML, despite the name "Ajax"; instead, they transport data as plain HTML or JSON (JavaScript Object Notation).

사실, "Ajax"라는 이름에도 불구하고 대부분의 jQuery 애플리케이션은 XML을 사용하지 않습니다. 대신, 일반 HTML이나 JSON(JavaScript Object Notation) 형식으로 데이터를 전송합니다.

In general, Ajax does not work across domains. For instance, a webpage loaded from example1.com is unable to make an Ajax request to example2.com as it would violate the same origin policy. As a work around, JSONP (JSON with Padding) uses `<script>` tags to load files containing arbitrary JavaScript content and JSON, from another domain. More recently browsers have implemented a technology called Cross-Origin Resource Sharing (CORS), that allows Ajax requests to different domains.

일반적으로, Ajax는 도메인 간에 작동하지 않습니다. 예를 들어, example1.com에서 로드된 웹페이지는 동일 출처 정책을 위반하므로 example2.com에 대한 Ajax 요청을 할 수 없습니다. 이를 해결하기 위해 JSONP (JSON with Padding)은 다른 도메인에서 임의의 JavaScript 콘텐츠와 JSON을 포함하는 파일을 `<script>` 태그를 사용하여 로드합니다. 최근 브라우저는 Cross-Origin Resource Sharing (CORS)라는 기술을 구현하여 서로 다른 도메인에 대한 Ajax 요청을 허용합니다.
