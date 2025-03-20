
# Module 6

## Commit  1 Reflection Notes


To process browser HTTP requests, I utilized a `BufReader` to wrap the incoming `TcpStream`. This enabled line-by-line reading of the stream using `.lines()`, where each line corresponds to a segment of the HTTP request. I then employed `.map(|line| line.unwrap())` to extract the `String` from each `Result`, and `.take_while(|line| !line.is_empty())` to delineate the request headers from the body, as HTTP uses an empty line as a separator. By aggregating these lines into a `Vec<String>`, I gained a clear, low-level view of the browser's request structure, enhancing my understanding of HTTP request internals.
