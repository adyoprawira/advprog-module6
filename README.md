
# Module 6

## Commit  1 Reflection Notes


To process browser HTTP requests, I utilized a `BufReader` to wrap the incoming `TcpStream`. This enabled line-by-line reading of the stream using `.lines()`, where each line corresponds to a segment of the HTTP request. I then employed `.map(|line| line.unwrap())` to extract the `String` from each `Result`, and `.take_while(|line| !line.is_empty())` to delineate the request headers from the body, as HTTP uses an empty line as a separator. By aggregating these lines into a `Vec<String>`, I gained a clear, low-level view of the browser's request structure, enhancing my understanding of HTTP request internals.

## Commit 2 Reflection Notes

I learned how to serve an HTML file by enhancing the `handle_connection` function. The `fs::read_to_string("hello.html").unwrap()` function allowed me to load the file's content into memory. I then constructed a complete HTTP response, including the "HTTP/1.1 200 OK" status line, the "Content-Length" header calculated using `contents.len()`, and the HTML content itself. The `format!` macro was instrumental in assembling the response string, and `stream.write_all(response.as_bytes()).unwrap()` sent it to the client. I understood the necessity of the "Content-Length" header for proper browser rendering and the required structure of an HTTP response: status line, headers, an empty line, and the body.

![Commit 2 screen capture](/assets/images/commit2.png)

## Commit 3 Reflection Notes

I implemented conditional response logic in the handle_connection method, checking the request line to serve different pages based on the path. For the path /, the server responds with a 200 OK status and hello.html. For any other path (e.g., /bad), it returns a 404 NOT FOUND status and 404.html. Specifically, if the status line is GET / HTTP/1.1, the server returns hello.html with a success status. Otherwise, it returns a 404 error and the 404.html error page. Refactoring was introduced to improve code cleanliness and maintainability, splitting the response construction into separate functions. This enhances code readability and facilitates future scalability.

![Commit 3 screen capture](/assets/images/commit3.png)