```rs
use axum::{routing::get, Router, Json};
use serde_json::{json, Value};

#[tokio::main]
async fn main() {
    let app = Router::new()
        .route("/plain_text", get(plain_text))
        .route("/json", get(json));

    axum::Server::bind(&"0.0.0.0:3000".parse().unwrap())
        .serve(app.into_make_service())
        .await
        .unwrap();
}

async fn plain_text() -> &'static str {
    "foo"
}

async fn json() -> Json<Value>{
    Json(json!({ "data": 42 }))
}
```

```
http GET 127.0.0.1:3000/json
HTTP/1.1 200 OK
content-length: 11
content-type: application/json
date: Wed, 19 Jan 2022 12:54:36 GMT

{
    "data": 42
}

-----------------------------------------

http GET 127.0.0.1:3000/plain_text
HTTP/1.1 200 OK
content-length: 3
content-type: text/plain; charset=utf-8
date: Wed, 19 Jan 2022 12:54:44 GMT

foo
```