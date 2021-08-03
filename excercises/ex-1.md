

Create a docker image that includes a simpler web server that has the following apis/endpoints:

1. `/creation` - provides the time the image was built
2. `/dynamic` - a dynamic parameters / value provided when the image is built
3. `/dockerfile` - provides the dockerfile the image was created with (in the image)
4. `/` - returns an index.html file with any items u see fit (can be a simple hello)


Advanced:  
a.      Create a /put api that gets a file and stores it on the image runtime  
b.      Create a /get?filename which returns a file from the lcoal store (that was uploaded previously)  
c.       Add some css/js stuff to the index.html  
 