Results of testing kepress v/s keyup & keydown events across diffent browsers

#Chrome/Opera
##KeyPress

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                  |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------               |
|Up            |No 	       |          |             |       |        |			|                                          |			
|a             |Yes	       |a         | U+0041      | 97    | 97     |97		|                                          |			
|A             |Yes	       |A         | U+0041      | 65    | 65     |65		|                                          |			
|;             |Yes	       |;         | U+003B      | 59    | 59     |59		|                                          |			
|Shift+a       |Yes	       |A         | U+0041      | 65    | 65     |65		|No Shift Event                            |			
|Shift+A       |Yes	       |a         | U+0041      | 97    | 97     |97		|                                          |			
|Ctrl+Shift+a  |Yes	       |          | U+0001      | 1     | 1      |1 		|                                          |			
|Ctrl+Shift+b  |No	       |          |             |       |        |			|Same: ctrl+shift +b/d/i/z                 |			
|Enter         |Yes	       |Enter     | Enter       | 13    | 13     |13		|                                          |			
|Tab           |No 	       |          |             |       |        |			|                                          |			
|Control       |No 	       |          |             |       |        |			|                                          |			

##KeyDown

|Actual Key    |Event Fired|key       |keyIdentifier|keyCode|charCode|which |Comments                                  |
|--------------|-----------|----------|-------------|-------|--------|------|---------------------------               |
|Up            |Yes	       |ArrowUp   | Up          | 38    | 0      |38 		|                                          |			
|a             |Yes	       |a         | U+0041      | 65    | 0      |65 		|                                          |			
|A             |Yes	       |A         | U+0041      | 65    | 0      |65 		|                                          |			
|;             |Yes	       |;         | U+00BA      | 186   | 0      |186		| Different from press.Same: ( ,  + etc     |			
|Shift+a       |Yes (2)    |Shift     | Shift       | 16    | 0      |16 		|                                          |			
|              |Yes	       |A         | U+0041      | 65    | 0      |65 		|                                          |			
|Shift+A       |Yes	(2)    |Shift     | Shift       | 16    | 0      |16 		|                                          |			
|              |Yes	       |a         | U+0041      | 65    | 0      |65 		|                                          |			
|Ctrl+Shift+a  |Yes (3)    |Control   | Control     | 17    | 0      |17 		|                                          |			
|              |  	       |Shift     | Shift       | 16    | 0      |16 		|                                          |			
|              |  	       |A         | U+0001      | 65    | 0      |65 		|                                          |			
|Enter         |Yes	       |Enter     | Enter       | 13    | 0      |13 		|                                          |			
|Tab           |Yes 	     |Tab       | U+0009      | 9     | 0      |9  		|                                          |			
|Control       |Yes	       |Control   | Control     | 17    | 0      |17 		|                                          |			
 
 
#IE 11

# Firefox

# Safari 7 (Emulation)

#Observation


