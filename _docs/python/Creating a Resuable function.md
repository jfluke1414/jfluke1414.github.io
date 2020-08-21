---         
order: 2         
title: (Python) Creating a Resuable function      
category: Python         
---         
         
```       
def emoji_converter(message):	      
   words = message.split(" ")      
   emojis= {      
      ":)" : "happy emoji",      
      ":(" : "sad emoji"      
   }      
   ouput = ""      
   for word in words:      
   output += emojis.get(word, word) + " "          
   return output      
      
      
message = input(">")      
emojo_converter(message)      
print(emojo_converter(message))      
      
```      
      
* should be Two black between function and next code