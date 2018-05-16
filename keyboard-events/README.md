# Table of Contents  
[Chrome/Opera](#chromeopera)  
[IE11](#ie-11)  
[Firefox](#firefox)  
[Safari](#safari-7-emulation)  
[Observation](#observation)  

Results of testing kepress v/s keyup & keydown events across diffent browsers

## Chrome/Opera

### KeyPress

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                  |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------               |
|Up            |No 	       |          |             |       |        |		    |                                          |			
|a             |Yes	       |a         | U+0041      | 97    | 97     |97	   |                                          |			
|A             |Yes	       |A         | U+0041      | 65    | 65     |65	   |                                          |			
|;             |Yes	       |;         | U+003B      | 59    | 59     |59	   |                                          |			
|Shift+a       |Yes	       |A         | U+0041      | 65    | 65     |65	   |No Shift Event                            |			
|Shift+A       |Yes	       |a         | U+0041      | 97    | 97     |97	   |Why one, bug ?                            |			
|Ctrl+Shift+a  |Yes	       |          | U+0001      | 1     | 1      |1 	   |                                          |			
|Ctrl+Shift+b  |No	        |          |             |       |        |		    |Same: ctrl+shift +b/d/i/z                 |			
|Enter         |Yes	       |Enter     | Enter       | 13    | 13     |13	   |                                          |			
|Tab           |No 	       |          |             |       |        |		    |                                          |			
|Control       |No 	       |          |             |       |        |		    |                                          |			


### KeyDown

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                  |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------               |
|Up            |Yes	       |ArrowUp   | Up          | 38    | 0      |38 		|                                           |			
|a             |Yes	       |a         | U+0041      | 65    | 0      |65 		|                                           |			
|A             |Yes	       |A         | U+0041      | 65    | 0      |65 		|                                           |			
|;             |Yes	       |;         | U+00BA      | 186   | 0      |186		| Different from press.Same: ( ,  + etc     |			
|Shift+a       |Yes (2)    |Shift     | Shift       | 16    | 0      |16 		|                                           |			
|              |   	       |A         | U+0041      | 65    | 0      |65 		|                                           |			
|Shift+A       |Yes	(2)    |Shift     | Shift       | 16    | 0      |16 		|                                           |			
|              |   	       |a         | U+0041      | 65    | 0      |65 		|                                           |			
|Ctrl+Shift+a  |Yes (3)    |Control   | Control     | 17    | 0      |17 		|                                           |			
|              |  	        |Shift     | Shift       | 16    | 0      |16 		|                                           |			
|              |  	        |A         | U+0001      | 65    | 0      |65 		|                                           |			
|Enter         |Yes	       |Enter     | Enter       | 13    | 0      |13 		|                                           |			
|Tab           |Yes 	      |Tab       | U+0009      | 9     | 0      |9  		|                                           |			
|Control       |Yes	       |Control   | Control     | 17    | 0      |17 		|                                           |			
 
 
## IE 11
### KeyPress

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                  |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------               |
|Up            |No 	       |          |             |       |        |		    |                                          |			
|a             |Yes	       |a         | Undefined   | 97    | 97     |97	   |                                          |			
|A             |Yes	       |A         | Undefined   | 65    | 65     |65	   |                                          |			
|;             |Yes	       |;         | Undefined   | 59    | 59     |59	   |                                          |			
|Shift+a       |Yes	       |A         | Undefined   | 65    | 65     |65	   |No Shift Event                            |			
|Shift+A       |Yes	       |a         | Undefined   | 97    | 97     |97	   |                                          |			
|Ctrl+Shift+a  |Yes	       |a         | Undefined   | 1     | 1      |1 	   |                                          |			
|Enter         |Yes	       |Enter     | Undefined   | 13    | 13     |13	   |                                          |			
|Tab           |No 	       |          |             |       |        |		    |                                          |			
|Control       |No 	       |          |             |       |        |		    |                                          |			


### KeyDown

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                   |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------                |
|Up            |Yes	       |Up        | Undefined   | 38    | 0      |38 	  |Different from Chrome's ArrowUp            |			
|a             |Yes	       |a         | Undefined   | 65    | 0      |65 	  |                                           |			
|A             |Yes	       |A         | Undefined   | 65    | 0      |65 	  |                                           |			
|;             |Yes	       |;         | Undefined   | 186   | 0      |186	  | Different from press.Same: ( ,  + etc     |			
|Shift+a       |Yes (2)    |Shift     | Undefined   | 16    | 0      |16 	  |                                           |			
|              |   	       |A         | Undefined   | 65    | 0      |65 	  |                                           |			
|Shift+A       |Yes	(2)    |Shift     | Undefined   | 16    | 0      |16 	  |                                           |			
|              |   	       |a         | Undefined   | 65    | 0      |65 	  |                                           |			
|Ctrl+Shift+a  |Yes (3)    |Control   | Undefined   | 17    | 0      |17 	  |                                           |			
|              |  	        |Shift     | Undefined   | 16    | 0      |16 	  |                                           |			
|              |  	        |A         | Undefined   | 65    | 0      |65 	  |                                           |			
|Enter         |Yes	       |Enter     | Undefined   | 13    | 0      |13 	  |                                           |			
|Tab           |Yes 	      |Tab       | Undefined   | 9     | 0      |9  	  |                                           |			
|Control       |Yes	       |Control   | Undefined   | 17    | 0      |17 	  |                                           |			

# Firefox

### KeyPress

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                  |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------               |
|Up            |Yes	       |ArrowUp   | Undefined   | 38    | 0      |0	    |Event fired, Same: Insert, Home etc       |			
|a             |Yes	       |a         | Undefined   | 0     | 97     |97	   |                                          |			
|A             |Yes	       |A         | Undefined   | 0     | 65     |65	   |                                          |			
|;             |Yes	       |;         | Undefined   | 0     | 59     |59	   |                                          |			
|Shift+a       |Yes	       |A         | Undefined   | 0     | 65     |65	   |No Shift Event                            |			
|Shift+A       |Yes	       |a         | Undefined   | 0     | 97     |97	   |                                          |			
|Ctrl+Shift+a  |Yes	       |a         | Undefined   | 0     | 1      |1 	   |                                          |			
|Enter         |Yes	       |Enter     | Undefined   | 13    | 13     |13	   |                                          |			
|Tab           |Yes	       |Tab       | Undefined   | 9     | 0      |0     |Same: backspace, esc                      |			
|Control       |No 	       |          |             |       |        |		    |Same: special keys like shift,alt         |			


### KeyDown

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                   |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------                |
|Up            |Yes	       |ArrowUp   | Undefined   | 38    | 0      |38 	  |                                           |			
|a             |Yes	       |a         | Undefined   | 65    | 0      |65 	  |                                           |			
|A             |Yes	       |A         | Undefined   | 65    | 0      |65 	  |                                           |			
|;             |Yes	       |;         | Undefined   | 59    | 0      |59 	  | Same as keypress (unlike chrome).         |			
|Shift+a       |Yes (2)    |Shift     | Undefined   | 16    | 0      |16 	  |                                           |			
|              |   	       |A         | Undefined   | 65    | 0      |65 	  |                                           |			
|Shift+A       |Yes	(2)    |Shift     | Undefined   | 16    | 0      |16 	  |                                           |			
|              |   	       |a         | Undefined   | 65    | 0      |65 	  |                                           |			
|Ctrl+Shift+a  |Yes (3)    |Control   | Undefined   | 17    | 0      |17 	  |                                           |			
|              |  	        |Shift     | Undefined   | 16    | 0      |16 	  |                                           |			
|              |  	        |A         | Undefined   | 65    | 0      |65 	  |                                           |			
|Enter         |Yes	       |Enter     | Undefined   | 13    | 0      |13 	  |                                           |			
|Tab           |Yes 	      |Tab       | Undefined   | 9     | 0      |9  	  |                                           |			
|Control       |Yes	       |Control   | Undefined   | 17    | 0      |17 	  |                                           |		

## Safari 7 (Emulation)
NOTE : Due to emulation issues and older version, results may not be accurate and/or up to date

### KeyPress

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                  |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------               |
|Up            |No 	       |          |             |       |        |		    |                                          |			
|a             |Yes	       |Undefined | a           | 97    | 97     |97	   |                                          |			
|A             |Yes	       |Undefined | A           | 65    | 65     |65	   |                                          |			
|;             |Yes	       |Undefined |             | 59    | 59     |59	   |keyId is empty. Same for other non-print  |			
|Shift+a       |Yes	       |Undefined |             | 65    | 65     |65	   |                                          |			
|Ctrl+Shift+a  |Yes	       |Undefined |             | 97    | 97     |97	   |                                          |			
|Enter         |Yes	       |Undefined |             | 13    | 13     |13	   |                                          |			
|Tab           |No 	       |          |             |       |        |		    |                                          |			
|Control       |No 	       |          |             |       |        |		    |                                          |			


### KeyDown

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                   |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------                |
|Up            |Yes	       |Undefined | Up          | 38    | 0      |38  		|                                           |			
|a             |Yes	       |Undefined | U+0041      | 65    | 0      |65  		|                                           |			
|A             |Yes	       |Undefined | U+0041      | 65    | 0      |65  		|                                           |			
|;             |Yes	       |Undefined | U+003B      | 186   | 0      |186 		| Different from press.Same: ( ,  + etc     |			
|Shift+a       |Yes (2)    |Undefined | Shift       | 16    | 0      |16  		|                                           |			
|              |   	       |Undefined | U+0041      | 65    | 0      |65  		|                                           |			
|Ctrl+Shift+a  |Yes (3)    |Undefined | Control     | 17    | 0      |17  		| emulation issues - give control as meta   |			
|              |  	        |Undefined | Shift       | 16    | 0      |16  		|                                           |			
|              |  	        |Undefined | U+0001      | 65    | 0      |65  		|                                           |			
|Enter         |Yes	       |Undefined | Enter       | 13    | 0      |13  		|                                           |			
|Tab           |Yes 	      |Undefined | U+0009      | 9     | 0      |9   		|                                           |			
|Control       |Yes	       |Undefined | Control     | 17    | 0      |17  		|                                           |			
 

## Observation
Browser Usage links:-
* http://caniuse.com/#feat=keyboardevent-charcode
* http://caniuse.com/#feat=keyboardevent-code
* http://caniuse.com/#feat=keyboardevent-key
* https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/which#Browser_compatibility 
* https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/keyCode#Browser_compatibility 
* https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/charCode#Browser_compatibility 

Lots of differences across all browsers.

##### Key
*	is not supported in Safari and Mobile browsers
*	Some variables in key press are different across browser like FF (Scroll, Up) vs Chrome (ScrollLock, ArrowUp)


##### KeyPress 
*	is not supported on many mobile browsers
*	Is not fired on chrome/ie for non-printable characters, fire on firefox for all and not fired on safari for some characters like Alt, Shift, Control.


##### KeyDown/Keyup
*	Does not differentiate between small caps and large caps variable of an alphabet
*	Will always show the Capital variant of alphabets


##### KeyIdentifer
*	Is not supported on many browsers
*	Has issues on safari


##### which
*	Is supposed to be deprecated but seems to have good support
*	Consistent for keydown across browsers except in FF where the value for some characters like plus(+), semi-color(;) etc are different
*	Consistent  for printable characters across browsers for keypress, not reliable for non-printable characters (keypress event may not fire at all)


##### keyCode
*	Deprecated
*	Not supported in FF for keypress, otherwise mostly similiar
*	Pretty much same for all cases for KeyDown expect some values for cases in FF like plus(+), semi-color(;) etc are different
*	Dependent on keyboard layout


##### charCode
*	Deprecated/Non-standard (MDN)
*	Not supported at all for keydown
*	Similar for keypress for printable characters 

### Usage
*	For printable characters, best to use keypress events and listen to charCode or which
*	For listening to non-printable characters like Arrow etc best to use keydown/keyup on keyCode and which fields
*	For listening to special actions like “Control + P” use keydown/keyup and then match the values of ctrlKey, altKey, metaKey and shiftKey and match the keycode/which values to capital variant of the keys
*	For checking multiple keys present at the same time like a + b, need to listen to both keydown and keyup events and match the order progmatically
* Due to large amount of variations in key events, may make sense to switch to a library for advance usage.

