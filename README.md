# sfs
Static File Server

By using this package you can serve static files with __404 Error__ fallback to custom `http.handler`.

For example if you want to serve static contents of a __Single Page Application__, you can always serve `index.html` when 404 error occurs.

Example: 
```go
func main() {
	port := os.Getenv("PORT")
	if port == "" {
		log.Panic("$PORT should not be empty")
	}

	h := sfs.New(http.Dir("client/build"), IndexHandler)

	log.Fatal(http.ListenAndServe(":"+port, h))
}

func IndexHandler(w http.ResponseWriter, r *http.Request) {
	http.ServeFile(w, r, "client/build/index.html")
}
```
