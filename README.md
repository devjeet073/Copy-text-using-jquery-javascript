# Copy-text-using-jquery-javascript

jQuery(document).ready(function($) {
	// If a copy clickable input is clicked
	// input value will be highlighted and copied to clipboard
	$('body').on('click', 'input.js-click-to-copy-input', function(e) {
		copy_input( this );
	});
	
	// If a button to copy an input is clicked
	// associated input value will be highlighted and copied to clipboard
	$('body').on('click', 'a.js-click-to-copy-link', function(e) {
		e.preventDefault();
		var copy_id = $(this).data('copy-id');
		copy_input( $('#'+copy_id) );

	});
	
	// If copy clickable text is clicked
	// all text in this element will be highlighted and copied to clipboard
	$('body').on('click', '.js-click-to-copy-text', function(e) {
		var range = document.createRange();
		var sel = window.getSelection();
		range.setStartBefore(this.firstChild);
		range.setEndAfter(this.lastChild);
		sel.removeAllRanges();
		sel.addRange(range);
		try {  
			var successful = document.execCommand('copy');  
		} catch(err) {  
			console.error('Unable to copy'); 
		} 		
	});
	
	// copy function
	function copy_input( $input ) {
		$input.focus();
		$input.select();
		try {  
			var successful = document.execCommand('copy');  
		} catch(err) {  
			console.error('Unable to copy'); 
		}		
	}	
});

// Plain JavaScript
// <textarea name="email-details" id="message-textarea" rows="15" style="width: 100%">
// <a href="#" class="button secondary" id="js-copy-message">Copy Message</a>
<script>
    var copy = document.getElementById('js-copy-message');
    copy.onclick = function() {
        var copyTextarea = document.querySelector('#message-textarea');
        copyTextarea.select();
        try {
            var successful = document.execCommand('copy');
            var msg = successful ? 'successful' : 'unsuccessful';
            console.log('Copying text command was ' + msg);
        } catch (err) {
            console.log('Oops, unable to copy');
        }        
        return false;
    };
</script>
