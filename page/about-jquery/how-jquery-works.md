<script>{
	"title": "How jQuery Works",
	"level": "beginner"
}</script>

### jQuery: The Basics

This is a basic tutorial, designed to help you get started using jQuery. If you don't have a test page setup yet, start by creating the following HTML page:  
이것은 jQuery를 사용하여 시작하는 데 도움이 되는 기본 튜토리얼입니다. 아직 테스트 페이지를 설정하지 않았다면, 다음과 같은 HTML 페이지를 만들기로 시작하세요:

```
<!doctype html>
<html>
<head>
	<meta charset="utf-8">
	<title>Demo</title>
</head>
<body>
	<a href="http://jquery.com/">jQuery</a>
	<script src="jquery.js"></script>
	<script>

	// Your code goes here.

	</script>
</body>
</html>
```

The `src` attribute in the `<script>` element must point to a copy of jQuery. Download a copy of jQuery from the [Downloading jQuery](http://jquery.com/download/) page and store the `jquery.js` file in the same directory as your HTML file.

`<script>` 요소의 `src` 속성은 jQuery의 사본을 가리켜야 합니다. [jQuery 다운로드 페이지](http://jquery.com/download/)에서 jQuery의 사본을 다운로드하여 `jquery.js` 파일을 HTML 파일과 동일한 디렉토리에 저장하십시오.

<div class="warning">

**Note**: When you download jQuery, the file name may contain a version number, e.g., `jquery-x.y.z.js`. Make sure to either rename this file to `jquery.js` or update the `src` attribute of the `<script>` element to match the file name.

참고: jQuery를 다운로드할 때 파일 이름에 버전 번호가 포함될 수 있습니다. 예를 들어, jquery-x.y.z.js와 같습니다. 이 파일을 jquery.js로 이름을 변경하거나 <script> 요소의 src 속성을 파일 이름과 일치하도록 업데이트해야 합니다.

</div>

### Launching Code on Document Ready 문서 준비 시 코드 실행

To ensure that their code runs after the browser finishes loading the document, many JavaScript programmers wrap their code in an `onload` function: 

브라우저가 문서 로딩을 완료한 후에 코드가 실행되도록 보장하기 위해 많은 JavaScript 프로그래머가 코드를 `onload` 함수로 감싸는 경우가 있습니다:

```
window.onload = function() {

	alert( "welcome" );

};
```

Unfortunately, the code doesn't run until all images are finished downloading, including banner ads. To run code as soon as the document is ready to be manipulated, jQuery has a statement known as the [ready event](http://api.jquery.com/ready/):

```

$( document ).ready(function() {

	// Your code here.

});
```

<div class="warning">

**Note**: The jQuery library exposes its methods and properties via two properties of the <code>window</code> object called <code>jQuery</code> and <code>$</code>. <code>$</code> is simply an alias for <code>jQuery</code> and it's often employed because it's shorter and faster to write.

</div>

For example, inside the `ready` event, you can add a click handler to the link:

```
$( document ).ready(function() {

	$( "a" ).click(function( event ) {

		alert( "Thanks for visiting!" );

	});

});
```

Copy the above jQuery code into your HTML file where it says `// Your code goes here`. Then, save your HTML file and reload the test page in your browser. Clicking the link should now first display an alert pop-up, then continue with the default behavior of navigating to http://jquery.com.

For `click` and most other [events](http://api.jquery.com/category/events/), you can prevent the default behavior by calling `event.preventDefault()` in the event handler:

```
$( document ).ready(function() {

	$( "a" ).click(function( event ) {

		alert( "As you can see, the link no longer took you to jquery.com" );

		event.preventDefault();

	});

});
```

Try replacing your first snippet of jQuery code, which you previously copied in to your HTML file, with the one above. Save the HTML file again and reload to try it out.

### Complete Example

The following example illustrates the click handling code discussed above, embedded directly in the HTML `<body>`. Note that in practice, it is usually better to place your code in a separate JS file and load it on the page with a `<script>` element's `src` attribute.

```
<!doctype html>
<html>
<head>
	<meta charset="utf-8">
	<title>Demo</title>
</head>
<body>
	<a href="http://jquery.com/">jQuery</a>
	<script src="jquery.js"></script>
	<script>

	$( document ).ready(function() {
		$( "a" ).click(function( event ) {
			alert( "The link will no longer take you to jquery.com" );
			event.preventDefault();
		});
	});

	</script>
</body>
</html>
```

### Adding and Removing an HTML Class

<div class="warning">

**Important:** You must place the remaining jQuery examples inside the `ready` event so that your code executes when the document is ready to be worked on.

</div>

Another common task is adding or removing a class.

First, add some style information into the `<head>` of the document, like this:

```
<style>
a.test {
	font-weight: bold;
}
</style>
```

Next, add the [.addClass()](http://api.jquery.com/addClass/) call to the script:

```
$( "a" ).addClass( "test" );
```

All `<a>` elements are now bold.

To remove an existing class, use [.removeClass()](http://api.jquery.com/removeClass/):

```
$( "a" ).removeClass( "test" );
```

### Special Effects

jQuery also provides some handy [effects](http://api.jquery.com/category/effects/) to help you make your web sites stand out. For example, if you create a click handler of:

```
$( "a" ).click(function( event ) {

	event.preventDefault();

	$( this ).hide( "slow" );

});
```

Then the link slowly disappears when clicked.

## Callbacks and Functions

Unlike many other programming languages, JavaScript enables you to freely pass functions around to be executed at a later time. A *callback* is a function that is passed as an argument to another function and is executed after its parent function has completed. Callbacks are special because they patiently wait to execute until their parent finishes. Meanwhile, the browser can be executing other functions or doing all sorts of other work.

To use callbacks, it is important to know how to pass them into their parent function.

### Callback *without* Arguments

If a callback has no arguments, you can pass it in like this:

```
$.get( "myhtmlpage.html", myCallBack );
```

When [$.get()](http://api.jquery.com/jQuery.get/) finishes getting the page `myhtmlpage.html`, it executes the `myCallBack()` function.

* **Note:** The second parameter here is simply the function name (but *not* as a string, and without parentheses).

### Callback *with* Arguments

Executing callbacks with arguments can be tricky.

#### Wrong

This code example will ***not*** work:

```
$.get( "myhtmlpage.html", myCallBack( param1, param2 ) );
```

The reason this fails is that the code executes `myCallBack( param1, param2 )` immediately and then passes `myCallBack()`'s *return value* as the second parameter to `$.get()`. We actually want to pass the function `myCallBack()`, not `myCallBack( param1, param2 )`'s return value (which might or might not be a function). So, how to pass in `myCallBack()` *and* include its arguments?

#### Right

To defer executing `myCallBack()` with its parameters, you can use an anonymous function as a wrapper. Note the use of `function() {`. The anonymous function does exactly one thing: calls `myCallBack()`, with the values of `param1` and `param2`.

```
$.get( "myhtmlpage.html", function() {

	myCallBack( param1, param2 );

});
```

When `$.get()` finishes getting the page `myhtmlpage.html`, it executes the anonymous function, which executes `myCallBack( param1, param2 )`.
