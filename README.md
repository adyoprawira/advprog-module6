
# Module 6

## Commit  1 Reflection Notes


To process browser HTTP requests, I utilized a `BufReader` to wrap the incoming `TcpStream`. This enabled line-by-line reading of the stream using `.lines()`, where each line corresponds to a segment of the HTTP request. I then employed `.map(|line| line.unwrap())` to extract the `String` from each `Result`, and `.take_while(|line| !line.is_empty())` to delineate the request headers from the body, as HTTP uses an empty line as a separator. By aggregating these lines into a `Vec<String>`, I gained a clear, low-level view of the browser's request structure, enhancing my understanding of HTTP request internals.

## Commit 2 Reflection Notes

I learned how to serve an HTML file by enhancing the `handle_connection` function. The `fs::read_to_string("hello.html").unwrap()` function allowed me to load the file's content into memory. I then constructed a complete HTTP response, including the "HTTP/1.1 200 OK" status line, the "Content-Length" header calculated using `contents.len()`, and the HTML content itself. The `format!` macro was instrumental in assembling the response string, and `stream.write_all(response.as_bytes()).unwrap()` sent it to the client. I understood the necessity of the "Content-Length" header for proper browser rendering and the required structure of an HTTP response: status line, headers, an empty line, and the body.

![Commit 2 screen capture](/assets/images/commit2.png)