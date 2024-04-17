<script>{
	"title": "Keep Things DRY",
	"level": "beginner",
	"source": "http://jqfundamentals.com/legacy",
	"attribution": [ "jQuery Fundamentals" ]
}</script>

Don't repeat yourself; if you're repeating yourself, you're doing it wrong.
자신을 반복하지 마세요. 반복하고 있다면 잘못하고 있습니다.

```
// BAD
if ( eventfade.data( "currently" ) !== "showing" ) {
	eventfade.stop();
}

if ( eventhover.data( "currently" ) !== "showing" ) {
	eventhover.stop();
}

if ( spans.data( "currently" ) !== "showing" ) {
	spans.stop();
}

// GOOD!!
var elems = [ eventfade, eventhover, spans ];

$.each( elems, function( i, elem ) {
	if ( elem.data( "currently" ) !== "showing" ) {
		elem.stop();
	}
});
```
